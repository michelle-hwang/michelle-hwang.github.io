---
title: D365 - Configuring Filtered Fields for Hierarchial Data
categories:
  - crm
tags:
  - resource
  - crm
header:
  overlay_image: 
  overlay_filter: 0.2
  teaser: 
---

Suppose we have a table of hierarchial data called Service Group. There are three levels of Service Group: SG1, SG2, and SG3. When a User selects Service Group 1, the options for Service Group 2 must be filtered based on the User selection. The same logic applies to Service Group 3.

We can configure this scenario using a single Custom Entity and self-referential relationships. 

<DIAGRAM>


### Step 1: Create Custom Entity.

I will create a custom entity called Service Group.

<SREENSHOT>

### Step 2: Create self-referential relationship.

We will need to create a self-referential relationship for Service Group. To do so, create an N:1 relationship.

<SCREENSHOT>

### Step 3: Create relationship with desired entity

Now, we need to create a relationship for each field on the entity we desire to place the fields.

<SCREENSHOT>

### Step 4: Create views

#### Create view for Parent

#### Create view for Child

<SCREENSHOT>

### Step 5: Add to form using filtered view

Filtered view on lookups

Tip: Remove the "Created On" date field that shows up on the Lookup View.


<SCREENSHOT>

### Step 6: Import data

Finally, we will need to import the values needed to populate the 

<SCREENSHOT>

