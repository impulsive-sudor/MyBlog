---
title: My Real Estate Software Problem
date: 2024-02-04T19:24:38.725Z
draft: false
featured_image: /images/57888_Picture of a computer with a house on the screen. _xl-1024-v1-0.png
type: Blog
slug: real-estate-software-problem
tags:
    - Business
    - Development
    - Python
    - Real Estate
    - Blog
---

## The Problem

One of the problems I've been dealing with lately is keeping track off all my real estate expenses. I don't have many properties but it's still a pain to keep organized. Looking around for open source solutions, I couldn't really find one. The software [Akaunting](https://akaunting.com) seems okay but doesn't do everything I need for real estate. There's also a few commercially available solutions like Avail, Quickbooks, Landlordstudios and Zillow but none of these are free. Each of these softwares also have their positive and negatives. Ultimately none of those paid solutions give me the full ownership of my data, which is something I value.

## What about Excel?

Excel is a very powerful software and can be used for many things. I could use this to help track expenses but it's not as scalable. I'm also not a fan of giving this important information over to Microsoft. However, Excel is going to be my fallback if I can't find another method that works.

## The Requirements

* Easy to use
* Easy to reference for taxes
* Cost effective
* Scalable
* Has all the categories required to be a one stop shop for real estate tracking
* Can attach receipts
* Miles tracking
* Be able to create budgets to track upcoming expenses (like window upgrades or a new roof)
* Private and Secure
* Contacts list for everything related to the business
* Multi-user environments to allow employees access (In my case, my family)
* A project task page to track upcoming tasks. Would be great to create something recurring (Spring cleaning, pest control, etc)

## Nice to haves

* Integration with your bank to track expenses and income
* A Tenant view to submit requests
* A Tenant portal where there's documentation to reference
* Tenants can submit payments through the portal
* Geolocation Miles tracking through an app
* Automated lease generation (Like what Avail has)
* Tenant screening
* List directly to websites like Zillow through the site
* MFA
* Export option for taxes
* Import options for moving from other platforms
* Email notifications
* Direct messaging within the platform

## The Solution

I'm going to attempt to build my own software that meets all these requirements. I don't have much experience building this kind of software, so it will be a great learning experience. My family does have a good amount of experiencing managing a small amount of real estate properties, so I feel like I have a good background. If there are any good platforms out there though, I'm still open to adopting another tool.

As of writing this article, I've made the code public to what I've worked on so far [here](https://github.com/impulsive-sudor/Miso). Currently focusing on the data model to ensure all the different possibilities are met. There's a long ways to go but I'm hoping this could be something that I can use long term.

The end goal with this software I'm creating is to better my knowledge on development and possible make a hosted version of this software to sell. I like the business model where the software is open source and there's a SaaS offering to make it easy for normal people to use.