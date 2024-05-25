---
kindle-sync:
  bookId: "1368"
  title: "Salesforce Platform Enterprise Architecture: A must-read guide to help you architect and deliver packaged applications for enterprise needs, 4th Edition"
  author: Andrew Fawcett and Daniel J. Peter
  asin: B0BD8TBT75
  lastAnnotatedDate: 2024-05-23
  bookImageUrl: https://m.media-amazon.com/images/I/81rMnAuRZFL._SY160.jpg
  highlightsCount: 5
share: "true"
---

# Salesforce Platform Enterprise Architecture
## Metadata
* Author: [Andrew Fawcett and Daniel J. Peter](https://www.amazon.comundefined)
* ASIN: B0BD8TBT75
* Reference: https://www.amazon.com/dp/B0BD8TBT75
* [Kindle link](kindle://book?action=open&asin=B0BD8TBT75)

## Highlights
organization of the new sf commands is oriented around the tasks developers perform, while sfdx commands are organized by features. — location: [558](kindle://book?action=open&asin=B0BD8TBT75&location=558) ^ref-62266

---
For example, all commands to manage and interact with environments (such as your Salesforce orgs) are under the env namespace, and ways to deploy to environments are under the deploy namespace. — location: [559](kindle://book?action=open&asin=B0BD8TBT75&location=559) ^ref-50529

---
The project directory layout created by the sf generate project command automatically includes a /force-app folder. As a convention in this book, we will be using a different directory layout for source code that allows us to contain all the source files for the application experiences and open-source libraries used throughout this book. To modify the project directory to support this convention, first create a new source folder in the root of the project, then rename the force-app folder to formulaforce before then moving this folder as a sub-folder into the new source folder. Note that the formulaforce folder will contain a default folder with empty directories, and my preference is to delete these and allow them to be created organically as the application development progresses. Finally, update your sfdx-project.json as shown below to let the sfdx CLI know where the source folder has moved — location: [648](kindle://book?action=open&asin=B0BD8TBT75&location=648) ^ref-44857

---
Salesforce CLI will place files representing the objects and corresponding UI layout information within new subdirectories within the /source/formulaforce/main/default folder. This is because the CLI is not sure of the desired final location of such files. You can now move the two new /objects and /layouts sub-folders directly under /source/formulaforce/main folder to confirm their final location. ==You only need to do this once for new files, once they are moved Salesforce CLI will update them automatically in their new location==. The entire project and the files representing your application can then be stored in source control from this point onward if desired. — location: [691](kindle://book?action=open&asin=B0BD8TBT75&location=691) ^ref-29904

---
There are two types of second-generation packages – managed and unlocked. — location: [704](kindle://book?action=open&asin=B0BD8TBT75&location=704) ^ref-47516

---
