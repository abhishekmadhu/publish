---
share: "true"
---



Read this first: [Data type number field can store more decimal places than defined (salesforce.com)](https://help.salesforce.com/s/articleView?id=000387302&type=1)

---

[The “number of decimal places” you set for a field in Salesforce determines the precision of the values that can be stored in that field](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1)[1](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1)[2](https://salesforcefaqs.com/set-length-and-decimal-place-for-the-number-field-in-salesforce/). [It refers to the number of digits that are allowed to the right of the decimal point](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1)[2](https://salesforcefaqs.com/set-length-and-decimal-place-for-the-number-field-in-salesforce/).

Here are some factors to consider when deciding the number of decimal places:

1. [**Data Precision**: If the data you are storing requires high precision (for example, financial data), you might want to allow more decimal places](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1)[2](https://salesforcefaqs.com/set-length-and-decimal-place-for-the-number-field-in-salesforce/).
2. [**User Interface**: The number of decimal places is enforced when editing data via the standard web UI](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1)[1](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1). [If you set the decimal places to 2, and try to enter a number with more than 2 decimal places in the UI, it will be rounded off](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1)[1](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1).
3. [**API and Apex**: Apex and API methods can actually save records with more decimal places than defined](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1)[1](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1). [So, if you are mainly interacting with the data programmatically, you might not need to worry as much about the number of decimal places](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1)[1](https://help.salesforce.com/s/articleView?id=000387302&language=en_US&type=1).

In summary, the number of decimal places should be decided based on the precision of the data you are working with and how you plan to interact with the data. Always test thoroughly to ensure the settings meet your requirements.