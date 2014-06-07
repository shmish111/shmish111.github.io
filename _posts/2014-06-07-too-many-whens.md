---
layout: post
title: "Too many Whens"
description: ""
category:
tags: []
---
{% include JB/setup %}
I've put in quite a lot of effort learning about automated testing in the last few years and have become quite passionate (some may say opinionated) about the subject.  Through trial and error, reading and working with some experienced QAs, I've formed some rules for myself about how I write BDD style tests.  I'd like to share one of these as I can't find anything on the internet that suggests or explains it.  The rule is:

A scenario should only ever have one 'When' statement.

Consider the scenario below:

    Given a user logs in
    And the user is an administrator
    When they click on 'my profile'
    And they click on 'view my cart'
    Then their shopping cart should be displayed
    When they click on an item
    Then the item details should be displayed
    And the price should be displayed

I've seen similar scenarios to this many times. It could be made a lot clearer by applying the 'When' rule:

    Given a user logs in
    And the user is an administrator
    When they click on 'my profile'
    Then the 'view my cart' button is displayed

    Given an administrator is on the 'view cart' page
    And the cart contains items
    When they click on an item
    Then the item details should be displayed
    And the price should be displayed

In order to apply the rule it was necessary to split the scenario into two.  With a bit of practice and attention you eventually see that every scenario can be viewed as a state transition.  The system starts in state A, an action is performed, the system is now in state B.  Uncle Bob wrote about this way back in 2008 [The Truth About BDD](https://sites.google.com/site/unclebobconsultingllc/the-truth-about-bdd).

I challenge you to find a feature that is not clearer and easier to understand when it has only one When in each scenario.

That's all well and good when we are just writing specifications, but what happens when we start to use these specifications as automated tests? There is a weakness in this method; by ensuring only one thing is tested at a time, the state of the system needs to be set up more often.  For example, in the scenarios above we will need to log in to the system twice instead of once, a UI automation task that could be quite expensive and slow down our test suite.

In some situations it is just not practical to do this and clarity and detail must be sacrificed in order to make the tests usable.  However I feel that too often people will state this reason, do more manual testing, produce lower quality software and become less agile when perhaps they could spend some of this time working on ways to speed up the test suite.

Have a go writing your scenarios using this rule and see what happens.  If you think it's not practical for some of your tests, challenge your team to make the tests run faster, by parallelizing them for example (I've got some ideas on this I'll put in another post).
