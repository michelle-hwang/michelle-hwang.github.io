---
title: D365: Capture Timestamp of Status Change
tags:
  - resource
  - crm
header:
  overlay_image: 
  overlay_filter: 0.2
  teaser: 
---


Often customers will want to record the timestamp at which a certain status changes for a record. For example, one might want to know at what time a Case was set to "In Progress". 

Why use a Workflow?
- A calculated field will clear when the status changes
- A "Set Value" business rule will overwrite the field on every form load if the status is the same
- A "Set Default" business rule will only capture the first time the status changes to a specific status. It will not account if the same status occurs again.

1. Create date/time field.

2. Create a XXX workflow. 
