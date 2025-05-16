Title: My humbly strong opinion on frameworks
Date: 2010-11-01
Tags: programming, framework, library, DSL

I'm not really a fan of general purpose heavy weight software frameworks like Ruby on Rails. Usually
you get fast bootstrap, but — because of insufficient knowledge of how things work inside (aka
magic) — you inevitably end up struggling with the framework instead of leveraging it. It may take a
few years until you can fluently use the tool. And then it becomes an investment you're reluctant to
give up. Actually, you loose your freedom, and obediently accept the "framework X programmer" label
attached to you. Which in construction business would sound like “a hammer specialist”.

Also, with all the deep knowledge you finally have acquired, you start feeling the boundaries: you
notice you're shoehorning your solution into something not quite appropriate. And then, all those
new shiny Sinatra-s, Lift-s, and node.js-es come. And you find out that one of the new fab toys
solves your current application's main problem just “by definition”. But… you've already committed
to the framework X, and, until the pain gets utterly intolerable, you won't switch.  Ultimately, the
story repeats with a framework Y then.

So, is there a better alternative? May be. An application-specific DSL-ish approach looks very
promising. That's when you build and evolve a kind of internal domain specific language, tailored
exactly to your application. I've shown an example
[earlier today. That's how](http://gist.github.com/658387) I wish I could work with persistent
objects and their HTML forms in my current Web app.  However, it's hard to judge the example without
the application context. Abstractly, it just feels like RoR. But the whole point here is that you
don't try to be in any way generic. Your “DSL” is minimal, and supports only what the application
needs. All the dates displayed in the GUI have the predefined format, a known JS date picker widget
is used; page element styles, menus, and navigation are known and fixed; and so on. No scaffolding,
it's all productive right away.

Basically, to achieve that DSL-ish effect, you DRY your app like crazy. Let you laziness drive you:
be impatient of _any_ repetition in coding.

Of course, that doesn't mean you must start each new project with a clean slate. You'll be able to
adapt a lot of past code, and, if you're lucky, or doing the same stuff all the time, even to
extract some rather generic components. But, if you're an application developer, please don't try to
build “a framework” of your own. Most likely it'll suck.
