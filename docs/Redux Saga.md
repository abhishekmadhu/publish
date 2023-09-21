---
share: "true"
---

**Summary**
**Installation:** `yarn add redux-saga`
Actions hit the Sagas after they pass through the reducers.  
**Flow of actions:** `Component => MiddleWare => Reducers => Sagas `^130f39


> [!NOTE] 
 Actions fired by a saga will pass through other sagas. 

Redux saga lies largely on [[generator functions|generator functions]] to work. 
![[generator functions#^7b11b9|generator functions > ^7b11b9]]


