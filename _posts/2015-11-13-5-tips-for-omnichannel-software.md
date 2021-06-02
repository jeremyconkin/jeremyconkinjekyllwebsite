---
layout: post
title:  "5 Tips for Building Omnichannel Software"
date:   2015-11-14
image: /images/posts/omnichannel.jpg
tags: [tech, product]
---

5 Tips for Building Omni-Channel Software
The landscape of "mobile" is ever expanding: phones, wearables, IoT and phablets are just a few areas where we're seeing rapid, technological advancement. As a business, keeping pace is not only a challenge - it's overwhelming. New platforms can be deterrents for organizations that have rigid content delivery models. However, the organization that is properly prepared can leverage these platforms as opportunities.

Here are 5 tips to help you create a successful, omni-channel software strategy.
<!--more-->

## 1. Separate Your Brand from Your Technology
Companies that succeed across mediums focus on core values rather than one-off experiences. New platforms become additional entry points to the same brand, and by embracing the ever broadening technology landscape, companies actually narrow their focus to the core of who they are. By defining the underlying principles of a brand, companies have a strong blueprint for new business opportunities.

Nordstrom demonstrated this with their acquisition of Trunk Club. Trunk Club delivers premium clothing selected by a customer's personal stylist. It focuses heavily on customer service and touts a user-friendly return policy. These values - personalized customer experiences, high satisfaction after the point of sale and quality clothing - align with Nordstrom's identity. Trunk Club is a new channel for delivering the Nordstrom brick and mortar experience.

Suppose a startup only has budget for a website or an app. The team decides to use a mobile web solution to get both. The product goes to market and succeeds. Then the company learns that users would like a different experience on mobile, and so development begins on native apps. At this juncture, the developers have a lot to consider:
* Will the data consumed be consistent on both platforms?
* What if mobile users don't update their app?
* How will two different applications keep the same look when the company's iconography changes?

If the development team uses RESTful services, the native mobile project can readily consume the same data as the web project. Unit tests on the services are valid for all platforms. The cost of maintenance is kept low without compromising on flexibility in native app design. Services should be versioned, so out of date software can still conform to the old APIs, thus removing the nasty user experience of a forced app upgrade.

## 2. Centralize Business Logic
> More code equals more bugs.

A few years ago I was working on a financial, iOS app and was building a feature to transfer funds. There were dozens of conditions that could affect which dates were valid for transferring money:
* Time zone
* Were both accounts internal or both external?
* Was a bank holiday involved?
* Were sufficient funds going to be available on the scheduled date?
* Was the transfer recurring?
…

These conditions created a lot of room for error, and the logic had to be consistent across all platforms! With multiple platforms to support, the margin of error increases significantly. This type of business logic should be sent to apps from a central server, then integration and unit testing can happen in one place. This approach keeps the total cost of ownership low, which includes expansion to new platforms.

If business logic must live on the client, consider developing it in a shareable framework that can target multiple platforms.

## 3. Identify What Content Changes in Production
Users will engage with your brand through multiple channels, and it's important to be both flexible and consistent with how the brand is portrayed. These two ideas, flexibility and consistency, can war against each other in a poorly architected system.

Let's say market research shows that your brand needs a new logo. If your native app has the logo embedded in it, an app update that corresponds with the rebrand launch must be coordinated. New platforms means more coordination. As your brand hits more mediums, the friction of this rebranding expands.

Now suppose the team uses "back end as a service" platforms such as Parse to send their imagery to both web and native platforms. A product manager or designer can update a logo on multiple platforms without programmer intervention. Brandfolder is another great tool for centralizing your brand's content. Companies must take care to structure their content so that they can scale and adapt the brand across all digital channels.

## 4. Play to a Platform's Strengths
Users on different platforms have different expectations. Web menus typically live in a horizontal bar, while iOS users expect a tab bar and Android users are accustomed to hamburger menus. The multitouch interface of mobile empowers greater user interaction than web, but screen real estate is more precious. Smart watches require a minimalistic approach and brief experiences. While a brand should be consistent and persistent across all of these mediums, they each empower users in unique ways. Identify the use cases that can be unique opportunities for each channel.

## 5. Aggregate the Data
Don't silo your user data by channel. Dashboards need to be able to filter information across any combination of platforms. If the product team members prefer different tools for viewing data, consider using Segment to aggregate the results. To really understand how your users interact with your brand, you need to be able to track their experience across channels. A better user interface for viewing this data will lead to greater insight.

In the new digital era, one thing is for sure - change is constant. New business channels will open up. New technologies will emerge. By acknowledging these realities when designing software, you can swiftly capitalize on new opportunities as opposed to getting caught in an endless game of catch up.
