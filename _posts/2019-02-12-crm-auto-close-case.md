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

*e.g. close a Case if it has been in "Resolved" for 15 days*

<img src="https://www.dqglobal.com/wp-content/uploads/2017/10/microsoft-dynamics-crm-365-icon.png" width="70">


A common ask is to automatically close a record, e.g. Case, after a certain amount of time (+ other conditions). For example, suppose we want to automatically close a Case after 15 days of a Case in the "Resolved" status. 

## Closing a Case Based on Set Wait Value

### Step 1: Create Wait Threshold Field

We will first need to create the field that will hold the maximum time at which the Case can remain open. 

### Step 2: Create Child Workflow

Next we want to create a Child Workflow to set the Case status to "Closed" given that the Process Execution Time of the workflow is past the Wait Threshold. 

### Step 3: Create Workflow

Finally, we will need to create an additional Workflow that will handle the conditions that sets the Wait Time and triggers the "wait".



## Closing a Case Based on a Dynamic Wait Value

The previous scenario allowed us to set the wait time at a standard value, such as 10 days, which is configurable in the solution. With some added complexity, we can make this a dynamic value that is based on some field on another record. For example, the value might be change dependening on the type of Account/Customer. To do this we can use 4 separate items in our solution:

1. Calculated Field on Case
2. Simple Field on Case
3. Workflow
4. Child Workflow

### Step 1: Create Simple Field for Wait Time

The simple field on the Case will store the dynamic value of the Wait time. 

### Step 2: Create Calculated Field for Wait Threshold

The calculated field will store the date/time of the maximum date/time allowe for the Case to still be open. If the current date/time is greater than this calculated date/time, the system needs to close the Case.

```
If (Case Status = "Resolved")
    Case Wait Threshold = NOW() + Case Wait Time
```

### Step 3: Create Child Workflow

The reason we need to create a Child Workflow is to handle the scenario in which the Case Status returns to Open and we will need to enter the Resolved status again (more than once).

```
If (Process Execution Time > Case Close Threshold)
    Update Case Status = "Closed"
```

### Step 4: Create Main Workflow

Recall that Calculated Fields cannot be used in Workflows on a Wait/Timeout condition. Therefore, instead of having the Workflow "wait" until the maximum date for the Case to be open, we will need to fire the Workflow to check if the current date is equal to the maximum date. This workflow that will handle this logic will use a bit of recursion to repeat itself until we reach a Case Status of "Closed". This is because we want this Workflow to fire on a daily basis.

```
If (Case Status = "XXX")
    Wait(1 day)
    Run(Child Workflow)
    If Case Status = "Closed", STOP
    Run(Main Workflow)
```
