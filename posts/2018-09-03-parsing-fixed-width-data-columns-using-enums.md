Title: Parsing fixed-width data columns using enums
Date: 2018-09-03
Tags: kotlin, java, idiom, pattern, jvm

This week at work I had to deal with [fixed-width column data like this.](https://www.six-group.com/interbank-clearing/dam/downloads/bc-bank-master/bcbankenstamm) That is: a plain text file where each line holds a single record with a predefined order of columns/fields. Each column has a predefined length (in symbols), and, if the value is shorter, it's padded with spaces. Every line contains every column, and, therefore, every line has exactly the same length. For example,

     Field A | Field B   | Field C     |…
    01234567890123456789AB0123456789ABCD…
    X         YYY         ZZZ           …
    …

having the lengths of 10, 12, and 14 respectively, would be

```javascript
[{
    A: "0123456789",
    B: "0123456789AB",
    C: "0123456789ABCD"
}, {
    A: "X",
    B: "YY",
    C: "ZZZ"
}, …]
```

Parsing the data, I came up with a very natural approach which relies on [Kotlin/Java
enums.](https://kotlinlang.org/docs/reference/enum-classes.html#enum-classes) Nothing groundbreaking
or novel here. I'm sure this trick is familiar to many. However, I liked how naturally the tool
suits the problem, and decided to share.

```kotlin
fun parseLine(rawData: String): BankRecord {
    val parseStringBound = { f: RawBankDataField -> parseString(rawData, f) }

    return BankRecord(
        clearingNumber = parseInt(rawData, RawBankDataField.CLEARING_NUMBER),
        name = parseStringBound(RawBankDataField.NAME),
        postalAddress = parseStringBound(RawBankDataField.POSTAL_ADDRESS),
        postalCode = parseStringBound(RawBankDataField.POSTAL_CODE),
        city = parseStringBound(RawBankDataField.CITY)
    )
}

data class BankRecord(
    val clearingNumber: Int,
    val name: String,
    val postalAddress: String,
    val postalCode: String,
    val city: String
)

private fun parseInt(rawData: String, f: RawBankDataField): Int {
    return parseString(rawData, f).toInt()
}

private fun parseString(rawData: String, f: RawBankDataField): String {
    return rawData.substring(indicesRange(offset(f), f.length)).trim()
}

private fun indicesRange(start: Int, length: Int) = start.until(start + length)

private fun offset(f: RawBankDataField): Int {
    var result = 0

    for (i in RawBankDataField.values()) {
        if (i == f) return result
        result += i.length
    }

    return result
}

private enum class RawBankDataField(val length: Int) {
    GROUP(2),                       // Gruppe
    CLEARING_NUMBER(5),             // BCNr
    SUBSIDIARY_ID(4),               // Filial-ID
    NEW_CLEARING_NUMBER(5),         // BCNr neu
    SIC_NUMBER(6),                  // SIC-Nr
    MAIN_OFFICE_CLEARING_NUMBER(5), // Hauptsitz
    CLEARING_NUMBER_TYPE(1),        // BC-Art
    VALID_SINCE(8),                 // gültig ab
    SIC(1),                         // SIC
    EURO_SIC(1),                    // euroSIC
    LANGUAGE(1),                    // Sprache
    SHORT_NAME(15),                 // Kurzbez.
    NAME(60),                       // Bank/Institut
    DOMICILE_ADDRESS(35),           // Domizil
    POSTAL_ADDRESS(35),             // Postadresse
    POSTAL_CODE(10),                // PLZ
    CITY(35)                        // Ort
}
```

Note that, like in this example, we may need just a subset of the fields present in the data
source. Nevertheless, obviously, we'd have to _enum_-erate all the columns anyway, up to the
rightmost relevant to us. I particularly like that it's so easy to adapt to the changes in the data
source format, and to support additional columns.

I only have to say that, if you have a lot of relevant fields packed into the data line, and a lot
of lines, you may wish — for a better performance — [to
memoize](https://en.wikipedia.org/wiki/Memoization) the `offset()` function.
