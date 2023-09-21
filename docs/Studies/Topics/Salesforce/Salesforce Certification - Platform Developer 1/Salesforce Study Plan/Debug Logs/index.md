---
aliases: 
Creation Timestamp: May 13, 2021 8:34 PM
Details: Trailblazer Community Documentation
Estimated Hours: 0.5
Has Exam Weight?: No
Status: Done
tags:
  - Link
Timeline: May 31, 2021 → May 31, 2021
share: "true"
---

# Debug Logs
- The debug log does not include information from actions triggered by time-based workflows.
- Debug logs don’t include transactions that lead conversion triggers. If a converted lead triggers a workflow rule, the debug log doesn’t show that this workflow rule fired.
- Max size allowed for each log = 20MB (older lines are deleted, debug statements can be removed from anywhere)
- Retained for 24 hours max
- 1000MB of logs add restrictions in changing trace flags. To edit them, logs need to be deleted

---

- Session IDs are replaced with "SESSION_ID_REMOVED" in Apex debug logs

[[https//resources.help.salesforce.com/images/68eb4da4ae0eae0a9859667b54797866.png]]

# Debug Log Categories

[[Difference in request cycles of Aura components and Visualforce|Difference in request cycles of Aura components and Visualforce]]

---

# Debug Log Levels

- `NONE`
- `ERROR`
- `WARN`
- `INFO`
- `DEBUG`
- `FINE`
- `FINER`
- `FINEST`

if you select FINE, the log also includes all events logged at the DEBUG, INFO, WARN, and ERROR levels ⬆️⬆️⬆️⬆️⬆️⬆️⬆️⬆️⬆️

[https://help.salesforce.com/articleView?id=sf.code_setting_debug_log_levels.htm&type=5](https://help.salesforce.com/articleView?id=sf.code_setting_debug_log_levels.htm&type=5)

⚠️  Before running a deployment, verify that the Apex Code log level isn’t set to FINEST. Otherwise, the deployment is likely to take longer than expected. If the Developer Console is open, the log levels in the Developer Console affect all logs, including logs created during a deployment.

# Modifying Trace flags

- For user-based trace flags, enter `Debug Logs`  in the Quick Find box, then click **Debug Logs**.
- For class-based trace flags, enter `Apex Classes` in the Quick Find box, click **Apex Classes**, click the name of a class, then click **Trace Flags**.
- For trigger-based trace flags, enter `Apex Triggers`  in the Quick Find box, click **Apex Triggers**, click the name of a trigger, then click **Trace Flags**.
