---
share: "true"
---

# Visualforce Basics

Creation Timestamp: May 13, 2021 8:33 PM
Date Finished: December 16, 2020
Details: Use Visualforce to build custom user interfaces for mobile and web apps.
Estimated Hours: 3
Has Exam Weight?: No
Points: 4100
Salesforce Docs URL: https://developer.salesforce.com/docs/atlas.en-us.224.0.pages.meta/pages/pages_intro.htm
Status: Done
Tags: Module
Timeline: December 16, 2020

# **[Get Started with Visualforce](https://trailhead.salesforce.com/content/learn/modules/visualforce_fundamentals/visualforce_intro?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)**

A web development framework

- An example of a Visualforce page

    ```jsx
    <apex:page standardController="Contact" >
        <apex:form >
            <apex:pageBlock title="Edit Contact">
                <apex:pageBlockSection columns="1">
                    <apex:inputField value="{!Contact.FirstName}"/>
                    <apex:inputField value="{!Contact.LastName}"/>
                    <apex:inputField value="{!Contact.Email}"/>
                    <apex:inputField value="{!Contact.Birthdate}"/>
                </apex:pageBlockSection>
                <apex:pageBlockButtons >
                    <apex:commandButton action="{!save}" value="Save"/>
                </apex:pageBlockButtons>
            </apex:pageBlock>
        </apex:form>
    </apex:page>
    ```

    [[../../../../../../e646fb225441602ba0db4e602bf4477c_visualforce-intro-sample-page.jpeg|e646fb225441602ba0db4e602bf4477c_visualforce-intro-sample-page.jpeg]]


# **[Create & Edit Visualforce Pages](https://trailhead.salesforce.com/content/learn/modules/visualforce_fundamentals/visualforce_creating_pages?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)**

The sidebar and showHeader attribute have no effect in Lightning Experience, and that there’s no way to suppress the Lightning Experience header.

# **[Use Simple Variables and Formulas](https://trailhead.salesforce.com/content/learn/modules/visualforce_fundamentals/visualforce_variables_expressions?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)**

# **[Use Standard Controllers](https://trailhead.salesforce.com/content/learn/modules/visualforce_fundamentals/visualforce_standard_controllers?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)**

# **[Display Records, Fields, and Tables](https://trailhead.salesforce.com/content/learn/modules/visualforce_fundamentals/visualforce_output_components?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)**

# **[Input Data Using Forms](https://trailhead.salesforce.com/content/learn/modules/visualforce_fundamentals/visualforce_forms?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)**

# **[Use Standard List Controllers](https://trailhead.salesforce.com/content/learn/modules/visualforce_fundamentals/visualforce_standard_list_controllers?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)**

Visualforce uses model–view–controller (MVC)

# **[Use Static Resources](https://trailhead.salesforce.com/content/learn/modules/visualforce_fundamentals/visualforce_static_resources?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)**

# **[Create & Use Custom Controllers](https://trailhead.salesforce.com/content/learn/modules/visualforce_fundamentals/visualforce_custom_controllers?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential)**

[https://developer.salesforce.com/docs/atlas.en-us.224.0.pages.meta/pages/pages_controller_def.htm](https://developer.salesforce.com/docs/atlas.en-us.224.0.pages.meta/pages/pages_controller_def.htm)

- Custom controller cannot accept parameters in constructors

```jsx
// Controller
public class MyController {

    private final Account account;

    public MyController() {
        account = [SELECT Id, Name, Site FROM Account
                   WHERE Id = :ApexPages.currentPage().getParameters().get('id')];
    }

    public Account getAccount() {
        return account;
    }

    public PageReference save() {
        update account;
        return null;
    }
}

// How to use in VF Page
<apex:page controller="myController" tabStyle="Account">
    <apex:form>
        <apex:pageBlock title="Congratulations {!$User.FirstName}">
            You belong to Account Name: <apex:inputField value="{!account.name}"/>
            <apex:commandButton action="{!save}" value="save"/>
        </apex:pageBlock>
    </apex:form>
</apex:page>
```

# Controller Extensions

A controller extension is any Apex class containing a constructor that takes a single argument of type `ApexPages.StandardController` or `CustomControllerName`, where `CustomControllerName` is the name of a custom controller you want to extend.

Use controller extensions when:

- You want to leverage the built-in functionality of a standard controller but override one or more actions, such as edit, view, save, or delete.
- You want to add new actions.
- You want to build a Visualforce page that respects user permissions. Although a controller extension class executes in system mode, if a controller extension extends a standard controller, the logic from the standard controller does not execute in system mode. Instead, it executes in user mode, in which permissions, field-level security, and sharing rules of the current user apply.
- Code examples

    ```jsx
    // Controller Extension
    public class myControllerExtension {

        private final Account acct;

        // The extension constructor initializes the private member
        // variable acct by using the getRecord method from the standard
        // controller.
        public myControllerExtension(ApexPages.StandardController stdController) {
            this.acct = (Account)stdController.getRecord();
        }

        public String getGreeting() {
            return 'Hello ' + acct.name + ' (' + acct.id + ')';
        }
    }

    // usage in VF
    <apex:page standardController="Account" extensions="myControllerExtension">
        {!greeting} <p/>
        <apex:form>
            <apex:inputField value="{!account.name}"/> <p/>
            <apex:commandButton value="Save" action="{!save}"/>
        </apex:form>
    </apex:page>
    ```

    - For multiple extensions, use comma separated values for the `extensions` attribute:
    `extensions="ExtOne,ExtTwo"`  ←   **Leftmost one gets preference**
    -

# [StandardSetController Class](https://developer.salesforce.com/docs/atlas.en-us.pages.meta/pages/apex_pages_standardsetcontroller.htm)

A way to extend StandardListControllers

Useful for:

- Mass updates to an object of a type
- Pagination (inbuilt feature)
