## Altering tables

The `ALTER TABLE` statement is used to add, delete, or modify columns in an existing table. it's also used to add and drop various constraints on an existing table.

To add a column in a table, use the following syntax:

```
ALTER TABLE table_name
ADD column_name datatype;
```

The following SQL adds an "Email" column to the "Customers" table:
```
ALTER TABLE Customers
ADD Email varchar(255);
```
To delete a column in a table, use the following syntax (notice that some database systems don't allow deleting a column):

```
ALTER TABLE table_name
DROP COLUMN column_name;
```
To change the data type of a column in a table, use the following syntax:

```
ALTER TABLE table_name
ALTER COLUMN column_name datatype;
```
## Database downtime

**Downtime** refers to periods of time during which a computer system, server or network is shut off or unavailable for use. Systems go through periods of downtime for a variety of reasons, including power or hardware failure, system crashes, hacker attacks, system reboots, operating system and/or software updates, lack of network connectivity and more.

**Databases go down** because they’re either corrupted or unavailable. Depending on the cause of the outage, you may lose a significant amount of data, and this can impact the productivity of the business for days, or weeks.

**SQL table alterations** can interrupt production traffic causing bad customer experience. Not all DBAs, developers, and syadmins know SQL well enough to avoid this pitfall. DBAs usually encounter these kinds of production interruptions when working with upgrade scripts that touch both application and database or if an inexperienced admin/dev engineer perform the schema change without knowing how MySQL operates internally.

## How to Update Database Schema Without Downtime?

Updating a database schema is pretty easy if you can take your application offline. You shut down the application, create a backup of the current database schema, perform all required update operations using tools like Flyway or Liquibase, restart the application, and hope that everything works fine. But that changes if your customers don’t accept any downtime. Simple changes, like removing a column or renaming a table, suddenly require a multi-step migration process. The reason for that is that high-available systems make heavy use of redundancy.

---------------------------------------------------
* Redundancy

     ![](https://i.imgur.com/Pryi2SP.png)

* Rolling Updates
    * Update an instance 
    * Shutdown
    * Update
    * Restart
* Multi-Step Migration Process
* Backward-Compatible Operations
    * Add a table or a view
    * Add a column
    * Remove a column that’s not used by the old
    * Remove constraints
* Backward-Incompatible Operations

    * Rename a column, a table or a view
    * ![](https://i.imgur.com/L8T7mb9.png)

        * Option 1: Sync with database triggers
        * Option 2: Sync programmatically
    * Change the data type of a column
    * Remove a column or table or view that’s still used by the old version of your application

## Summery

Migrating a database schema without downtime is possible, but it often requires a complex, multi-step approach. It requires you to change your database in a backward-compatible way so that the old and the new version of your application can use it.

As you’ve seen in this article, not all migration operations are backward-compatible. But you can split them into multiple steps so that you can create a database version that can be used by both versions of your application. In most cases, that requires you to add a new column or table or view which will be used by the new version of your application. After you updated all application instances, you can then remove the old one.
