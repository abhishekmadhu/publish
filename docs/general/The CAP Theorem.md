---
share: "true"
---

#programming
# The CAP Theorem

## Resource:

[http://ksat.me/a-plain-english-introduction-to-cap-theorem](http://ksat.me/a-plain-english-introduction-to-cap-theorem)

All the three of the following cannot be guaranteed at a time

- Consistency - Always same information in all components of distributed system
- Availability - Always available to serve requests
- [[Partition Tolerance|Partition Tolerance]] - Can tolerate communication loss between the components

One workaround is to have availability and [[Partition Tolerance|Partition Tolerance]], but not consistency. Instead, the goal can be to have “**eventual consistency**” (generally by using a batch process to synchronize the information updated in one storage)