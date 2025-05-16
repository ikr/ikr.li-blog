Title: The Agile (Shmagile) custom software development
Date: 2010-12-21
Tags: agile, story

At the point when Agile has hit the fan in Russia, I had already left two own-product-based software
companies; and since then was only doing custom software development. Therefore I will not
generalize, claiming that Agile movement is just a publicity stunt to sell seminars and Scrum Master
certificates, even though Steve Yegge
[says so](http://steve-yegge.blogspot.com/2006/09/good-agile-bad-agile_27.html). May be indeed it
works great _for products_. I don't know, and won't judge until I try. What I do know, is that some
of the core Agile practices are useless, and can even become harmful, — for the projects where
external customers ask to develop software for money.

What⁈ I must be [doing it wrong](http://www.youtube.com/watch?v=08xQLGWTSag). How can cute unicorns
and rainbows from the warm fuzzy Agile cloud do any harm? Alright, let's double-check
together. Here's my interpretation of what that core practices are.

The development is done in short (1—2 week) cycles. After each one a new functional version is
deployed on a productive server accessible by the customer. At the end of each iteration we announce
the results, present the new version at a meeting, and solicit the feedback. We briefly define the
features (user stories) we need to implement in the nearest future, and estimate how much work they
are. We also collect and prioritize all the feedback we receive along the way. Having assembled all
those elements into a regularly reviewed priority list, we'd just pick stuff from the top for the
next iteration.

Sounds pretty Agile, huh? I intentionally omit the code-related practices here. We'll return to them
later. For the moment, let's focus on _the process_.

So, that was _the theory_ of operation. Now, are you ready to meet _the reality_?

Let me make up a sample customer project for you. I may exaggerate a little for a deeper artistic
effect, but, if you've ever built software for a customer, you'd agree that's, in general, how stuff
is actually done in our sector of economy.

The imaginary application you'll build is going to be a legacy system rewrite. Actually, it'll be
the second attempt. Your predecessors failed miserably, but, because of some reasons, the customer
still believes that [rewrite is a good idea](http://www.joelonsoftware.com/articles/fog0000000069.html "Things You Should Never Do, Part I - Joel on Software"). So, you'll have the utterly worst possible specification: an existing system.

Probably, a conversation like this would take place at a kick-off meeting:

— The app [is really simple](http://raptureinvenice.com/?p=89 "Rapture In Venice: Is Good Code Impossible? Part 2: Project Manipulation Patterns"). Look! It even already exists!

— Hm, true, but…

— Oh, come on, [we can make it](http://www.youtube.com/watch?v=R2a8TRSgzZY "YouTube - The Vendor Client relationship - in real world situations")! We've even made a huge paper folder (aka _the folder_) full of screen shots of the existing system, so all must be clear.

— Well, we believe it should be possible to have a basic implementation of this functionality in a
year. But, for sure, no fancy stuff. Just a bare bones solution.

— Right, we can elaborate later. But you won't do a Web site with
[frames](http://www.htmlhelp.com/reference/html40/frames/frame.html "HTML Frame"), as it is now,
will you?

— Of course not.

— Perfect! So we'll have _all_ the same functionality, but implemented better. Expectations set.

— We'd like to develop iteratively: 2 week cycles. So that you clearly see the progress and have
full control. And we, in turn, can immediately react to change. Let's do it the _Agile_ way.

— What? Cycles? We didn't really plan that many meetings… But OK, we guess you know better how
software is developed.

So you start burning your development cycles. You keep deploying a new version every iteration,
making steady progress. Then, in a few months the customer asks:

— So, how are we doing? Is the project on track?

— Let us check… If we enumerate all the open functional points and the completed ones, and make a
proportion… Yes, it's still possible to release on time, but things are getting very tight because
of those two search module rewrites, and the complete front-end redesign we did according to your
feedback. We should be very careful planning the iterations, so that high priority issues make it to
the release, while not so important stuff we leave out of the first version.

— Huh? What do you mean — leave out? Haven't you seen _the folder⁈_ You promised us we'll have it
all in a year!

— But we thought we're doing it the Agile way…

— Look! We have an approved budget for this year, and when the year is over the application must be
100% done. Otherwise the project is a failure. Ah, by the way, we're already starting to plan the
next year's budget, and need you telling us what it takes to add a CRM, XML API-s, reports, bar
charts, PDF export, billing module, and SAP integration; we also need a mobile version of the app,
and two more system installations, which will be _exactly_ the same; well, may be a little
different… So, we need an estimation from you, and a plan. Yes, for the whole year.

— Do you have the specification for all that?

— No, sorry. But we're sure you'll offer us a sensible solution. Our budget meeting is in 3 weeks.

How much Agile would you feel in this situation? But wait, it can be worse. You naively believe that
the customer is _using_ the system you deploy at the end of each iteration. But — surprise — they
totally don't! The only time they pay any attention to the application is during your meetings. And
they are thoughtfully nodding then, asking questions — ultimately to conclude that the system is not
finished yet, and all those missing things they're asking about are coming in the following
iterations. Now imagine, [what happens](https://www.youtube.com/watch?v=zsTRxXvQY0s), when
they — the very first time — _really_ start using the system, only a year after the project started.

So, what do you think? Is the customer _wrong_ when acting like that? I don't think so. Well, at
least their position makes sense. They didn't come to you for Scrum master certification. They are
shopping. Shopping for software.

Now, imagine you're buying a car… Yeah-yeah, I'm going to throw a car metaphor at you. I discourage
it myself normally: it doesn't work for software. But that's how customers think. So, buying a car,
you're asking a dealer how much a family car would cost, with "standard" features. And instead of
telling you, he says:

— I have a better idea: let's _build_ a car together. We'll do it iteratively. So, say, in 2 weeks
you come and test how the 4 wheels roll in standalone mode.

What would you do then? I bet you'll go to a dealer who'll just show you a freaking price tag. You
can always find more than enough of them. And! We've been feeding this beast ourselves — by
accepting the long-term fixed price projects.

Isn't that a little depressing? OK, enough. Let's finish on a positive note. There are parts of
Agile that work great in customer projects. Test-driven development, collective code ownership,
continuous integration, (occasional) pair programming… Well, basically everything that doesn't
involve a manager. Those are the essential professional programmer disciplines today. And you're
very… brave if you aren't following them; especially in year-long fixed price projects, which aren't
going anyway any time soon.
