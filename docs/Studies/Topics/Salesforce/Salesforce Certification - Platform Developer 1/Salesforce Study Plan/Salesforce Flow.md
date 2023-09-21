---
Creation Timestamp: May 13, 2021 8:31 PM
Date Finished: April 12, 2021
Details: Automate processes for every app, experience, and portal with declarative tools.
Has Exam Weight?: true
Points: 1600
Status: Done
Timeline: April 12, 2021
Trailhead URL: https://trailhead.salesforce.com/content/learn/modules/business_process_automation?trailmix_creator_id=strailhead&trailmix_slug=prepare-for-your-salesforce-platform-developer-i-credential
share: "true"
---

## **Choose the Right Automation Tool**

To sum up the differences:

- Salesforce Flow is the name of the product.
- Flow Builder and Process Builder are the names of the tools.
- Use Flow Builder to make flows; use Process Builder to refine existing processes.

| Use Case | Salesforce Flow Functionality |
| --- | --- |
| Create a guided tutorial or wizard with screens. | Flow Builder includes several out-of-the-box screen components, like text boxes, radio buttons, and file-uploads. If you need more than what’s offered, add custom Lightning components to your screens. |
| Set up automated tasks and processes. | Declaratively configure logic and actions for your business process with Flow Builder. If needed, you can build custom Apex code to fill any functional gaps. |
| Connect to external systems. | Communicate changes between your Salesforce org and your external systems with platform events.Flow Builder lets you respond to and send platform event messages. Flow Builder can also retrieve data from third-party systems with External Services. |
| Add automation to your pages and apps. | Make sure your behind-the-scenes processes start when the right action happens, whether that’s when records change or when users click a particular button.Once you build guided visual experiences, add them to Lightning pages, Experience Builder pages, the utility bar in your Lightning apps, and more. |
| Reuse what you build. | In Flow Builder, break down process logic or actions into a flow that's referenced by a Subflow element. You can reuse or reference this flow in other business processes.In Process Builder, call an autolaunched flow from a process to automate complex business processes.  |

### Decision Making

| Type of Business Process | Description | Available Tools |
| --- | --- | --- |
| Guided visual experience | Business processes that need input from users, whether they’re employees or customers. | Flow Builder |
| Behind-the-scenes automation | Business processes that get all the necessary data from your Salesforce org or a connected system. In other words, user input isn’t needed. | Flow Builder (Recommended)Process Builder (Use for existing processes)Apex |
| Approval automation | Business processes that determine how a record, like a time-off request, gets approved by the right stakeholders. | Approvals |

## **Automate Simple Business Processes with Process Builder**

Trigger - Criteria - Actions (+ Schedule)

| Type | Process Starts When |
| --- | --- |
| Record Change | A record is created or edited |
| Invocable | It’s called by another process |
| Platform Event | A platform event message is received |

 🚨 Safari and Edge behave horribly with Process Builder → The save button goes missing. Stick to Google Chrome for this

 ⚠️ Read the question, stupid!! Disable the damn validation rules!

## **Guide Users Through Your Business Processes with Flow Builder**

Random notes

1. For Allow Multiple Files, select **`$GlobalConstant.True`** in case of file uploads

- **Add Your Flow to the Home Page - details in the trailhead**

### Make Sure Your Users Can Run the Flow

To make sure that your users can run the flow, add the Run Flows user permission to a permission set or profile, and assign it to the right users. If **Override default behavior and restrict access to enabled profiles or permission sets** is selected for the flow, add the flow to a permission set or profile, and assign it to the right users.

Only flow admins (users with the Manage Flow user permission) can run inactive flows.

## **Customize How Records Get Approved with Approvals**

### Preplanning

| In Order to... | We Need... |
| --- | --- |
| Track each opportunity’s discount percent | Custom field (Opportunity) |
| Track each opportunity’s approval status | Custom field (Opportunity) |
| Request approval from managers when an opportunity discount is more than 40% | Approval process (Opportunity) |
| Notify managers when an opportunity discount needs approval | Email template |
| When managers respond, update the opportunity’s approval status | Approval actions (Field Update) |

#todo

- [x]  finish the suggested stuff at the end and read the tell me more
