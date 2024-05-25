---
share: "true"
---


# Disti Quote Merge

# Question

## UI (Visualforce and APEX syntax and understanding)

- [x]  Create a form in a visualforce page to take items as an input
- [x]  Each item should have following fields:
    - [x]  `Part_Number__c` : (String) is an unique identification of one product type, same for all of the same type (IE: all IDENTICAL routers of company X has same part number)
    - [x]  `Quantity__c` :  (Integer) denotes the number of items bought for that part number (If someone buys 10 packets of same potato chips from one company, the quantity is `10`)
    - [x]  `Quote__c` : (String) denotes the quotation it belongs to (for now, assume it to be a bill number of the purchase. Of course, one bill can have multiple items). Ideally, this should be a separate objet with master detail relationship, but for now, use alphanumeric strings for this. Can be bla Quote_Text__c
    - [x]  `Type__c`: (dropdown single-selection, options: `["bom", "disti"]`) denoted the type of vendor from whom this purchase was made
- [x]  The items should be saved in one object `Item__c` upon clicking save
- [x]  The items, as soon as saved, should be updated and displayed below the input form in a separate component (preferably a list component containing individual item components)
- [x]  The items, when displayed, should be separated into two different lists, depending on the `Type__c` field on each item
- [ ]  There should be two buttons in the form
    - [x]  Save (to save the items into database)
    - [ ]  Compare (to initialise the next part of the solution, and print the result in the debug console)

## Pure APEX (Testing logical and algorithmic abilities)

Please write an Apex class and a Test Class that resolves the following problem.

The sample data should be used in the Test Class. The method should be generic and receive the data as input and return the result. The test class should use `System.debug()` to print the output table. You can Copy/Paste the result from the log.

Enter the test data given below into the UI created in the previous test and show as output the “Unified List”.

### The Input:

2 lists of key: value pairs called “BoM” and “Disti”

Each has “Part Number” as a key and “Quantity” as a number.

Part Number may appear multiple times in the BoM with an arbitrary Quantity (including zero)

Part Number will appear only once in Disti, in other words, Quantities will be aggregated..

Part Numbers may exist only in BoM or only in Disti (there is no quantity zero)

The purpose is to “intelligently” compare the BoM and Disti, after fixing the Disti Quantity if needed, and showing items missing on each side.

### The Expected Result.

Create a 3rd list, with 5 fields: bom_pn, bom_qty, Dsti_pn, Dsti_qty, Error Flag.

All items from the BoM will appear as is and based on the same order of the input BoM.

Against each bom_pn there should be a Dsti_pn (if one exists). If Disti is missing a Part Number, the Disti side should be left blank and Error Flag should be checked

It is possible that Disti will be missing PN or BOM will be missing some Part Numbers

If Disti Quantity is bigger than BoM Quantity (for any given Pat Number), Disti line should be **split** to match the Quantity of the BoM, and the remainder should be aligned with another BoM line, if exists.

If there is another record with same part number, the above should be repeated.

The joint list should be as similar as possible in term of quantities.

You may end up with some lines that do not have a Disti values, and vice-a-versa.

No matter what, the overall BoM side in the Unified Table should be the same as the original BoM.

The Disti Side, as a whole, should include all items from original Disti, even if lines were split.

### Test Data

Below is the test data you should use and the expected result of the algorithm. The code must actually run and produce results using system.debug().

Develop the class/methods and a unit test with the sample data given below.

[[BOM|BOM]]
[[Disti|Disti]]
[[Unified List |Unified List ]]

## Optional

- [ ]  Create a button to edit the items on the flow from the visualforce page
- [ ]  Clear the new item entry form after the last item have been saved (save button is clicked and the save is successful)

# Solution

```python
https://github.com/abhishekmadhu/distiQuoteMerge_example.git
```

Now do the same UI with LWC and datatable
