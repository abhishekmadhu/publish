---
share: "true"
---


# Process Automation Specialist

Creation Timestamp: May 13, 2021 8:32 PM
Details: Showcase your mastery of business process automation without writing a line of code
Estimated Hours: 16
Has Exam Weight?: No
Points: 5500
Status: Done
Tags: superbadge
Timeline: May 17, 2021 → May 19, 2021
Trailhead URL: https://trailhead.salesforce.com/content/learn/superbadges/superbadge_process_automation?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential

# PREREQUISITES

Need to finish one more module about lightning.

[[Leads & Opportunities for Lightning Experience|Leads & Opportunities for Lightning Experience]]

# Automate Leads

### **Takeaway:**

Leads can be automatically assigned using lead assignment rules.

⚠️  Do not edit the "Standard" Lead Assignment Rule ⇒ It will not work. Create a new one with any name, and then create the rules inside it.

# Automate Accounts

### **Takeaway:**

The rollup summary and validation rules are really awesome ways to NOT write code and automate stuff.

⚠️  Although they say add "formula fields", all fields should not be formula fields. Use Rollup-Summary as needed.

# Create Robot Setup Object

### **Takeaway:**

⚠️ The business requirement says "So for every sale we close and win, we need a setup record created that we can use for scheduling". You might think that you need to automatically create the setup records as soon as an opportunity is set to "Won". You might also think that how you can automate this without writing code for triggers. The truth is: **YOU DO NOT NEED TO**. You will pass anyway. But even if you pass, after passing the tests, you should try to implement this. 
- Implemented, was pretty easy. 

# Create Sales Process and Validate Opportunities

### **Takeaway:**

- Sales Processes (in SETUP) can be used to customize the stages in the Opportunity.
Later, they can be used for specific Record Types on Opportunity Objects.
So, always create the Sales Process first, then create the Record Type, otherwise you will have to go back again.
- Master-Detail relationships are created in Detail (or "child") objects
- Validation rules — Always check for boolean values if possible ⇒ Makes things easier

ℹ️  If you know about triggers, this assessment will really make you want to use those. Don't, as the tests will not work

# Automate Opportunities

### Takeaway:

- Invokable Processes can be reused, and therefore, should be defined in modular way, and called from other processes.
- Always do negative testing. It means, your code should implement what is required. It should stop the items from being saved as per requirement. But along with that, it should allow the items that pass the validation to be saved. *Seems trivial, but you should test it.*
- **THE DEBUG LOG IS A GOD AND A MESSIAH. PAY YOUR RESPECTS BY USING IT ALL THE TIME WHENEVER YOU CAN instead of fiddling around looking for bugs.**

⚠️  Do not be over-smart and implement stuff that is not specified in the requirements just because you think it is a nice to have validation. No need to follow basic best practices of testing, they can come back and bite you. Only follow salesforce best practices. 

# Create Flow for Opportunities
meh