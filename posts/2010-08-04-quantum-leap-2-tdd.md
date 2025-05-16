Title: Quantum leap No. 2, or why Test-driven Development will solve world hunger
Date: 2010-08-04
Tags: oop, story, tdd, biography

Before I was 11 I didn't even care if computers exist. Then, one day I randomly stumbled upon a book
about BASIC, the programming language.  _And then it began…_ I was totally blown away by the idea
that I could create my own worlds in code. I was eager to build smart, beautiful things, which are
able to make their own decisions, and be… alive, sort of.

For several years it was a constant creativity bliss: all those small programs and games I made and
never really finished — because new shiny ideas appeared faster than I could code.

And then I've hit the first brick wall. When a body of code grew big enough it started to become
unmanageable. I've been spending long hours debugging and guessing what could had been wrong, and
drove myself many times into complete despair. I was close to convincing myself that _I simply can't program_.

And exactly when I was in my professional dire straits, I discovered
[another book](http://www.amazon.com/Object-Oriented-Analysis-Design-Applications-3rd/dp/020189551X). And, a few months later,
[yet another one](http://www.amazon.com/Design-Patterns-Elements-Reusable-Object-Oriented/dp/0201633612).

That was my quantum leap No.1. The object-oriented programming. I've learned to build _really_
sophisticated shit. I mean **really**.  Usually, for a feature I did a few days of detailed up-front
OOD; played all those object interaction scenarios in my mind; and then writing the code was pure
formality. I made it compile, and then… it just worked! With unlimited undo/redo support, my own
object-relational mapping, C++ private class inheritance, Visitors, Builders, Chains of
Responsibilities, and many other “cool” things that made me feel smarter than I am.

That worked for quite a while. I mean it could last considerably longer before I found myself in the
same tar pit of debugging & guessing. However, something else emerged: people who were inheriting my
code complained it's too complex, and, well… too object-oriented.  And I thought “C'mon! Give me a
break! Too OO? What does that even mean⁈”, and sometimes even ”OMG, our industry is full of
incompetent amateurs!”

But then I gave it a second thought. Indeed, my heavily pattern-ized and tangled code with tons of
polymorphic calls is hard to follow.  Then, still, it may take longer, but in the long run, I end up
with a messy code base anyway.

“I was looking for an answer. It's the question that drives us, Neo.  It's the question that brought
you here. You know the question, just as I did…”

— _Must it really be that freaking complex?_

…And the answer found me.

— _No dude, it must not. Here's the trick: to keep it simple, you're not allowed to write more production code than it's necessary to satisfy a minimal failing test. Sounds crazy, but just let it go. Free your mind._

Oh, I did write unit tests before. Well, I _thought_ they are _unit_-tests. But I had no idea that
writing a test _first_ makes such a humongous difference. Here's why.

* Even the worst programmer in the world, like me, can actually program. Test/code loop is very
tight, and if you make a mistake, you catch it immediately. You can almost forget about
debugging. Anything that's broken was written not more than a couple of minutes ago.

* You are no longer afraid of change. If the tests run, you're fine.  And if they don't, you know
_exactly_ where the conflict is. You “don't think you are, you _know_ you are”.

* TDD makes the OOP really kick in. You feel the pain from violating the Law of Demeter, or from a
public static function _immediately_, and not half a year later, trying to make a change under
pressure of a big bang deadline. You know all your dependencies; the code becomes modular and
flexible.

* You get the best possible and 100% up-to-date documentation of your production code — the tests.

* Tests-first make over-engineering much harder. They keep you goal-oriented and focused on what's
truly important.

So, that's how I've made my latest level-up. I swear by TDD; and I full-heartedly agree with Uncle
Bob Martin: today, as a professional, you have no excuse not to follow this practice.
