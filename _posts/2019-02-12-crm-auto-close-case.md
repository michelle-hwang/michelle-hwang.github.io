---
title: D365 - Automatically Close Record Based on Wait Time
tags:
  - resource
  - crm
header:
  overlay_image: https://docs.microsoft.com/en-us/dynamics365/images/dynamics-whats-new.svg
  overlay_filter: 0.2
  teaser: https://docs.microsoft.com/en-us/dynamics365/images/dynamics-whats-new.svg
---

*e.g. close a Case if it has been in "Resolved" for 15 days*

<img src="https://www.dqglobal.com/wp-content/uploads/2017/10/microsoft-dynamics-crm-365-icon.png" width="70">


A common ask is to automatically close a record, e.g. Case, after a certain amount of time (+ other conditions). For example, suppose we want to automatically close a Case after 15 days of a Case in the "Resolved" status. 

## Closing a Case Based on Set Wait Value

### Step 1: Create Wait Threshold Field

We will first need to create the field that will hold the maximum time at which the Case can remain open. 

> ![posts-crm-autoclose-case-1.png](/images/posts-crm-autoclose-case-1.png)


### Step 2: Create Child Workflow

Next we want to create a **Child Workflow** to set the Case status to "Closed" given that the Process Execution Time of the workflow is past the Wait Threshold. 

> ![posts-crm-autoclose-case-2.png](/images/posts-crm-autoclose-case-2.png)

> ![posts-crm-autoclose-case-3.png](/images/posts-crm-autoclose-case-3.png)


### Step 3: Create Workflow

Finally, we will need to create an additional Workflow that will handle the conditions that sets the Wait Time and triggers the "wait". We want this Workflow to trigger on the change of **Case Status**. It will then check for the *Resolved* status before beginning the wait timer. In this example, I have set the wait at 10 days. 

Once the timer is up, we call the child workflow to perform the evaluation to check whether the Case can be closed.

> ![posts-crm-autoclose-case-4.png](/images/posts-crm-autoclose-case-4.png)

**Why two workflows?** This is to handle the scenario in which the Case Status is changed from *Resolved* and back to an *In Progress* status. We would not want the original Workflow to prematurely close the Case. 

