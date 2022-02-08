---
title: Going Back to Work 
draft: true
weight: 141
---

# Going Back to Work 

This chapter is a summary of what we learned during the CS-GY-6613 course in Spring 2020. Implementation of an app that realized the plumbing of this project idea   

## Introduction

In the spring of 2020 the world has experienced an unprecedented in modern history event - a pandemic that killed hundreds of thousands of people and resulted in a deep global economic recession; tens of millions lost their jobs with many countries including the US reporting double digit unemployment rates. To deal with the economic blow, we need to develop systems that can protect people from infection while still allow them to go back to work. 

One of the ways that this can be achieved is by maintaining a certain density of people in buildings. To do that, we need to engineer a reservation (booking) system where each user uses an app that can reserve a period of time that she is allowed in the building, by entering the destination address and desired arrival time and length of stay. 

The _AI-powered decision system_ responds giving the actor a decision. Each decision is either an accept, manifested with a QR code with the address and allowed _arrival_ and _departure_ times in text or a downright reject. The departure time is needed since the system must preserve building density and be _fair_ to other perspective actors. People must leave the building to make "space" for others to enter. The system must be flexible - it can be integrated to automated badge control systems in office towers or simply used by security personnel or receptionist that manually [scan](https://support.apple.com/en-us/HT208843) the QR code from their own smartphone to confirm the permission to enter or compliance to exit time limits. The system also allows for group bookings, to enable face to face meetings. In this case the decision system accepts or rejects the whole group.

The system can be entirely powered by [well known chat / messaging apps](https://www.apple.com/ios/business-chat/) and a cloud-native application - the decision system. The system also complements contact-tracing systems that are powered by mobile OS and are under active development by Apple and Google or have already been deployed via [government-backed apps](https://www.technologyreview.com/2020/05/11/1001541/iceland-rakning-c19-covid-contact-tracing/).



