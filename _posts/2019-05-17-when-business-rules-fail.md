---
title: D365 - When Business Rules Fail You
tags:
  - resource
  - crm
header:
  overlay_image: https://docs.microsoft.com/en-us/dynamics365/images/dynamics-whats-new.svg
  overlay_filter: 0.2
  teaser: https://docs.microsoft.com/en-us/dynamics365/images/dynamics-whats-new.svg
---

*When configuration isn't always your friend*

Business Rules in Dynamics 365 are awesome. They provide a lightweight method for non-technical users to implement simple logic on forms without any code. The interface itself is very straightforward (although clunky at times), and you can have as many Business Rules on an entity as you want (in theory)! While Business Rules are easy to configure, they aren't always the best solution. There are many downfalls that come with using Business Rules.

One thing that continually trips myself and my colleagues up is the fact that Business Rules run on the form level. More specifically, Business Rules are triggered on Form Load and Field Change. So, hypothetically, if a form is never opened/loaded and only changed via backend code, Business Rules will never fire! 

Here are some more Business Rule blunders that I've ran into in my experience.


## The Case of the Manual Override 

A requirement I received from a client went a little something like this: 

1. I want Field A to be automatically determined based on Field B and Field C.
2. I want to manually overide the system-determined Field A if I need to.

At initial glance, this sounds like a pretty easy requirement. A simple business rule can be created to automatically set Field A based on Fields B and C. It still leaves Field A editable for a User to change if desired! 

But what will happen the next time that record loads?

**Field A will automatically be reset based on the business rule, which was triggered on form load.**

So, yes, you can manually override that automatically set Field A, but that change is going to revert as soon as the form refreshes.

### So what can we do instead?

1. Use workflow triggered on field change
2. Use "Set Default" condition on the business rule


## The Case of the "Required" Field

One of the configurable options for a field in Dynamics is the requirement level of a field:

> ![XXXXX.png](/images/XXXXXXX.png)

Option | Description
--- | --- 
Optional | Data not required to save record
Business Recommended | Data not required to save record, but is highly recommended
System Required | Data required to save record

Setting a field as *system required* is a great way to ensure Users populate a field on an entity. In theory, it works pretty well on to guarantee that every record for an entity contains data in that field. However, it's not foolproof. In fact, here are some ways to get around the data requirement:

### When a Required Field is Not Really Required

* Data import 
* Clear field using workflow
* Record creation from custom code
* Field is not on the form


## The Case of the Rule Overlap

Sometimes there are multiple business rules associated with a single field that can be handled by a combination of business rules and/or Javascript code. We know that Javascript will always fire *first* before Business Rules fire on form load. But what if we have multiple business rules executing logic on a single field? Unfortunately, Dynamics still doesn't have a way to configure the execution order of business rules, but there is logic you can use as a workaround:

**Business Rules are executed in order of activation.**


