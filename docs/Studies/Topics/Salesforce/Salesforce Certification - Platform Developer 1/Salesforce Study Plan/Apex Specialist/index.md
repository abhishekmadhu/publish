---
share: "true"
---


```toc
```

Creation Timestamp: May 13, 2021 8:32 PM
Details: Use integration and business logic to push your Apex coding skills to the limit.
Estimated Hours: 12
Has Exam Weight?: No
Points: 13000
Status: Done
Tags: superbadge
Timeline: May 20, 2021 12:00 AM → May 22, 2021 10:30 PM

# Backdrop

### Standard objects:

- **Maintenance Request (renamed Case) —** Service requests for broken vehicles, malfunctions, and routine maintenance.
- **Equipment (renamed Product) —** Parts and items in the warehouse used to fix or maintain RVs.

### **Custom Objects**

- **Vehicle —** Vehicles in HowWeRoll’s rental fleet.
- **Equipment Maintenance Item —** Joins an Equipment record with a Maintenance Request record, indicating the equipment needed for the maintenance request.

### Entity Diagram

![[../../../../../../Untitled.png|Untitled]]

11:00 to 13:52

# Automate record creation

Use the parent ID to understand which scheduled `Maintenance_Request__c` was created on closure of which "normal" maintenance request, and then link the `Equipment_Maintenance_Request__c` items with the new ones. Use the `Sobject.clone()` judiciously.

# Synchronize Salesforce data with an external system

To make a call from your `Queueable`, also implement the `Database.AllowCallouts` interface.

```jsx
public with sharing class WarehouseCalloutService
implements Queueable, Database.AllowsCallouts {}
```

Use `if(!Test.isRunningTest())` to avoid making callouts while running tests.

Use **JSON2Apex** ([http://json2apex.herokuapp.com/](http://json2apex.herokuapp.com/)) to generate the parser classes quickly.

# Schedule synchronization

In the `Schedulable` , write the whole call logic in one line, otherwise it will not pass the test for some weird reason.

```jsx
// RIGHT, BUT WILL NOT PASS THE TEST FOR SOME REASON
WarehouseCalloutService wcs = new WarehouseCalloutService();
System.debug('Enqueueing WarehouseCalloutService');
System.enqueueJob(wcs);
System.debug('Enqueued WarehouseCalloutService');

// WILL PASS THE TEST
System.debug('Enqueueing WarehouseCalloutService');
System.enqueueJob(new WarehouseCalloutService());
System.debug('Enqueued WarehouseCalloutService');
```

# Test Automation Logic

![[../../../../../../Untitled 1.png|Untitled 1]]

The question asks you to create a test class called `MaintenanceRequestHelperTest` which might make you think that you need to test that helper class directly and achieve 100% coverage.

NO.

They want you to test just the trigger and have 100% coverage on that one line. Makes no sense, I know. But that is what it is.

# Test callout logic

Simple tests. Easy to trick the system. DON'T.
