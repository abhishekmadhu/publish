---
created: 2024-08-04T23:59:24 (UTC +05:30)
keywords: 
source: https://help.salesforce.com/s/articleView?id=sf.bre_example_expression_with_context_definition.htm&type=5
author: 
share: "true"
---

# How to Create an Expression Set That Uses Context Definition

> ## Excerpt
> This example shows how to associate a context definition with an expression set, and how to use the definition’s tags as list variables in the expression...

---
You are here:

1.  [Salesforce Help](https://help.salesforce.com/s/?language=en_US)
2.  [Docs](https://help.salesforce.com/s/products?language=en_US)
3.  [Industries Common Features Guide](https://help.salesforce.com/s/articleView?id=sf.industries_common_features.htm&language=en_US&type=5)

This example shows how to associate a context definition with an expression set, and how to use the definition’s tags as list variables in the expression set version. The example also shows how to verify if the expression set version works as expected.

To encourage writers to publish their blog posts on their platform, a new blogging platform is offering an introductory, short-term income opportunity. Blog writers are entitled to an income based on the number of views, comments, and likes for their blog posts. Each blog post published on the platform is entitled to a flat income of $10. In addition, the writers are entitled to $0.20 per like and comment, and $0.10 per view.

The platform’s marketing team asks their rule designer and Salesforce admin to create an automated rule that instantly shows the writers their earnings in real time.

The rule designer and the platform’s Salesforce admin divide the requirement into these tasks.

1.  **[Create a Context Definition to Define the Blog Data Structure](https://help.salesforce.com/s/articleView?id=sf.bre_example_expression_with_context_definition.htm&language=en_US&type=5#bre_example_create_context_definition)**  
    The definition has the complete set of information that’s required to build the expression set to calculate the income based on the views, likes, and comments on each blog post.
2.  **[Map the Definition to Data Sources and Activate the Definition](https://help.salesforce.com/s/articleView?id=sf.bre_example_expression_with_context_definition.htm&language=en_US&type=5#bre_example_map_context_and_activate_definition)**  
    After you create the context definition, map the definition’s nodes and attributes to sObjects and their fields. The mapping feeds data into the definition.
3.  **[Create an Expression Set to Calculate Blogging Income](https://help.salesforce.com/s/articleView?id=sf.bre_example_expression_with_context_definition.htm&language=en_US&type=5#bre_example_create_expression_set_to_calculate_income_from_blogging)**  
    In this example, the expression set is associated with the BlogDetails context definition. When you open the expression set version, you can use the context definition’s tags as list variables in the version’s steps.

## Create a Context Definition to Define the Blog Data Structure

The definition has the complete set of information that’s required to build the expression set to calculate the income based on the views, likes, and comments on each blog post.

1.  From Setup, in the Quick Find box, enter Context Definitions, and then select **Context Definitions**.
2.  Click **New**.
3.  For Name, enter BlogDetails.
4.  Enter the effective start and end dates for the definition.
    
    To use a context definition in an expression set, enter a start date that’s before the expression set’s start date, and enter an end date that’s after the expression set’s end date.
    
5.  Click **Next**.
6.  To define the relationship between the definition’s nodes, create the definition’s structure.
    
    1.  Add a top-level node named Blog\_Data.
        
        This node represents all attributes related to blogging data, including the child nodes and their attributes.
        
    2.  Add a child node named Engagement\_Stats.
    
    ![Top-level node and child nodes in new context definition.](https://resources.help.salesforce.com/images/e1837737dab112ee19f6d52d2c55525d.png)
    
7.  Click **Next**.
8.  Add attributes to each node, select whether the attribute is used as input, output, or both, and select the data type for each attribute.
    
    Here are the attributes in the Blog\_Data and Engagement\_Stats nodes respectively.
    
    ![Attributes in Blog_Data node](https://resources.help.salesforce.com/images/4d494a043265a51c4cf80312e8381ccd.png)
    
    ![Attributes in the Engagement_Stats node.](https://resources.help.salesforce.com/images/2318dcaca92c2cdfecaea55a50b90576.png)
    
9.  Click **Next**, and add tags for each node and the node’s attributes.
    
    Tags appear as list variables in versions of the expression sets that are associated with context definitions.
    
    Here are the tags for the nodes and their attributes.
    
    ![Node and attribute tags](https://resources.help.salesforce.com/images/63ff7f1f4a36ca982b7a2122802b851f.png)
    
    ![Node and attribute tags for Engagement_Stats](https://resources.help.salesforce.com/images/bbb184cb6a84d2511c36934c4c731abc.png)
    
10.  Save the definition.

## Map the Definition to Data Sources and Activate the Definition

After you create the context definition, map the definition’s nodes and attributes to sObjects and their fields. The mapping feeds data into the definition.

In this example, we’re mapping the BlogDetails context definition’s nodes and attributes to the Blog and Blog Engagement custom objects, which we’ve already created. These objects have fields that are similar to the attributes in the context definition’s nodes.

1.  From Setup, in the Quick Find box, enter Context Definitions, and then select **Context Definitions**.
2.  To open the BlogDetails definition to map the data, select the BlogDetails from the definitions list.
3.  Select **Map Data**.
4.  Click **Add Mapping**.
    
    The mapping page opens on a new tab.
    
5.  Provide mapping details.
    1.  For name, enter Blog\_Readership.
    2.  Enter a description.
    3.  For Mapping Type, select **Automatic sObject mapping**.
    4.  Select **Mark as Default**.
    5.  Click **Map**.
6.  Map the context definition’s nodes and attributes to sObjects and their fields.
    1.  Click **Select Objects**.
    2.  Search for the objects.
        
        In this example, we selected Blog\_\_c and Blog\_Engagement\_\_c.
        
    3.  Click **Done**.
    4.  To map the nodes to sObjects, select a node and then select the object. This mapping forms a connection between the node and the object.
    5.  To map attributes to sObject fields, select an attribute and then select the field.
        
        This mapping forms a connection between the attribute and the field.
        
    6.  Save the mapping.
7.  Return to the context definitions list.
8.  To activate the BlogDetails context definition, click ![Show actions icon](https://resources.help.salesforce.com/images/fbeda177222067a73601ced711930fd9.png) for the definition, and select **Activate**.

Your context definition is now ready to be used in the expression set.

## Create an Expression Set to Calculate Blogging Income

In this example, the expression set is associated with the BlogDetails context definition. When you open the expression set version, you can use the context definition’s tags as list variables in the version’s steps.

1.  From the App Launcher (![App explorer icon.](https://resources.help.salesforce.com/images/c60e993695db0338377e6e28588c96af.png)), find and select **Business Rules Engine**.
2.  Click the app navigation menu, and then select **Expression Sets**.
3.  Click **New**.
4.  Create the expression set.
    1.  For name, enter Calculate\_Blogging\_Income.
    2.  Select **Default** as the usage type.
    3.  For context definition, select **BlogDetails**.
    4.  Save the expression set.
5.  From the Expression Set Versions area, select **Calculate\_Blogging\_Income V1**.
    
    The version opens in Expression Set Builder.
    
6.  To see the resources available for use in the version, click ![Resource manager icon](https://resources.help.salesforce.com/images/994e71d0bf44c9ce0163fd943044b0c8.png).
    
    You can use these context definition’s tags as list variables in the steps.
    
    ![Resource manager shows context tags](https://resources.help.salesforce.com/images/b8be063233c4319e8285105437543226.png)
    
7.  Create the additional resources to be used in the version.
    1.  Click **Add Resource**.
    2.  For the first resource, specify these details, and click **Done and New**.
        
        Resource Type: Constant, Resource Name: Blog\_Flat\_Rate, Data Type: Currency, Default Value: 10.
        
    3.  For the second resource, specify these details, and click **Done**.
        
        Resource Type: Variable, Resource Name: Blog\_Income, Data Type: Currency
        
8.  On the builder canvas, add a step to calculate the number of likes per blog post by the platform’s subscribers.
    
    1.  Click ![Add step icon](https://resources.help.salesforce.com/images/686dcd50c3db18bbf6988016fd9fe4eb.png), and select **Calculation**.
    2.  In the Formula field, search for and select **LISTSUM**.
    3.  Replace ListVariable inside the parenthesis with **Like\_Count**.
        
        Like\_Count is an attribute tag from the Blog\_Data context definition. The tag is used as a list variable in the calculation and is part of the Engagement\_Stats node in the BlogDetails context definition.
        
    4.  For Output Variable, select **Likes**.
        
        Likes is an attribute tag under the Blog\_Data node in the BlogDetails context definition.
        
    
    ![Tag hierarchy](https://resources.help.salesforce.com/images/c01a935c5988b1d215caec1a19b782f6.png)
    
    Here, Like\_Count is lower in the context definition’s node hierarchy than Likes. When the LISTSUM function sums the number of likes across subscribers per blog post, the sum is stored in the Likes variable, which is above Like\_Count in the node hierarchy.
    
9.  Calculate the number of comments per blog post by the platform’s subscribers.
    1.  Click ![Add step icon](https://resources.help.salesforce.com/images/686dcd50c3db18bbf6988016fd9fe4eb.png), and select **Calculation**.
    2.  In the Formula field, search for and select **LISTSUM**.
    3.  Replace ListVariable inside the parenthesis with Comment\_Count.
        
        Comment\_Count is an attribute tag from the Blog\_Data node. The tag is used as a list variable in the calculation and is part of the Engagement\_Stats node in the BlogDetails context definition.
        
    4.  For Output Variable, select **Comments**.
        
        Comments is an attribute tag under the Blog\_Data node in the BlogDetails context definition.
        
10.  Add the condition logic to filter blogs based on their total views, likes, and comments.
    1.  Click ![Add step icon](https://resources.help.salesforce.com/images/686dcd50c3db18bbf6988016fd9fe4eb.png), and select **List Group**.
    2.  In the list filter, for Resource, select **Views**, for Operator, select **Greater than or Equal**, and for Value, enter 100.
        
        This expression represents the condition, Views are greater than or equal to 100.
        
    3.  To add a condition, click **Add Condition**.
    4.  For Resource, select **Likes**, for Operator, select **Greater than or Equal**, and for Value, enter 10.
        
        This expression represents the condition, Likes are greater than or equal to 10.
        
    5.  To add another condition, click **Add Condition**.
    6.  For Resource, select **Comments**, for Operator, select **Greater than or Equal**, and for Value, enter 5.
        
        This expression represents the condition, Comments are greater than or equal to 5.
        
    7.  In the list filter, for Filter Condition Requirements, select **Custom Condition is Met**.
    8.  For Custom Condition Logic, enter 1 AND (2 OR 3).
        
        The custom logic indicates that the list filter’s conditions evaluate to true when the first condition and either the second or the third condition are met.
        
        ![List filter's custom logic](https://resources.help.salesforce.com/images/2ac3d60e733c2f0f5d65f2cff18545f1.png)
        
11.  Calculate the blogging income for the filtered list items.
    1.  In the list group, after the list filter, click ![Add step icon](https://resources.help.salesforce.com/images/686dcd50c3db18bbf6988016fd9fe4eb.png).
    2.  Select **Calculation**.
    3.  In the Formula field, enter Blog\_Flat\_Rate + ( 0.10 \* Views ) + 0.20 \* ( Likes + Comments ).
        
        The formula represents how the blogging income is calculated. Each blog post earns the writer a flat blog rate of $10, which is stored in the Blog\_Flat\_Rate resource. The writer is entitled to $0.10 per view on the blog post. The income from the view is calculated by multiplying the number of views with 0.10. The writer is entitled to an additional income of $0.20 per like and comment on the blog post. The income from the likes and comments is calculated by adding the number of comments and likes per post, and multiplying the number by 0.20. The income from the likes, views, and comments is then added to the blog flat rate.
        
    4.  In the Output Variable field, select **Blog\_Income**.
        
        The Blog\_Income variable stores the output of the calculation formula for the total blog income.
        
12.  To see a version step’s output when the expression set version runs, select the step element, click ![Element details icon](https://resources.help.salesforce.com/images/8dea61540f21d9028bd48bedf957f67b.png), and select **Include in output**.
13.  Save the version.
14.  To verify that the steps work as expected, simulate the version.
    1.  Click **Simulate**.
    2.  For Input Mode, select **Advanced**.
        
        When you use list variables in an expression set, always use the Advanced input mode to pass sample values for simulation.
        
    3.  Modify the JSON input template with these sample values.
        
        ![JSON input example](https://resources.help.salesforce.com/images/769950e77cbd627405f51a36cac93ea0.png)
        
    4.  Click **Simulate**.
        
        The list filter returns one matching result based on the filter criteria.
        
        ![Simulation result from the list filter](https://resources.help.salesforce.com/images/b1a52cf80b58d47b16f53f91072ac1b4.png)
        
        The calculation step in the list group returns the blogging income for the blog post that meets the filter conditions.
        
        ![Simulation results from the calculation step in the list group](https://resources.help.salesforce.com/images/0d3b226f742dc046df68d2de5dfac2d2.png)
---

This link is a resource that is not owned by me. I have saved this as a resource for my personal use. This document may have been modified by my or multiple tools, and none of those changes denote a correction or violation of copyright. This is fair usage of document, with attribution provided at the top of the page.