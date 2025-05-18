Title: On components and modules
Date: 2016-10-14
Tags: software, architecture, composition, abstraction, module, component

At the place where I [work currently](http://www.xiag.ch/), we tend to prefer multiple independently
deployable small software _components_ to huge single-piece monoliths. Component is an overloaded
term that can easily be misinterpreted. By _component_ I personally mean something very specific. To
avoid the ambiguity, let me first enumerate what it's not. A component is not a programming language
namespace or class, it's not a file, and not an in-process linked library like a jar, a dll, a
Composer- or an NPM package. Component is a unit of deployment, and is also an _actor._ "Actor"
means it's, well, active -- running in its own process, initiating events, or reacting to events.

As many others these days, we found following the
[Microservices](http://martinfowler.com/articles/microservices.html) architectural style quite
beneficial. Normally, we connect components to each other via HTTP, or via message-oriented
middleware, passing data around in JSON format. Thus, a component either serves HTTP requests, or
reads from- or writes to a message queue. That flavor of Microservices style has a number of
benefits:

* HTTP -- all the goodies of the Web (caching, proxy-ing, gzip-ing, basic auth, accessibility and
  readability -- just `curl` it or access from the browser directly)
* Easy composition: piping stuff into stuff, `curl`, `json`, and `ramda-cli` can get you very far;
  often you can implement a whole new feature in a few lines of Bash
* Super-low coupling
* Parts are easy to understand
* If a component has rotten beyond recovery, just rewrite it; no big deal
* Freedom in choosing the programming language for each component independently
* Coherent and fast test suites
* Scalability
* Statelessness
* Value-based, data-oriented interfaces

It's not all bright and happy, of course. Microservices come with a price, and also caused us a
certain bit of pain. That's not the point of this post though. Instead, I want to claim that good
modularization is essential to software project success whether you opt for microservices or
not. What is a _module?_ I'd say it's any unit of abstraction: very broad, very general thing. It's
pretty much any building block for constructing software.

Not every _module_ has to be a microservice -- thus, a separate _component._ Very often an
in-process [Composer package](https://packagist.org/) or [npm module](https://www.npmjs.com/) is
a perfectly appropriate building block.

It's quite a widespread fallacy to conflate the deployment architecture view, and the logical
architecture view. One may hear "We're not Facebook to care about microservices, therefore it's OK
to toss all the code into a single amorphous ball of mud -- aka The Monolith". That's a false
dichotomy, of course. There's nothing inherently wrong with a monolithic application in the
deployment view: a single process of execution, one application server listening on a network
port. Facebook itself is a single multi-gigabyte-large executable file. Yet, there's pretty much
everything wrong about a monolith in the logical view: no clear-cut borders between modules,
everything depends on everything else.

Coming down to the basics, why exactly should we (1) split a software system into modules, and,
_also,_ (2) strive to keep those modules in separate repositories in a version control system? The
(2) is my personal opinion I'd like to substantiate.

Let's start by answering the first question. As a matter of fact, a Turing machine couldn't care
less whether we glue the tape together from separate strips or not. The tape cut is required by our
limited minds to disassemble a hard problem's solution into digestible pieces. Abstraction and
composition are the only two weapons we have to combat the complexity. Software development lives
and dies by the composable abstractions _of just the right size._

Now, let's go on to the second question. Is it possible to have composable abstractions of just the
right size within a single Git repository containing all the application's code? Yes, of course!
Then, though, the "just the right size" part comes into consideration. Abstractions within the
application [work best](https://en.wikipedia.org/wiki/Separation_of_concerns) when each has the
[only reason to change](https://en.wikipedia.org/wiki/Single_responsibility_principle) -- it's own
technical or business _concern._ To which programming language construct -- say, in PHP -- such a
concern [bijectively](https://en.wikipedia.org/wiki/Bijection) corresponds? A function? No. A class
or a trait? Definitely not. A namespace? That probably is the closest approximation, which may
actually work given a cast-iron discipline of the project participants. However, namespaces don't
accommodate well artifacts like database schemas and stored procedures, or cronjobs.

Conclusion: concern boundaries in a single-repository monolithic code base are seriously
blurred. What can prevent crossing those boundaries and slowly but surely crawling to the
[Big Ball of Mud](http://www.laputan.org/mud/) architecture, where everything depends on everything
else? Only the clear understanding and active enforcement of consistent program design, and the
aforementioned discipline. How realistic is to expect that in an ordinary project, where not all the
developers are seniors with over 15 years of industry experience?

Thereby, principally, modules isolated into their own source code repositories are the concerns'
border guards. That purpose of modularization will stay relevant forever, even when computers become
a million times faster.

So, what do we want? Composable modules with clear-cut borders! Do we want them actually to work?
You bet!

The easiest way I know to ensure that the code works correctly is the test-driven development
(TDD). Is it possible to practice TDD when a unit test suite's run time is, say, over 10 seconds?
Definitely not! That imposes an objective hardware-bound restriction on how big of a module one can
build. Indeed, computers get faster or more parallel all the time. On the other hand, programming
languages and platforms get more sophisticated, and tend to do more and more things. May well be
that those two opposing trends will compensate each other eternally.

So, the next time you'll be adding a file to your code base, may be consider sprouting a new module
with its own repository instead?
