---
share: "true"
Creation Timestamp: May 13, 2021 8:30 PM
Date Finished: May 14, 2021
Details: Explore key Aura components concepts by comparing them with Visualforce.
Estimated Hours: 1
Has Exam Weight?: No
Points: 700
Status: Done
Tags: Module
Timeline: May 14, 2021
---

# Aura Components Core Concepts


# Bundles and the Request Lifecycle

## Core Concepts

Visualforce and Aura are different in architecture. Not everything maps cleanly between them.

## Concept of Page vs Bundle

VFPs are stored as a single entity in salesforce ⇒ "ApexPage". the controller or static resources or extensions are *referenced and not included* in the VFP.

Aura components have 8 artefacts and separate metadata (total 9). Each individual component is stored in a bundle that *includes* resources.

## Concept of Server-Side vs Client-Side

VFP is server-side, so the server evaluates all expressions `{! }` and everything else, creates the final HTML markup, and sends that to the browser for display.

Aura Components are client-side, so the browser sends all information (static resources, javascript, data) to the browser. The browser runs the JS, and renders the resulting HTML into an existing "page". Expression evaluation, global variables, controller properties—those are all resolved on the client (browser).

[[../../../../../../Untitled.png|Untitled]]

[[../../../../../../Untitled 1.png|Untitled 1]]

[[Difference between Aura and VFP request cycles|Difference between Aura and VFP request cycles]]

# Architectural Concepts

## Concept of Page-by-Page vs Single-Page Applications (SPA)

Instead of getting "pages" as in VFP, Aura components work with one single page, and a Javascript app that runs and updates the user interface of the same page depending on the "*state*".

The SPA knows which components to load for each state, and those components know how to draw, or render, themselves.

Key takeaway: Navigation is very different in Aura components. Depending on how complex your app is and where it runs, you might never need to worry about navigation. Say goodbye to PageReference, $Action, and the anti-pattern of hand-constructed URLs. (The horror!)

## Concept of Page vs Components

Aggregating VFP pages into large pages is horrible and problematic.

Aura components can easily be put one into another.

## Concept of Component vs. Component

Few of the biggest differences. (copied. Need to summarise)

- Aura components can fire and receive events to communicate between components. You can work with framework or container events, or define your own. You write event handlers, and the framework takes care of the details of invoking them when the right event occurs. This is *huge,* and opens up entirely new frontiers in the design of your apps.There’s nothing comparable in Visualforce, unless you roll it yourself. At which point, congratulations, you have your own framework! Now you need an ironic name for it, a GitHub repo, and a hipster hat.
- The Aura component bundle structure has separate artifacts for separate functions and “auto-wires” them together. Being able to group the essential dependencies of a component, while keeping different elements separate, is a terrific organization tool. Value providers and so on makes it easy to use the different elements with minimal ceremony.Again, getting something comparable in Visualforce means you’re writing framework code, not feature code.
- Aura components can be used in more contexts. Indeed, because it’s client-side code, you can use Lightning Out to pull your “Salesforce” features into other, completely *not* Salesforce apps and contexts—can you say SharePoint? Server-bound Visualforce runs only on Salesforce.

## Concept of Application Containers

Distinct containers where your code might run.

- Salesforce Classic
- Visualforce
- Salesforce App
- Lightning Experience
- Lightning App Builder (LAB)
- Lightning console apps
- Communities
- Lightning Components for Visualforce (LC4VF)
- Lightning Out
- Lightning for Outlook and Lightning for Gmail
- Stand-alone my.app

## Container Services

If you fire an event in a container where nothing is listening, does it have an effect? ***No***. What’s the work-around? Write your own container service to create records, and an event handler to catch the event and dispatch it to your custom service.

## Container Containment

Your component can only count on the services of the container it runs in. If you create a component for multiple contexts, you need multiple code paths to account for different sets of services. See [Lightning Components in Visualforce with Lightning Out](https://developer.salesforce.com/blogs/developer-relations/2016/02/lightning-components-visualforce-lightning.html) for an example of this technique.

---

# Coding Concepts

## Concept of Controllers

No standard controller in Aura components (which is present in VFP)

VFP controllers always run on the server side. Aura custom controllers can run in either the server or the client side.

[[../../../../../../Untitled 2.png|Untitled 2]]

VF Controllers

[[../../../../../../Untitled 3.png|Untitled 3]]

Aura Components Controller

While creating VFP and controllers, always use JS remoting and APEX `@RemoteAction` as that helps in later migrating to Aura components.

Lightning Data Service (LDS) is only available in Aura Components, which is close to standard controllers in VF. [Read more here.](https://developer.salesforce.com/docs/atlas.en-us.224.0.lightning.meta/lightning/data_service.htm)

## Concept of Actions

## Concept of Properties vs. Attributes vs. “Expandos”

## Component Attributes

```jsx
// Declaration
<aura:attribute name="myAttribute" type="Integer"/>

// Reference using standard syntax
{!v.myAttribute}

// Getting and setting example in JS
({
    myAction : function(component, event, helper) {
        var counter = component.get("v.myAttribute");
        counter++;
        component.set("v.myAttribute", counter);
    },
})
```

Make attributes private, otherwise it will become part of component's public API.

## JavaScript Expandos and Private Attributes

Quick JS way to set values on the component instance:

```jsx
component._myExpando = "A new string variable";
```

Recommended to not use as they can cause memory leaks ⇒ Instead, use component attributes, and set access level to Private

## Concept of Method Calls vs Events

Let’s conclude with two specific bits of advice.

- **Give the principles of composition and loose coupling a fair shake and some time, and you’ll grow as a developer.**The approach is different than what you’re used to with Visualforce. Some would say it’s harder, but we think it’s a matter of learning and experience.
- **Don’t treat methods the same as you would in Visualforce.** You’ll inevitably discover that you can publish and call methods in your Aura components. It’s tempting, when you run into a design challenge, to fall back on what you know. Resist temptation. Aura component methods *do* have their appropriate uses. Use them when they’re the right tool for the job. Just don’t make them the proverbial hammer that you solve every problem with.

## Questions

- Do Aura components have controllers that are analogous to standard and custom controllers in Visualforce?

    No. LDS is somewhat similar in terms of functionality, but very different in most aspects.

- Which punctuation symbol is the #1 source of syntax errors in Aura component controller code? (. or , or : or %)

    the comma

- What is the mechanism for loose coupling in the Lightning framework?

    Events


---
