---
share: "true"
---


## Problem

## Read more:
- Wrong solution to do this: https://salesforce.stackexchange.com/questions/10307/cyclic-trigger-calls

- Add following comment:
	- Use a condition to check if you really need to update a record, based on any condition.
	- Creating a static variable to achieve this is a horrible idea in most situations (situations where more than 200 records of the Object might be updated/inserted at once).
	- The static variable will be shared across trigger runs, and therefore, all the "chunks" except the first chunk will provide incorrect results.
	- Details can be found here: https://nebulaconsulting.co.uk/insights/please-dont-use-static-flags-to-control-apex-trigger-recursion/
