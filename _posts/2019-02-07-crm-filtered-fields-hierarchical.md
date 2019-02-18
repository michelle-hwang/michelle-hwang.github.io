---
title: (Draft) D365 - Configuring Filtered Fields for Hierarchial Data
categories:
  - crm
tags:
  - resource
  - crm
header:
  overlay_image: https://docs.microsoft.com/en-us/dynamics365/images/dynamics-whats-new.svg
  overlay_filter: 0.2
  teaser: https://docs.microsoft.com/en-us/dynamics365/images/dynamics-whats-new.svg
---

*Using a single entity for hierarchical filtering*

<img src="https://www.dqglobal.com/wp-content/uploads/2017/10/microsoft-dynamics-crm-365-icon.png" width="70">

Suppose we have a table of hierarchial data called Service Group. There are three levels of Service Group: SG1, SG2, and SG3. When a User selects Service Group 1, the options for Service Group 2 must be filtered based on the User selection. The same logic applies to Service Group 3.

We can configure this scenario using a single Custom Entity and self-referential relationships. 


### Step 1: Create Custom Entity.

I will create a custom entity called Service Group.

![posts-crm-hierarchical-fields-1](/images/posts-crm-hierarchical-fields-1.png)


### Step 2: Create self-referential relationship.

We will need to create a self-referential relationship for Service Group. To do so, create an N:1 referential relationship. The ID for this field will be the "Parent" Service Group. 

![posts-crm-hierarchical-fields-2](/images/posts-crm-hierarchical-fields-2.png)


### Step 3: Create relationship with desired entity

Now, we need to create a relationship for each field on the entity (I will use Case) we desire to place the fields. Suppose I want to place these Service Group fields on the Contact. I will need to make 3 1:N relationships for the 3 Look-up fields.

![posts-crm-hierarchical-fields-3](/images/posts-crm-hierarchical-fields-3.png)

The following settings will be used to Service Group 1, Service Group 2, and Service Group 3:

![posts-crm-hierarchical-fields-3](/images/posts-crm-hierarchical-fields-3b.png)
 

### Step 4: Create views

#### Create view for Parent

Now we need to configure the Lookup Views. For the first field, Service Group 1, we want to create a filtered view so we don't see the entire list of Service Groups. We only want to see options for Service Group 1.

![posts-crm-hierarchical-fields-4c](/images/posts-crm-hierarchical-fields-4c.png)

![posts-crm-hierarchical-fields-4d](/images/posts-crm-hierarchical-fields-4d.png)

#### Create view for Child

For Service Group 2 and 3, we don't need to use a filtered view, as these will be filtered using filtered lookups.

*Tip: Remove the "Created On" date field that shows up on the Lookup View to free up space in the Lookup.*

![posts-crm-hierarchical-fields-4](/images/posts-crm-hierarchical-fields-4.png)

![posts-crm-hierarchical-fields-4b](/images/posts-crm-hierarchical-fields-4b.png)



### Step 5: Add to form 

Since the data will be hierarchically filtered, we will use filtered lookups on Service Group 2 and Service Group 3 to handle this.

![posts-crm-hierarchical-fields-3](/images/posts-crm-hierarchical-fields-3c.png)

![posts-crm-hierarchical-fields-5](/images/posts-crm-hierarchical-fields-5.png)

For the Service Group 1, we also have to set the view to the one we created without a parent:

![posts-crm-hierarchical-fields-5b](/images/posts-crm-hierarchical-fields-5b.png)


### Step 6: Import data

Finally, we will need to import the values needed to populate the 



