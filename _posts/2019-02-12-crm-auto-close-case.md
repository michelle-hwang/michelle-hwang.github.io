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

1. Simple Field on Case for Wait
2. Simple Field on Case for Counter
3. Workflow

We are essentially going to mimic/configure the following pseudocode:

```
function Workflow(Case Close Counter = 0, Case Close Wait) {
    if(Case Status = "XXX")
        Wait(1 day)
        if(Case Close Counter >= Case Close Wait)
            Case Status = "Closed'
            STOP
        Workflow()
    else
        Case Close Counter = 0
}
```

### Step 1: Create Simple Field for Wait Time

The first field will be used to hold the Wait Time, or the maximum threshold in which a Case can remain open before automatically becoming "Closed". 


### Step 2: Create  Field for Wait Counter

Now we want a field to store our "counter", or how many days has elasped since the Case Status became "Resolved". 


### Step 3: Create Main Workflow

This workflow that will handle this logic will use a bit of recursion to repeat itself until we reach a Case Status of "Closed". This is because we want this Workflow to fire on a daily basis. On each fire, we will have a condition to check whether the days elasped has psased the threshold. If so, the Case will close and the workflow will stop. If not, we will increment the counter and call the workflow again. 



