---
layout: post
title:  "How to Integrate Analytics Frameworks in your App"
date:   2021-06-02
image: /images/posts/analytics.jpg
tags: [tech, mobile, product]
---
Data on product usage is essential for most teams. Dozens of SDK options are available, many with unique value to provide to product owners. When integrating these frameworks into your app, take caution. Clean data is essential for insights. A little foresight on creating testable solutions will ensure your data is consistent and useful.

<!--more-->

## Story Time - How Teams Get into Trouble with Analytics Frameworks
Let's walk through a perilous scenario I've encountered with dozens of teams. Your product team has settled on an analytics framework to integrate into a suite of applications. Time to get to work.

### 1. Product owners and data analysts write analytics requirements
When event X happens, send an event name and an additional payload that provides details around the event. Maybe the user tapped on an ad. Maybe they exited a workflow early. Whatever the events are and the contextual data to accompany them, they should be sent to the analytics SDK or API.
![Writing requirements](/images/posts/analyticsFramework/requirements.png)

### 2. Programmer implement the requirements
This process, particularly when teams are in a rush or junior, is to import and configure the framework upon app startup, and then call `SDK.sendEvent()` throughout the app. Seems innocuous enough, particularly when most tutorials instruct developers to do this exactly.
![Implementing requirements from a tutorial](/images/posts/analyticsFramework/requirementsImplementation.png)

### 3. App deploys
The analytics work is dev complete, and the app is deployed to some environment. Users begin testing that events are fired and show in the analytics portal. Testing is tricky here. Often a quality engineer will announce "no one use the app for the 4 hours! I don't need to analytics portal cluttered with other people's events."
![Away it goes!](/images/posts/analyticsFramework/deployment.png)

## Trouble
At this point, the team is struggling.
1. Slow cycle time
Dev to deployment is a long time to test. Asking your team to freeze work while manual testing occurs slows things down further. To compound the issues, some data problems likely won't be uncovered until the app is in production.
![That's a lot of steps to start testing](/images/posts/analyticsFramework/slowCycleTime.png)

2. Incorrect, inconsistent, or missing data
Some data points won't match requirements, and some will differ slightly across platforms based on developer interpretation of requirements. Your team went to all this trouble to generate useful insights, but the data on the other end isn't trustworthy! Maybe your data team can clean it up on the other side, maybe.
![Oops. Typos happen.](/images/posts/analyticsFramework/codingErrors.png)

### Plot Twist! Product Needs Another Analytics SDK
Different tools have different value props, or maybe they are similar and product owners want to compare in production to see which one meets their needs. Regardless, this simple ask means big trouble for delivery teams. All of the previous problems are doubles, plus they have the new problem that data inconsistency not only spans apps, it spans analytics platforms!

## A Better Way - Test as a Team During Development
This story is a common one, and the solution is a simple one, yet I rarely see companies utilize it. Take a breath, and let's slow down a little bit to ultimately go a lot faster.

Here is a formula I've successfully deployed nearly a dozen times.

### 1. Inject a Lightweight Analytics Abstraction Layer in Code
Use a protocol (interface for you Swift folks) to talk to analytics SDKs. This basic dependency injection is textbook "inversion of control", meaning that your team is in control of how to communicate with analytics SDKs, rather than the inverse.
![Might seem obvious, but most teams slip up here.](/images/posts/analyticsFramework/frameworkInjection.png)

### 2. Substitute a Fake SDK that Writes to a File
Rather than integrating the SDK now, send your output to a file. This file is a clutch asset! Product, data, and quality team members can validate against this file rather than waiting on data to show up in the analytics portal.
![Intermediate source of truth](/images/posts/analyticsFramework/writeToAFile.png)

Okay the TDD purists are saying you should write tests before doing this. Yes, in practice, but for story telling's sake, I'm shifting the order up a bit.

### 3. Test to Ensure Results Stay Consistent with Requirements
Unit tests ensure that the payload for different events is as expected. Integration tests ensure that the proper event fire's the expected event name and payloads. Bonus if your data analysts help write the tests! This extra layer of quality control helps with typos and shifting requirements.
![Quality control shifted left ftw](/images/posts/analyticsFramework/testThroughout.png)

UI automation tests are helpful to ensure the expected event behaves as it should. Implement these if practical for your app.

Now you are ready to integrate the analytics SDK and explore full stack testing options.

### Enter a New Framework
This time when product needs a new SDK, the team is setup to consume it! A single chokepoint in the code base is where the SDK event handling is integrated. Code review is light, and test coverage is high.

![New SDK? No problem.](/images/posts/analyticsFramework/newFramework.png)

I hope this process is as helpful for you as it has been for me.

Thanks for reading!

