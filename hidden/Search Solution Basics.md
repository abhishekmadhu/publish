---
share: "true"
---

# Search Solution Basics

Creation Timestamp: May 13, 2021 8:31 PM
Details: Learn how search works, navigate use cases, and optimize search results.
Estimated Hours: 1
Has Exam Weight?: No
Points: 300
Status: Done
Tags: Module
Timeline: May 16, 2021 → May 16, 2021

# How it works

## When saving the records

When saving any record, Salesforce Search Engine

- Makes a copy of the record
- Breaks the record down into small pieces called "tokens"
- Saves the tokens in a "Search index"

## When performing a search

When the user searches by writing "search terms" in the search bar, SSE

- Breaks the search term down into tokens
- Matches the tokens with the information in search index
- Ranks the results matched by relevance
- Returns the results to which the user has access

Both SOQL and SOSL can be used in all cases. They can be executed through REST and SOAP APIs, and also through APEX.

# Building Search for Common Use Cases

## Search Within a Single Object

```jsx
FIND {term} RETURNING ObjectTypeName
// term: whatever the user enters
// ObjectTypeName is the API name of the object

// Example:
FIND {march 2016 email} RETURNING Campaign
```

## Search Within Multiple Objects

```jsx
FIND {term} RETURNING ObjectTypeName1, ObjectTypeName2, ObjectTypeNameYouGetTheIdea

// Comma separated list of object API names

// Example
FIND {recycled materials} RETURNING Product2, ContentVersion, FeedItem
```

## Search Within Custom Objects

Same as with normal objects

`FIND {pink hi\-top} RETURNING Merchandise__c`

# Optimize Search Results

## Limiting data that is searched

`IN SearchGroup`

Use this to search for the term only in email type fields

```jsx
FIND {jsmith@cloudkicks.com} IN EMAIL FIELDS RETURNING Contact
```

`FIND {term} RETURNING ObjectTypeName (FieldList ORDER BY Field LIMIT Limit OFFSET Offset)`

```jsx
FIND {Cloud Kicks} RETURNING Account (Name, Industry ORDER BY Name LIMIT 10 OFFSET 25)
```

`WITH` statements filter records by certain predefined fields.

```jsx
FIND {race} RETURNING KnowledgeArticleVersion
    (Id, Title WHERE PublishStatus='online' and language='en_US')
    WITH DATA CATEGORY Location__c AT America__c
```

### Summary

[[Search Keywords|Search Keywords]]

## Display Suggested Results

Use the API. Example:

```jsx
// Sample Query
/vXX.X/search/suggestTitleMatches?q=race+tips&language=en_US&publishStatus=Online

// Sample Response
{
  "autoSuggestResults" : [ {
    "attributes" : {
    "type" : "KnowledgeArticleVersion",
    "url" : "/services/data/v30.0/sobjects/KnowledgeArticleVersion/ka0D00000004CcQ"
    },
  "Id" : "ka0D00000004CcQ",
  "UrlName" : "tips-for-your-first-trail-race",
  "Title" : "race tips",
  "KnowledgeArticleId" : "kA0D00000004Cfz",
  "isMasterLanguage" : "1",
  } ],
  "hasMoreResults" : false
}
```
