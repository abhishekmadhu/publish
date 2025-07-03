---
share: "true"
---

# Master Slave Database Architecture

One master, one or more slaves (parent-child is the politically correct term)

**Master**
 - Handled the writes
 - RAM is optimized to writes
 - The disk head can stay where it is for consecutive writes - saves time

**Slave**
 - Handles the reads
 - Essentially a copy of the master
 - RAM is large and can have query caching

This architecture is only good in situations where the system is more read-oriented. For example, in a blogging website, where data is written once (writing the blog) and then read thousands of times. The system hardware and configuration needs to be tuned to the requirements of the specific use-case.