Title: Well, I guess sometimes you just need stuff being mutable
Date: 2011-09-26
Tags: clojure, functional, php, prime

I’ve been generating some prime numbers in Clojure lately, and I was struggling to get decent
performance when working with “idiomatic” immutable sequences. I’ve started with a naive
implementation of a lazy prime sequence:

```clojure
(defn denormalized-prime-indicator [n smaller-primes]
    (reduce
        *
        (map
            #(rem n %)
            (filter #(<= (* % %) n) smaller-primes))))

(defn prime-rel? [n smaller-primes]
    (if (> (denormalized-prime-indicator n smaller-primes) 0) true false))

(defn next-prime [cnt smaller-primes]
    (if (prime-rel? cnt smaller-primes)
        cnt
        (recur (inc cnt) smaller-primes)))

(def prime-seq
    (map last
        (iterate
            (fn [p-seq]
                (conj p-seq (next-prime (inc (last p-seq)) p-seq)))
            [2])))
```

It took over a minute to compute all the primes under 200'000, and over 2 hours to crunch till
2'000'000. Then, I went for
[Sieve of Eratosthenes](http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes):

```clojure
(defn primes-below [n]
    (loop [primes [] source (range 2 n)]
        (if (empty? source)
            primes
            (recur
                (conj primes (first source))
                (doall (filter #(not (= (rem % (first source)) 0)) source))))))
```

Here, n = 200'000 took 24 seconds, and n = 2'000'000 — 44 minutes. Kind of an improvement, right? By
the way, mind the “doall” at the last line. If you remove it, the poor thing dies from heap
overeating, when lazy “filters” stack on top of each other long enough.

Still, 44 minutes for a 2'000'000-limit? That sounds just too slow. Therefore, I wrote a quick and
dirty sieve function in PHP, and verified I’m getting the same results by checking the numbers' sum:

```php
<?php

$sieve = array_fill(0, 2000000, true);

$sum = 0;
$p = 2;

while ($p < count($sieve)) {
    $sum += $p;


    for ($i = 2 * $p; $i < count($sieve); $i += $p) {
        $sieve[$i] = false;
    }

    $p++;

    while (($p < count($sieve)) && !$sieve[$p]) {
        $p++;
    }
}

echo "$sum\n";
```

Time to find all the primes under 2'000'000? Two freaking seconds. If you bother writing this in C,
you may shrink it down to under 100 ms, I’m sure.

Wait, but what if I do need generating primes fast in Clojure? And the answer found me

```clojure
(defn sieve [n]
  (let [n (int n)]
    "Returns a list of all primes from 2 to n"
    (let [root (int (Math/round (Math/floor (Math/sqrt n))))]
      (loop [i (int 3)
             a (int-array n)
             result (list 2)]
        (if (>= i n)
          (reverse result)
          (recur (+ i (int 2))
                 (if (< i root)
                   (loop [arr a
                          inc (+ i i)
                          j (* i i)]
                     (if (>= j n)
                       arr
                       (recur (do (aset arr j (int 1)) arr)
                              inc
                              (+ j inc))))
                   a)
                 (if (zero? (aget a i))
                   (conj result i)
                   result)))))))
```

It’s a sieve-with-hints function written by someone under the moniker "rhickey" ;) and it uses… Java
arrays, reaching 2'000'000 limit in about a second.

So, that’s how I learned to stop worrying and love mutable arrays.
