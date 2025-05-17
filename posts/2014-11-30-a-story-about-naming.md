Title: A story about naming
Date: 2014-11-30
Tags: story

Long time ago I contracted for a company selling digital photo prints. Me and a colleague of mine
developed an MS Windows application in which you would drop some JPEG-s, crop, rotate them, fix some
red eyes, and then ultimately order prints in various formats. And by Windows I mean the just
released XP -- that's what _I_ had back then; while our lowest supported OS was Windows 98.

There was a twist though: the _customer_ wanted a _custom_ look for the application. Very, very
custom. So custom that we had to cover the whole window client area with bitmaps. Now, add to that
numerous states of controls: disabled, pressed, checked, disabled and checked, mouse hovering,
etc. Then, there was no transparency support for bitmaps, as there was no GDI+ for Windows 98 and
Windows 2000. Therefore, graphic designers had to draw every text on every background, for every of
the 4 supported languages in Photoshop, with their nice font, and then give it to us as... correct,
a bitmap.

Ever since I've never had a project with accidental complexity that high. A tiniest thing required
tons of work and rigorous attention to details. But that's not the point of the story, actually.

So, as you can imagine we've ended up with _thousands_ of bitmaps and color constants. They were
stored, of course, as _resources_ in resource DLL-s, one DLL per language, and their ID-s were
aliased with `#define`-s in a long `resource.h` file. That was a pretty standard setup for the
old-school Win32 apps. On top of the resources we had an object-oriented widgets implementation,
often doubling in the object properties in `camelCase` the `CONST_CASE` names from
`resource.h`. Now, the interesting part was how we named our visual elements. Here are some examples
for you:

* `lightBlueBackground`
* `redButtonDisabledText`
* `blueFrameLeftTopCorner`
* `yellowishGradientInTheCenter`

Thus, the names reflected what color or pattern elements had, or where they were located in the GUI
layout. We often reused the same visual element in multiple widgets. A light blue gradient could
easily appear in a dozen of different places.

After a few months we've successfully shipped the first version, and plenty of end users could
appreciate our unique and fresh custom look. He-he. That was sarcasm. Frankly, I was quite glad it
was all over.

Then, about a year later we've got a call. The customer was really excited: they were expanding to
Scandinavian market -- buying a Swedish, a Norwegian, and a Finnish digital photos printing
company. Oh yeah, and they were also running a total re-branding in Switzerland. They were even
going to change the company name. Now guess whose brilliant ordering software they wanted to use for
all the new brands... While you're at it, guess how many of the `lightBlueGradient`-s stayed either
light or blue in any of the new brands' GUI-s. Yep, you guessed it right: almost none. Moreover,
many visual elements used in several places in the current version -- just because it was all, say,
yellowish -- were going to get a completely different look in the new revision. And finally, let's
not forget that instead of 4 bitmap localizations we were going to support 7. What an epic
surprise...

So, the next time you get an idea of calling something a `redHeader` or a `rightColumn`, may be just
stop for a moment, and think if that's really the best you can do.
