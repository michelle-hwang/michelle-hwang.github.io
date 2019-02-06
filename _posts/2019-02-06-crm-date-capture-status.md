---
title: D365 - Capture Timestamp of Status Change
tags:
  - crm
  - resource
---


## Capture on Enter of Status

Often customers will want to record the timestamp at which a certain status changes for a record. For example, one might want to know at what time a Case was set to "In Progress". 

Why use a Workflow?
- A calculated field will clear when the status changes
- A "Set Value" business rule will overwrite the field on every form load if the status is the same
- A "Set Default" business rule will only capture the first time the status changes to a specific status. It will not account if the same status occurs again.

### Step 1: Create date/time field.

TBD

### Step 2: Create a background workflow. 

TBD



## Capture on Leave of Status

I previously described how to write a Workflow to capture the timestamp at which a status changes for a record. In this post, I will describe how to write a Workflow to capture the timestamp when a certain status is changed. For example, suppose we want to capture the timestamp when a Case is no longer in an "Escalated" status, regardless of status it was changed to. 

### Create date/time field.

TBD

###  Create a background workflow.

TBD
