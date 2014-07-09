---
layout: post
title: "Consistency is not the key"
description: ""
category:
tags: []
---
{% include JB/setup %}

Everyone's heard it, probably everyone's said it and on the face of it it makes sense, "We need a consistent approach", "Consistency will make our code more maintainable", "Consistency will make it easier for new joiners to understand the code".  These days though, when it comes to software development, I've learnt to question everything and I'm questioning this attitude.

TLDR; Consistency certainly has a place in development but it should never restrict innovation and improvement.

The problem I have with consistency is that I find what it usually means is consistently doing something in a legacy way.  Lets take tools as an example.

I've just been pushing for a move from subversion to git.  Some of our projects have a problem with git so we have 3 choices:

1. Find a solution to the problem
2. Leave the problematic projects in subversion and move the rest to git
3. Stay using subversion

Option 1 is ideal but it may take too long or perhaps not even be possible right now.
Option 2 enables us to improve the way we work but we will have 2 places to go to to find our code.
Option 3 is avoiding innovation to maintain consistency.  We are conciously deciding to limit the scope with which we can improve our workflows and dev ops process, among other things.

For me it's obvious, start with option 2 and move to option 1 if you can.

Next we can look at code; instead of driving consistency, drive idiomaticity.  Idiomatic code is consistent, but it's much more than that, it's a way of writing your code that many people better than us have come to agree is usually best.  The word idiomatic doesn't seem to be used much in the Java/C# world but you find it all the time in functional language communities.  Idiomatic code is not just consistent within your team, it's consistent within the community.  It is not however, consistent in time.  Idioms evolve with a language, they are always up to date but that means you also need to stay up to date.

On to architecture.  This is the area where there is probably the most bad consistency.  I think some people think of architecture as something that should be decided upon once at the start of a big project and we should stick with it through thick and thin because architecture is hard to change.  To that I say, if it's hard to change then it's not a good architecture and you should improve it.  Architecture is the enabler of improvement, that is why it's so crucial to agile development.  It is also evolving quickly, new technologies and new ideas lead to new ways of architecting systems.  An architecture that seemed pretty good five years ago is almost definitely not the best way to do things now (although a lot of the concepts will still be the same).

Finally we have team process.  Consistency here should be used in a different way.  New ideas need to be given a chance before they are either accepted or modified.  You should maintain consistency in the majority of your process whilst you pick areas to expermint with.  Just make sure you consistently try new ideas!

Technology evolves so quickly that finding a good way of doing something and sticking with it means you are effectively going backwards.  If you don't make improvements to each of the 4 areas mentioned above every day then you will quickly find yourself in a legacy world of pain and you will not be able to keep up with the competition.
