---
title: (Draft) D365 - Automatically Close Record Based on Wait Time
tags:
  - resource
  - crm
header:
  overlay_image: https://docs.microsoft.com/en-us/dynamics365/images/dynamics-whats-new.svg
  overlay_filter: 0.2
  teaser: https://docs.microsoft.com/en-us/dynamics365/images/dynamics-whats-new.svg
---

*e.g. close a Case if it has been in "Resolved" for 15 days

<img src="https://www.dqglobal.com/wp-content/uploads/2017/10/microsoft-dynamics-crm-365-icon.png" width="70">


A common ask is to automatically close a record, e.g. Case, after a certain amount of time (+ other conditions). For example, suppose we want to automatically close a Case after 15 days of a Case in the "Resolved" status. 


### Step 1: Create Wait Field

We will first need to create the field that will hold the maximum time at which the Case can remain open. 

### Step 2: Create Child Workflow

Next we want to create a Child Workflow to set the Case status to "Closed given that the Process Execution Time of the workflow is past the Wait Time. 

### Step 3: Create Workflow

Finally, we will need to create an additional Workflow that will handle the conditions that sets the Wait Time and triggers the "wait".
