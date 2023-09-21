---
share: "true"
---

# Aura Components Basics

Creation Timestamp: May 14, 2021 4:16 PM
Date Finished: May 15, 2021
Details: Learning about aura components and how they are useful
Estimated Hours: 4
Has Exam Weight?: No
Status: Done
Tags: Module
Timeline: May 14, 2021

# Attributes and Expressions

`helloMessage` component being "called" with an attribute:

```jsx
<aura:component>
    <c:helloMessage message="You look nice today."/>
</aura:component>
```

`helloMessage` component with expressions that accept a `String` named `message` and then displays it:

```jsx
<aura:component>
    <aura:attribute name="message" type="String"/>
    <p>Hello! {!v.message}</p>
</aura:component>

// The expressions support operations as well.
<aura:component>
    <aura:attribute name="message" type="String"/>
    <p>{!'Hello! ' + v.message}</p>
</aura:component>
```

## Challenge solution

```jsx
<aura:component>
    <aura:attribute name='item' type='Camping_Item__c' required="true"/>
    <p>Name:
        <ui:outputText value="{!v.item.Name}"/>
    </p>
    <p>Price:
        <lightning:formattedNumber value="{! v.item.Price__c }" style="currency"/>
    </p>
    <p>Quantity:
        <lightning:formattedNumber value="{! v.item.Quantity__c }" style="number"/>
    </p>
    <p>{! 'Packed: ' + v.item.Packed}</p>

    <lightning:input type="toggle"
        label="Packed?"
        name="packed"
        checked="{!v.item.Packed__c}"
    />

</aura:component>
```

---

# Handling Actions with Controllers

## Controllers

A controller is a collection of code that defines your app’s behavior when “things happen”, in which we have logic to handle each "action" (action-handlers) which are generally "mapped" to the events/actions.

Lightning components are mostly *View-Controller-Controller-Database* architecture.

[[../../../../../../Untitled.png|Untitled]]

## Action Handlers

[[../../../../../../Untitled 1.png|Untitled 1]]

Function signature

```jsx
handleEventXyz: function(component, event, helper)
```

We called get() on btnClicked, the `<lightning:button>` that’s inside helloMessageInteractive. We’re calling set() on component—the helloMessageInteractive component itself. This is a pattern you’ll repeat in virtually every component you create

[[../../../../../../Untitled 2.png|Untitled 2]]

## Function Chaining, Rewiring, and Simple Debugging

### Chaining calls

```jsx
({
    handleClick: function(component, event, helper) {
        let btnClicked = event.getSource();         // the button
        let btnMessage = btnClicked.get("v.label"); // the button's label
        component.set("v.message", btnMessage);     // update our message
    },
		handleClick2: function(component, event, helper) {
        let newMessage = event.getSource().get("v.label");
        component.set("v.message", newMessage);
    },
    handleClick3: function(component, event, helper) {
        component.set("v.message", event.getSource().get("v.label"));
    }
})
```

## Resources

