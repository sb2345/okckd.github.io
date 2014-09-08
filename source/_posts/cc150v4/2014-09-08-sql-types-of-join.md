---
layout: post
title: "[CC150v4] 15.2 SQL Types of Join "
comments: true
category: CC150v4
tags: [  ]
---

### Question

> What are the different types of joins? Please explain how they differ and why certain types are better in certain situations. 

### Answer 

1. INNER JOIN: Returns all rows when there is at least one match in BOTH tables

1. OUTER JOIN

    1. LEFT JOIN: Return all rows from the left table, and the matched rows from the right table

    1. RIGHT JOIN: Return all rows from the right table, and the matched rows from the left table

    1. FULL JOIN: Return all rows when there is a match in ONE of the tables. If no matching record was found then the corresponding result fields will have a NULL value. 

[source](http://www.w3schools.com/sql/sql_join.asp)
