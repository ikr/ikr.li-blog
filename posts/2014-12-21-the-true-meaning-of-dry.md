Title: The true meaning of DRY
Date: 2014-12-21
Tags: solid, design, best-practice

I've been listening to [Corey Haines](http://articles.coreyhaines.com/) talking about [his exploration](https://leanpub.com/4rulesofsimpledesign) of [Kent Beck's](https://kentbeck.com/) 4 Rules of Simple Design, and he has brought up an exceptionally important point about the Don't Repeat Yourself _(DRY)_ principle. DRY isn't about running an automatic repetition detection tool on your code base, and making sure it finds nothing. But rather it's about not repeating _the knowledge_ in the code. There's _incidental,_ and there's _essential_ repetition. Chasing the incidental repetition is a road to hell: things that look the same today will most certainly change differently in the future.

Just as almost everything else in software, the _essential DRY_ can be traced back to a paper from the 1970-s. This time, it's Parnas'es ["On the criteria to be used in decomposing systems into modules"](https://wstomv.win.tue.nl/edu/2ip30/references/criteria_for_modularization.pdf). Encapsulating a design decision into a module, suggested by Parnas, is pretty much equivalent to not repeating knowledge in the code.
