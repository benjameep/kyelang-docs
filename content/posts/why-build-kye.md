---
title: "Why am I building Kye?"
date: 2023-07-29T16:04:14-06:00
# bookComments: false
# bookSearchExclude: false
---

Hello! My name is Benjamin Earl and I am off on an adventure to improve how data pipelines are built. I come from a software engineering background where I got my start in data engineering through web scraping.

The thing about web scraping is that you have absolutely no control over your data sources (and often your data sources are deliberately trying to stop you). I believe web scraping is not alone in this lack of control over data sources. Ownership over a data source really comes down to who has permission to makes changes to the data. Data teams rarely have that luxury. If a data team wants a new field or event to be logged on an internal data source, maybe you'll be able to ask the software engineers very nicely. If it's an external data source then good luck.

### A lack of data ownership leads to two main problems:
1. **Lack of Documentation** You're not the one who created the data so you don't have all the context around what it means, how it is used, etc. You can nicely ask the person who created the data to document the context somewhere, but once again you're at the whim of the data owner, and it's not a problem you can solve on your own.
2. **Constantly on the Defense** Without ownership over your data sources you often wont get a warning before changes are made upstream. So data teams are often scrambling to put out fires, because they won't know anything has gone wrong until either their data pipelines are screaming errors. Or worse, silent failures wont get noticed until months later when their consumer tells them a dashboard "looks wrong".

These problems are intrinsically tied to not having ownership over data sources, so they aren't going away overnight. But I believe that there are some things we can do to lessen the blow.

First off, we may not have the full context as to what the data means or how it is being used within it's source. But we can document what we *assume* it means and how *we* are using it. And if that documentation is written in such a way that those assumptions can be automatically verified, then it will help with the second problem of knowing exactly when and where something went wrong.

So that is my goal for Kye, to be a system where you can define and validate your assumptions of not only your upstream data sources but also ensure you're not creating unexpected changes for *your* down stream consumers.

I've got a lot more to say about the benefits of such a system, my implementation plan, and how it compares to existing solutions, so keep in touch and hopefully i'll have it ready soon!