---
layout: post
title:  "Beacons: You’re Doing it Wrong"
date:   2015-11-13
image: /images/posts/beacons/beacons.jpg
tags: [mobile, tech, ble]
---

Beacons are a powerful technology at the forefront of bridging digital and physical experiences. They provide [assitive technology to those with blindness](http://blindsquare.com/about/) and [show us how to navigate airports](http://blindsquare.com/about/), but how? Beacons are often misunderstood. They are used for less than ideal purposes with hacky implementations. Let’s clarify when and how to use beacons.

<!--more-->

## What Does a Beacon Really Do?
> The core use case of a beacon is this: have a phone do something when it enters an area.

That’s it.

What makes this functionality particularly useful is that it works even when your app isn’t running. When the phone comes within range of a beacon, the app wakes up in the background to perform a task.

The duration your app is awake to do work is only 3–5 seconds. Developers can kick off other background processes in that time. When developing background processes for beacon interaction, remember you are on the clock.
Don’t try to fit a square peg into a round hole. If your use case is different than what beacons are designed to do, be open to other technologies.


## Beacon Misconceptions

Clients often approach me with grand ideas for how to integrate beacon technology into their apps. Many of these ideas are great, but oftentimes beacons aren’t the best solution to their problem. I’d like to clear up some common beacon misconceptions.

### Myth: Beacons and Phones Have an Open Dialogue

Beacons are not terminals of information that can respond to information from the phone. They aren’t even aware of any devices other than themselves.

> Beacons are dumb. Their uses are powerful.

Not This:
![Complex Beacon Scenario](/images/posts/beacons/notThisBeacons1.png)

This:
![Simple Beacon Scenario](/images/posts/beacons/thisBeacons1.png)

### Myth: Beacons Have Precise Ranges

Beacons aren’t fit for coupon redemption or mobile payments. The range is too imprecise. Wallet or QR codes get that job done. Apple’s documentation states that beacon accuracy “is heavily subject to variations in an RF environment.” Also, the range isn’t a sphere. All sorts of environmental factors change the shape of a beacon’s range.

Not This:
![Ideal Beacon Scenario](/images/posts/beacons/notThisBeacons2.png)

Beacons are built on Bluetooth Low Energy (BLE) which is subject to interference, particularly from water. Because 60% of the human body is water, crowded spaces cause some crazy variation in beacon ranges.

This:
![Real World Beacon Scenario](/images/posts/beacons/thisBeacons2.png)

Yes, beacons can be used for indoor wayfinding, but they’re not as robust as GPS. For navigation, the phone is constantly searching for nearby beacons. This is the opposite behavior of the ideal beacon use case. Apps are asking for beacons rather than being told when beacons are nearby. **Searching for beacons kills battery life!**

First try iOS Indoor Positioning. If that doesn’t give you the results your app needs, then consider beacons.

## How to Find Your Location
If you do use beacons for wayfinding, know that reverse-engineering the phone’s position from beacons is different than most positioning algorithms.

[Trilateration](https://en.wikipedia.org/wiki/True-range_multilateration) is the process of finding a location, assuming the location is known distances from known points. Put another way, it finds the intersection of three circles.

Not this:
![Won't Work Beacon Scenario](/images/posts/beacons/notThisBeacons3.png)

The problem with this process is that beacons don’t give a precise distance to the device. They give a range.

This:
![More Realistic Beacon Scenario](/images/posts/beacons/thisBeacons3.png)

Still, this info can give us a pretty good idea of where the phone is. Here’s how:

1. Find circle intersections. Use trilateration to find the intersection points of all inner and outer ranges of the phone’s distance from each beacon.
![Find Intersections](/images/posts/beacons/thisBeacons4.png)

2. Throw out bad points. Points that are inside the minimum or outside the maximum of any beacon’s range are invalid.
![Remove Bad Points](/images/posts/beacons/thisBeacons5.png)

3. Find the centroid. The centroid is calculated by averaging the positions of the remaining points.

4. Filter noise. Some of the values returned will be bad data. Be sure to look for anomalies or the user’s position may jump around the map.

Greater beacon density provides smaller ranges and yields more accurate positioning.

## When to Use Beacons

### Contextual Displays

A potential new hire is coming by the office. You’re in back-to-back meetings and won’t be at the door to greet her if she arrives early. Instead, she’ll see a digital display. It provides relevant information such as meeting room location and where to find the beverages.

This personalized information can be streaming on a display at all times, OR it can show up only when the candidate walks into the lobby. When designing apps like this, it’s important not to overthink the role of beacons. The only thing a beacon does here is trigger the process for retrieving and displaying the candidate’s information. Simple yet powerful.

### Pre-loading Promotions

Beacons are a great way for retailers to tell your app that you are near a store, or even a section of the store. If each location provides different specials, the relevant local deals can be retrieved by the app.

Although beacons are not the right tool to push the promotions to the phone, they can trigger the action to start the retrieval process. The Starbucks iOS app does a great job of this without bothering the user. Consider pushing the deals via a Bluetooth device at the retail location. That way you aren’t eating up a customer’s data plan.

### Indoor Positioning

If you must (see above).

## When Not to Use Beacons

**Use Case** | **Beacon Alternatives**
Coupon Redemption | Wallet, QR Codes
Details on each item in a store |Bar code scanners, OCR
Deciding if a meeting room is occupied | Motion Sensors, microphones, heat sensors
Pushing data to a phone | Cloud server, Bluetooth

## First What. Then How.

Beacons provide a simple yet powerful service. They notify your app of an event: user entered a region. Use beacons wisely. Be open to other hardware when beacons aren’t doing what they do best. When designing apps, we need to first define the problemset, then decide on the solution. Sometimes beacons are the perfect fit. Oftentimes they’re hired to do the wrong job.