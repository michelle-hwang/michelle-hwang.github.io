---
title: D365 - Capture Timestamp of Status Change
tags:
  - crm
  - resource
header:
  overlay_image: https://docs.microsoft.com/en-us/dynamics365/images/dynamics-whats-new.svg
  overlay_filter: 0.2
  teaser: https://docs.microsoft.com/en-us/dynamics365/images/dynamics-whats-new.svg
---

*Using a Workflow to capture the date and time of a Status change*

<img src="https://www.dqglobal.com/wp-content/uploads/2017/10/microsoft-dynamics-crm-365-icon.png" width="70">

## Capture on Enter of Status

Often customers will want to record the timestamp at which a certain status changes for a record. For example, one might want to know at what time a Case was set to "In Progress". 

Why use a Workflow?
- A calculated field will clear when the status changes
- A "Set Value" business rule will overwrite the field on every form load if the status is the same
- A "Set Default" business rule will only capture the first time the status changes to a specific status. It will not account if the same status occurs again.


### Step 1: Create date/time field.

First we need to create the Date/Time field that we want to populate.

![posts-crm-create-date-field](/images/posts-crm-create-date-field.png)

### Step 2: Create a background workflow. 

Workflow should update on change of your Status field.

![posts-crm-status-workflow](/images/posts-crm-cast-status-workflow.png)

The workflow should start with a condition that depends on the Status desired. In this example, the Workflow will trigger if the Case Status is "Escalated":

![posts-crm-status-condition](/images/posts-crm-case-status-condition.png)

A step should follow this condition to Update Record. Use the Process Execution time of the Workflow.

![posts-crm-case-status-update-2](/images/posts-crm-case-status-update-2.png)

![posts-crm-case-status-update](/images/posts-crm-case-status-update.png)

Since this date is being determined automatically by the system, it is recommended to make the field Read-Only if it is going to be placed on the form.

![posts-crm-cast-status-ui](/images/posts-crm-cast-status-ui.png)



## Capture on Leave of Status

I previously described how to write a Workflow to capture the timestamp at which a status changes for a record. In this post, I will describe how to write a Workflow to capture the timestamp when a certain status is changed. For example, suppose we want to capture the timestamp when a Case is no longer in an "Escalated" status, regardless of status it was changed to. 

In order to handle this added complexity, I am adding an additional field to hold the last Status value. (It is helpful if your Status field is using a global option set, which can be shared with this field.)


### Step 1: Create date/time field.

First we need to create the Date/Time field that we want to populate.

![posts-crm-create-date-field](/images/posts-crm-create-date-field.png)

###  Step 2: Create a "Last Status" field.

We need to create a Status field with the same option set as the Case Status. This will store the previous Status that the Case was in. 

### Step 3: create Workflow.

Finally, we can create a background workflow to both (1) Update the Last Status field and (2) Populate the Escalation Date. Please ensure that the Workflow is triggered on the update of the Case Status field.

![posts-crm-case-status-last-workflow](/images/posts-crm-case-status-last-workflow.png)


