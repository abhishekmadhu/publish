---
Date Studied: May 12, 2021
Online Materials: https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_triggers_order_of_execution.htm#!
Reviewed: No
Type: Basics
share: "true"
tags:
  - permanent
---


## Schematic Diagram 
![[../../../../../../../Salesforce-Order-Of-Execution-Diagram.png|Salesforce-Order-Of-Execution-Diagram.png]]
![[../../../../../../../Untitled.png|Untitled]]

Source: ([https://prasannajyothi.medium.com/what-is-the-order-of-execution-in-salesforce-c273f9059f6c](https://prasannajyothi.medium.com/what-is-the-order-of-execution-in-salesforce-c273f9059f6c))

[Order of execution in salesforce_ _ by Prasanna _ Medium.pdf](Order_of_execution_in_salesforce____by_Prasanna___Medium.pdf.md)

## Mnemonic for memorization

[https://tomsblogisnotnull.blogspot.com/2019/01/mnemonic-for-salesforce-save-order-of.html](https://tomsblogisnotnull.blogspot.com/2019/01/mnemonic-for-salesforce-save-order-of.html)

> Lion Visits Tiger, Voicing Displeasure to Tiger. Assuming AUTOmatically they Would Fight, he Pounces, ESCALating the ENTanglement Really Furiously, and the Pride Shared the Conquest Party.
>

### Recall Keyword

### Execution Step

**L**ion **V**isits **T**iger

- Load (record is loaded)
- Validation (system validation) rules are run, if the request was sent from a standard UI "edit" page. 
- Triggers (before triggers are executed)

**V**oicing **D**ispleasure to **T**iger

- Validation (system and custom validation)
- Duplicates (Execute duplicate Rules) if record is identified as duplicate and "block" action is taken, no further step is taken down below
- Triggers (after triggers are executed) after the **record is saved**, but **not** committed to database

**ASS**uming **AUTO**matically they **W**ould **F**ight

- Assignment (Execution of assignment rules) [#9]
- Auto-response (execution of auto-response rules) [#10]
- Workflow (execution of workflow rules)

he **P**ounced, **ESCAL**ating the **ENT**anglement **R**eally **F**uriously

- Process (process builder and flow execution)
- Escalation rules execution
- Entitlement rules execution
- Rollup-Summary fields are updated
- Cross-object formulas are updated

the **P**ride **S**hared the **C**onquest **P**arty

- Parent (and grandparent records are updated)
- Sharing (Criteria bases Sharing Rules are evaluated)
- Commit DML Operations to database
- Post-Commit Operations ([sending email](https://www.jitendrazaa.com/blog/salesforce/salesforce-interview-questions-part-3/), etc)

- There are some Additional Considerations to be taken into account while working with Triggers:
    - **TBD**
