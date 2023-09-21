---
share: "true"
---


Some items in [[Cisco|Cisco]] are known as Overage. 

Overage items were earlier provided a quantity = 0 in Cisco. 
Currently, we see a few Overage items have a quantity of 1 in Cisco for estimates, and `null` for deal regs. 
- [ ] Need to confirm if there are others with any other quantity value. 

In AJAX Estimate, there is no identifier of whether the item is Overage or not. 
(the description contains the word "overage" but that is not reliable)
in some items we do not have "overage" in the description, but
1. WE have `-O` suffix in the part number
2. We have "usage charge" icon on the item

In estimate, we can decide the "type" of the charging/billing based on the field `chargeType`. 

What to do for deals ❓

1. We can use the quantity = null condition


ANM Requirement:
Ability to change the quote item's quantity to X from 0 when a custom setting is enabled -- ANM-205 (set quantity) + ANM-220 (config)

#### Ensure ==Consistent Data== on BoM for Estimate and Deals
..as Cisco is inconsistent. 

##### Deal
1. the quantity should be change to 0 if and only if the quantity is `null`.  
2. Also, we will set the `chargeType = "Usage"` on the BoM item from the GW. 
3. Set `isUsage__c = true` on BoM item

##### Estimate
All is good. 

#### Changes in calculations

```java
// ANM-220
Find all places where we have logic that is conditional on isOverage__c
For all such places on quote item...
Assume current code is 
if (isOverage){do X}
else {do Y}

==> Switch this to
if (isOverage && !allowOverageOverride){ do X } 
else{ do Y }
```


Quote calculations
1//
```java
src/classes/CalcDefinitions.cls:
194              quoteItem.Quantity__c = quoteItem.Quantity__c != null ? quoteItem.Quantity__c : 1;
195:             if(quoteItem.isOverage__c == true || quoteItem.Quantity__c == 0){
196                  quoteItem.Quantity__c = 1;
				}
```

> [!warning] Quantity values after processing by calculation engine
> The quantity must be reset back to what it was before after the calculations are done by [[Calculation Engine|Calculation Engine]] 

Also check MSDRCalculationDefinitions.cls


2//
```java
src/classes/cls_trg_CustomerBoM_Handler.cls:
  260          //query all related sms quote items
  261:         list < Cust_BoM_Item__c > lst_smsQuoteItems = new list < Cust_BoM_Item__c > ([select id, CustomerBoM__c, Cust_Extended_Price__c, VAR_Total_Cost__c, Quantity__c, Total_List_Price__c, isOverage__c
  262              from Cust_BoM_Item__c

  277              qItem.VAR_Unit_Cost__c = qItem.VAR_Total_Cost__c / qItem.Quantity__c;
  278:             qItem.VAR_Margin__c = qItem.isOverage__c ? 0 : qItem.Cust_Unit_Price__c - qItem.VAR_Unit_Cost__c;
  279              qItem.VAR_Total_Profit__c = qItem.Cust_Extended_Price__c - qItem.VAR_Total_Cost__c;
```


What happens if the user tries to change the item type of an overage item from SAAS to something else (like, Hardware)?
What is the difference between isUsage__c  and isOverage__c ?
What happens if we end up with a wrong data state -- `HARDWARE` item with `isOverage__c == true`? (via Disti Import maybe): We should prevent by some kind of validation.