- [Working with Base Lightning Components](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/lightning_overview.htm)
- [Event Handling in Base Lightning Components](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/lightning_base_events.htm)
- [lightning:button Documentation](https://developer.salesforce.com/docs/component-library/bundle/lightning:button/documentation)
- [lightning:input Documentation](https://developer.salesforce.com/docs/component-library/bundle/lightning:input/documentation)
- [Actions and Events](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/events_and_actions.htm)
- [Handling Events with Client-Side Controllers](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/js_client_side_controller.htm)
- [Which Button Was Pressed?](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/js_cb_which_button_pressed.htm)
- [Enable Debug Mode for Lightning Components](https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/aura_debug_mode.htm)

## Solution for assessment

```jsx
<aura:component>
    <aura:attribute name='item' type='Camping_Item__c' required="true"/>
    <aura:attribute name="disabled" type="boolean" default="true"/>
    <p>Name:
        <ui:outputText value="{!v.item.Name}"/>
    </p>
    <p>Price:
        <lightning:formattedNumber value="{! v.item.Price__c }" style="currency"/>
    </p>
    <p>Quantity:
        <lightning:formattedNumber value="{! v.item.Quantity__c }" style="number"/>
    </p>
    <p>{! 'Packed: ' + v.item.Packed}</p>

    <lightning:input type="toggle"
        label="Packed?"
        name="packed"
        checked="{!v.item.Packed__c}"
    />

    <lightning:button
        label="Packed!"
        onclick="{!c.packItem}"
        disabled="{!v.disabled}"
    />

</aura:component>
```

```jsx
({
    packItem : function(component, event, helper) {
        component.set('v.item.Packed__c', true);
        component.set('v.disabled', true);
    }
})
```

# Input Data Using Forms

## Creating the forms

To make sure that the application uses SLDS (Salesforce Lightning Design System) at all possible times, extend your `harness` application as follows

```html
<aura:application extends="force:slds">
        <!-- This component is the real "app" -->
        <!-- c:expenses/ -->
</aura:application>
```

aura:id is for adding a locally unique ID on each tag it is added to. This is useful in cases where we want to access all that data as an array at once in JS.

After the form is created, Lightning Components framework will let us treat the new object in JavaScript and markup like it is a record from Salesforce, even though we did not load it from Salesforce.

- The forms area looks somewhat like this. (expand to view an example from Trailhead)

    ```jsx
    <!-- CREATE NEW EXPENSE -->
        <div aria-labelledby="newexpenseform">
            <!-- BOXED AREA -->
            <fieldset class="slds-box slds-theme_default slds-container_small">
            <legend id="newexpenseform" class="slds-text-heading_small
              slds-p-vertical_medium">
              Add Expense
            </legend>
            <!-- CREATE NEW EXPENSE FORM -->
            <form class="slds-form_stacked">
                <lightning:input aura:id="expenseform" label="Expense Name"
                                 name="expensename"
                                 value="{!v.newExpense.Name}"
                                 required="true"/>
                <lightning:input type="number" aura:id="expenseform" label="Amount"
                                 name="expenseamount"
                                 min="0.1"
                                 formatter="currency"
                                 step="0.01"
                                 value="{!v.newExpense.Amount__c}"
                                 messageWhenRangeUnderflow="Enter an amount that's at least $0.10."/>
                <lightning:input aura:id="expenseform" label="Client"
                                 name="expenseclient"
                                 value="{!v.newExpense.Client__c}"
                                 placeholder="ABC Co."/>
                <lightning:input type="date" aura:id="expenseform" label="Expense Date"
                                 name="expensedate"
                                 value="{!v.newExpense.Date__c}"/>
                <lightning:input type="checkbox" aura:id="expenseform" label="Reimbursed?"
                                 name="expreimbursed"
                                 checked="{!v.newExpense.Reimbursed__c}"/>
                <lightning:button label="Create Expense"
                                  class="slds-m-top_medium"
                                  variant="brand"
                                  onclick="{!c.clickCreate}"/>
            </form>
            <!-- / CREATE NEW EXPENSE FORM -->
          </fieldset>
          <!-- / BOXED AREA -->
        </div>
        <!-- / CREATE NEW EXPENSE -->
    ```


## Handling Form Submission in an Action Handler

- An example to handle the creation of an expense record. This corresponds to the form in [[the section above|the section above]].

    ```jsx
    ({
        clickCreate: function(component, event, helper) {
            let validExpense = component.find('expenseform').reduce(function (validSoFar, inputCmp) {
                // Displays error messages for invalid fields
                inputCmp.showHelpMessageIfInvalid();
                return validSoFar && inputCmp.get('v.validity').valid;
            }, true);
            // If we pass error checking, do some real work
            if(validExpense){
                // Create the new expense
                let newExpense = component.get("v.newExpense");
                console.log("Create expense: " + JSON.stringify(newExpense));
                helper.createExpense(component, newExpense);
            }
        }
    })
    ```


When the controller needs a way to get to a child component, first set an `aura:id` on that component in markup, and then use `component.find(theId)` to get a reference to the component at runtime. ***But do not misuse this, as components are expected to be self-contained.***

The Helper Functions can have any function signature as we control the calls and the definition (but it is recommended to pass the component as the first parameter to all helper functions)

- Example helper function that will save the expense as a list in the expense component.

    ```jsx
    ({
        createExpense: function(component, expense) {
            let theExpenses = component.get("v.expenses");
            // Copy the expense to a new object
            // THIS IS A DISGUSTING, TEMPORARY HACK
            let newExpense = JSON.parse(JSON.stringify(expense));
            theExpenses.push(newExpense);
            component.set("v.expenses", theExpenses);
        }
    })
    ```


The common pattern here is `get => process => set` for most handlers and helpers.

The `component.set()` does not affect the data at all if references are updates ([[as it is done here|as it is done here]]). It only triggers a notification that the component has changed, and therefore, the UI is updated (or "re-rendered").

### Solution for challenge

- Code found here inside

    ```jsx
    <aura:application extends="force:slds">
        <c:camping/>
        <!-- <c:campingListItem item=""/> -->
    </aura:application>
    ```

    ```jsx
    <aura:component >
    	<!-- Camping Page Header  -->
    	<lightning:layout class="slds-page-header slds-page-header_object-home">
    		<lightning:layoutItem>
    			<lightning:icon iconName="action:goal" alternativeText="My Camping List"/>
    		</lightning:layoutItem>
    		<lightning:layoutItem padding="horizontal-small">
    			<h1>Camping List</h1>
    			<h2>My Camping List</h2>
    		</lightning:layoutItem>
    	</lightning:layout>
    </aura:component>
    ```

    ```jsx
    <aura:component >
        <aura:attribute name="items" type="Camping_Item__c[]"></aura:attribute>
        <aura:attribute name="newItem" type="Camping_Item__c" default="{
            'sobjectType': 'Camping_Item__c',
            'Name': '',
            'Price__c': 0.00,
            'Quantity__c': 0,
            'Packed__c': false
        }"/>

        <!-- <ol>
        	<li>Bug Spray</li>
            <li>Bear Repellant</li>
            <li>Goat Food</li>
        </ol> -->

        <lightning:layout class="a">
            <lightning:layoutItem padding="around-small" size="6">
                <!-- form here -->
                <div aria-labelledby="newcampingitemform">
                    <fieldset class="slds-box slds-theme_default slds-container_small">
                        <legend id="newexpenseitemform" class="slds-text-heading_small slds-p-vertical_medium">Add Expense</legend>

                        <form class="slds-form_stacked">
                            <lightning:input type="text" aura:id="campingitemform" label="Camping Item Name" name="itemName" value="{!v.newItem.Name}" required="true"/>
                            <lightning:input type="number" aura:id="campingitemform" label="Price" name="itemPrice" value="{!v.newItem.Price__c}" min="0.01"
                                            formatter="currency" step="0.01" messageWhenRangeUnderflow="Enter a higher amount please as this is very low!"/>
                            <lightning:input type="number" aura:id="campingitemform" label="Quantity" name="itemQuantity" value="{!v.newItem.Quantity__c}" min="1"
                                            step="1.0" messageWhenRangeUnderflow="Quantity cannot be less than one!" required="true"/>
                            <lightning:input type="checkbox" aura:id="campingformitem" label="Has been packed?" name="itemHasBeenPacked" checked="{!v.newItem.Packed__c}"/>
                            <lightning:button label="Create Camping Item" class="slds-m-top_medium" variant="brand" onclick="{!c.clickCreateItem}"/>
                        </form>
                    </fieldset>
                </div>
            </lightning:layoutItem>
            <lightning:layoutItem padding="around-small">
                <aura:iteration items="{!v.items}" var="item">
                    <c:campingListItem item="{!item}"/>
                </aura:iteration>
            </lightning:layoutItem>
        </lightning:layout>
    </aura:component>
    ```

    ```jsx
    ({
    	clickCreateItem : function(component, event, helper) {
    		// Validate that the data is OK
    		let validCampingItem = component.find('campingitemform').reduce(function (validSoFar, inputCmp) {
                // Displays error messages for invalid fields
                inputCmp.showHelpMessageIfInvalid();
    			let componentIsValid = inputCmp.get('v.validity').valid;
                return validSoFar && componentIsValid;
            }, true);

    		if (validCampingItem) {
    			let newItem = component.get("v.newItem");
    			console.log("Creating new Camping Item \n" + JSON.stringify(newItem));
    			// helper.createItem(component, newItem);	// Commenting as the questions asks to use the helper logic in the controller itself

    			// HELPER COPIED as the questions needs it to be in the controller itself
    			console.log('Starting createItem helper');
    			let campingItems = component.get("v.items");

    			// DISGUSTING HACK FOR THE TEST. NEVER DO FOR REAL SITUATION.
    			let newItemCopy = JSON.parse(JSON.stringify(newItem));
    			// Add the jsonified item to the list of camping items set at attribute on the component
    			campingItems.push(newItemCopy);

    			// Trigger a re-render
    			component.set("v.items", campingItems);

    			// console.log("Camping Items after insert: \n" + JSON.stringify(campingItems))
    			console.log('Finished createItem helper');

    			// Set the form to blanks
    			component.set(
    				"v.newItem", {
    					'sobjectType': 'Camping_Item__c',
    					'Name': '',
    					'Quantity__c': 0,
    					'Price__c': 0,
    					'Packed__c': false
    				}
    			)
    		}
    	}
    })
    ```

    ```jsx
    ({
    	createItem : function(component, newItem) {
    		console.log('Starting createItem helper');
    		let campingItems = component.get("v.items");

    		// DISGUSTING HACK FOR THE TEST. NEVER DO FOR REAL SITUATION.
    		let newItemCopy = JSON.parse(JSON.stringify(newItem));
    		campingItems.push(newItemCopy);

    		// Trigger a re-render
    		component.set("v.items", campingItems);

    		// Set the form to blanks
    		component.set(
    			"v.newItem", {
    				'sobjectType': 'Camping_Item__c',
    				'Name': '',
    				'Quantity__c': 0,
    				'Price__c': 0,
    				'Packed__c': false
    			}
    		)

    		// console.log("Camping Items after insert: \n" + JSON.stringify(campingItems))
    		console.log('Finished createItem helper');
    	}
    })
    ```

    ```jsx
    <aura:component>
        <aura:attribute name='item' type='Camping_Item__c' required="true"/>
        <aura:attribute name="disabled" type="boolean" default="false"/>
        <!-- <lightning:outputField  -->

        <p>Name:
            <ui:outputText value="{!v.item.Name}"/>
        </p>
        <p>Price:
            <lightning:formattedNumber value="{! v.item.Price__c }" style="currency"/>
        </p>
        <p>Quantity:
            <lightning:formattedNumber value="{! v.item.Quantity__c }" style="decimal"/>
        </p>
        <p>{! 'Packed: ' + v.item.Packed}</p>

        <lightning:input type="toggle"
            label="Packed?"
            name="packed"
            checked="{!v.item.Packed__c}"
        />

        <lightning:button
            label="Packed!"
            onclick="{!c.packItem}"
            disabled="{!v.disabled}"
        />

    </aura:component>
    ```

    ```jsx
    ({
        packItem : function(component, event, helper) {
            component.set('v.item.Packed__c', true);
            component.set('v.disabled', true);
        }
    })
    ```


# Connect to Salesforce with Server-Side Controllers

[[../../../../../../Untitled 3.png|Untitled 3]]

```jsx
public with sharing class ExpensesController {
    // STERN LECTURE ABOUT WHAT'S MISSING HERE COMING SOON
    @AuraEnabled
    public static List<Expense__c> getExpenses() {
        return [SELECT Id, Name, Amount__c, Client__c, Date__c,
                       Reimbursed__c, CreatedDate
                FROM Expense__c];
    }
}
```

- The `@AuraEnabled` annotation before the `method` declaration. “Aura” is the name of the framework at the core of Lightning Components. It is used in the namespace for some of the core tags, such as `<aura:component>`.
- The `static` keyword. All `@AuraEnabled` controller methods must be static methods, and either public or global scope.

```jsx
// Specifying a handler (doInit()) for the "init" event
<aura:handler name="init" action="{!c.doInit}" value="{!this}"/>

// The value="{!this}" is a "mandatory" complicated thing
// that I need to read about in different place
```

## Calling Server-side controller methods

```jsx
// Load expenses from Salesforce
    doInit: function(component, event, helper) {
        // Create the action
        let action = component.get("c.getExpenses");
        // Add callback behavior for when response is received
        action.setCallback(this, function(response) {
            let state = response.getState();
            if (state === "SUCCESS") {
                component.set("v.expenses", response.getReturnValue());
            }
            else {
                console.log("Failed with state: " + state);
            }
        });
        // Send action off to be executed
        $A.enqueueAction(action);
    },
```

[[c and it's many meanings|c and it's many meanings]]

All we need to know about `$A.enqueueAction(action)` (for now):

- It queues up the server request.
- As far as your controller action is concerned, that’s the end of it.
- You’re not guaranteed when, or if, you’ll hear back.

## Handling the Server Response

## Apex controllers for Aura Components

### Checking Access

```jsx
@AuraEnabled
public static List<Expense__c> getExpenses() {
    // Check to make sure all fields are accessible to this user
    String[] fieldsToCheck = new String[] {
        'Id', 'Name', 'Amount__c', 'Client__c', 'Date__c',
        'Reimbursed__c', 'CreatedDate'
    };
    Map<String,Schema.SObjectField> fieldDescribeTokens =
        Schema.SObjectType.Expense__c.fields.getMap();
    for(String field : fieldsToCheck) {
        if( ! fieldDescribeTokens.get(field).getDescribe().isAccessible()) {
            throw new System.NoAccessException();
        }
    }
    // OK, they're cool, let 'em through
    return [SELECT Id, Name, Amount__c, Client__c, Date__c,
                   Reimbursed__c, CreatedDate
            FROM Expense__c];
}
```

# Connect Components with Events

Lightning components are supposed to be self-contained. They are stand-alone elements that encapsulate all of their essential functionality. A component is not allowed to reach into another component, even a child component, and alter its internals.

There are two principal ways to interact with or affect another component.

- The first way is one we’ve seen and done quite a bit of already: setting attributes on the component’s tag. A component’s public attributes constitute one part of its API.
- The second way to interact with a component is through *events*. Like attributes, components declare the events they send out, and the events they can handle. Like attributes, these public events constitute a part of the component’s public API. We’ve actually used and handled events already, but the events have been hiding behind some convenience features. In this unit, we’ll drag events out into the light, and create a few of our own.

There are two types of events, component and application. Here we’re using a component event, because we want an ancestor component to catch and handle the event. An ancestor is a component “above” this one in the component hierarchy. If we wanted a “general broadcast” kind of event, where any component could receive it, we’d use an application event instead
