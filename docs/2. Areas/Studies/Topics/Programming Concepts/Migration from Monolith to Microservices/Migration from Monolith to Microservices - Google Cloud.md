---
share: "true"
---


Source: https://cloud.google.com/architecture/microservices-architecture-introduction


Notes: 
1. Each microservice should have it's own database
2. All database transactions should be atomic. So if there are any transactions that are "cross-service" and the databases of all the services need to be updated, the entire transaction should be atomic. 
	1. This means that in case one of the transactions fail, the previous transactions must be rolled back. 
	2. A service should probably manage those transactions - use a message queue where applicable 
3. Need to understand if it is worth it to migrate given the drawbacks
![[Drawing 2022-09-21 18.01.06.excalidraw|Drawing 2022-09-21 18.01.06.excalidraw]]





