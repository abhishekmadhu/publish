---
share: "true"
---

# Difference in request cycles of Aura components and Visualforce

Aura Components Request Cycle: 1. The user requests an application or a component
2. The application or component bundle is returned to the client
3. The browser loads the bundle
4. The JavaScript application generates the UI
5. When the user interacts with the page, the JavaScript application modifies the user interface as needed (return to previous step)
![[../../../../../../../Untitled.png|200]]

Visualforce Request Cycle: 1. User requests a page
2. The server executes the page’s underlying code and sends the resulting HTML to the browser
3. The browser displays the HTML
4. When the user interacts with the page, return to step one