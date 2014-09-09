---
layout: post
title: "Static vs Dynamic"
description: ""
category:
tags: []
---
{% include JB/setup %}
I have recently moved jobs and now I am using Clojure rather than Java and Scala.  Before starting I had been reading up on the static vs dynamic typing argument.  I enjoy all the type stuff, when you start learning Haskell and Scala there's some really interesting things to learn and some parts of static typing can really help.  Most noteable for me is function signatures, I really find function signatures to be one of the best things about static typing.

Once I started using Clojure, however, I was amazed how productive and fun it was.  Using functional Scala and Haskell makes you feel clever and when you get something working it's really satisfying, using Clojure though is just plain fun!  It's so productive, the feedback is instant (I'd recommend trying Light Table with it's inline evaluation) and you don't have to fight against the type system.

Of course this comes at a cost, the main downsides supposedly being

1. difficult to understand and navigate a large codebase
2. lack of refactoring in tooling
3. it's slow
4. minor bugs that would have been caught by the type checker

The comapany I moved to has a fairly large and complex codebase of a reasonable age (around 4 years) but I was amazed at how easy it was to understand and navigate.  I have no doubt that you could make something truely incomprehensible with Clojure but the thing is it doesn't actually lend itself to this.

First of all it's pretty terse: Before I started my new job I re-wrote a program in Clojure that I had recently written in Groovy.  I compared a function for manipulating some data that was reasonably complex, both the Groovy and the Clojure version were the same size in terms of lines of code.  However the Groovy project was around 1300 lines of code verses around 350 for the Clojure project!  This suggests to me that a huge amount of space was taken up by the Java-style boilerplate code required, lets multiply that by 10 and imagine how easy a codebase of 3000 lines is to understand compared to 13000...  I have no doubt that a Java version would have been even worse.

Something else about the maintainability of a decent size codebase in Clojure is that the culture is that of making small, specific libraries and spending time thinking about the API of these libraries.  This leads to quite a lot of projects but good separation of concerns.  It also makes it easier to open source parts of your codebase.

Moving on to refactoring and tooling, I definitely found there were a few refactoring features I missed, find usages in a project was the biggest one.  However I found, as I had read, that with Clojure, text manipuation is far more important than cross-file refactoring.  I didn't really miss much and there's a lot to be said for weak autocomplete actually forcing you to understand the code better.

Speed is an interesting one.  Clojure can be optimized to be not far off the speed of Java however you sacrifice idiomaticity and it will never be quite as fast.  The thing is though that this single thread speed is not often a requirement, especially as Clojure makes parallelism much easier.  When it becomes an issue though, it is quite easy to integrate Java for performance, a good quote is from the http-kit blog, "Clojure + JAVA = Performance + Nice API".

Finally we come to bugs.  I'm not sure about this, I imagine it's true but I haven't been working with Clojure long enough to see.  So far I haven't come accross a bug that would not have existed with a type checker but that's just circumstantial.

Perhaps in a few years I'll change my mind but for now I'm sold on the advantages of dynamic languages and I'm embarrased to say that I have even become a bit if a Clojure fan-boy :(
