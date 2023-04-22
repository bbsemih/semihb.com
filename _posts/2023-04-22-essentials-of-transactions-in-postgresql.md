---
title: Essentials of Transactions in PostgreSQL
date: 2023-04-22 22:25:00 +0800
categories: [transaction, postgresql,database]
tags: [transaction, postgresql,database]
---

It is quite essential to understand the transactions in order to build robust and reliable applications. In this blog post I'll be explaining what a transaction is and what key concepts we should keep in mind when using PostgreSQL.

## Transactions

In almost every database, including Postgres, a transaction refers to a set of database operations that we want to do together. In other words, a transaction is a way to group multiple operations like updates, deletes and inserts, into a single logical unit.

## An Example From Transfering Money

Let's say that we have an "accounts" table where we basically store information about bank accounts, including the customer's name and balance. In this scenario we will be transfering money from one account to another.

```sql
CREATE TABLE accounts (
    id SERIAL PRIMARY KEY,
    name VARCHAR(20) NOT NULL,
    balance INTEGER NOT NULL
);
```

```sql
INSERT INTO accounts (name, balance)
VALUES  ('Semih',200),('Gilfoyle',200);
```
## Opening Transactions

```sql
BEGIN;
```

At the beginning, before opening a transaction let's say that we do have 3 connections to the database and they all connected to the main data pool. 

When we want to open a transaction using the BEGIN keyword, we need to specify which connection we want to use. For example, we might type BEGIN; to open a transaction on the current connection. If we want to open a transaction on a different connection, we would need to switch to it first using the appropriate command. 

As soon as we open up a transaction,(let's say, on connection number 1) we can imagine this process like our database is creating a seperate workspace for that connection. This workspace is isolated from other transactions and is used exclusively for the statements executed within the transaction. No other connections are going to see those changes that we made in that so called seperate workspace.

# Making Changes In Connection #1

In the connection #1 where we opened a transaction earlier, let's update the first user's account by reducing its balance and increment the second user's balance.

```sql
UPDATE accounts

SET balance = balance - 50

WHERE name = 'Semih'
```

```sql
UPDATE accounts

SET balance = balance + 50

WHERE name = 'Gilfoyle'
```


This is the balance result when we run ``` SELECT * FROM accounts``` after the updates:

* Semih's Balance: 150
* Gilfoyle's Balance: 250

But when we switch back to the Connection #2 and run the same query we see that nothing has changed:

* Semih's Balance: 200
* Gilfoyle's Balance: 200

# How to Merge These Changes Into the Main Data Pool?

To merge the changes made within a transaction into the main data pool and make them visible to everyone, committing the transaction is necessary. 

However, in some cases, rolling back the transaction may be necessary to undo the changes we made and revert the database to its previous state. What's more, PostgreSQL can also automatically clean up transactions in specific situations, such as when a client disconnects or a server crash occurs. In these cases, any uncommitted transactions will be rolled back to maintain consistency in the database.













