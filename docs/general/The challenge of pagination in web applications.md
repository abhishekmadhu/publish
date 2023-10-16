---
share: "true"
---
#programming

Pagination in web applications is a challenge. 

Quoting [Ashwin Bande](https://stackoverflow.com/users/7769232/ashwin-bande) at [laravel - Is it better to paginate on the server side or front end? - Stack Overflow](https://stackoverflow.com/a/54493622)
> It is A Tradeoff, each one has its own advantages and disadvantages.

### For Server Side Pagination:
1.  your request time and data are reduced, as only a selected no of rows will be sent by the server.
2.  browser required less memory hence faster to process like filter, map, reduce etc.(only for one page)

### For Client Side Pagination:
1.  As all data is present on client machine user can easily switch between back and forth.
2.  filter, search, map, reduce is possible on whole data.
3.  server get few requests as for search, filter, etc needed extra request and many iterations to the server.

## My thoughts
Separate all pagination requirements into two kinds:
