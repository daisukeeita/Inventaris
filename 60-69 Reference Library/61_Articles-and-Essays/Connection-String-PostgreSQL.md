---
id: Connection-String-PostgreSQL
aliases: []
tags:
  - postgresql
---

# PostgreSQL Connection String

A **Connection String** is an essential component that enables applications to communicate with databases or other data sources by providing the necessary configuration details.

It [[consolidates]] critical information such as the **server address**, **database name**, **user credentials**, and additional parameters like **port numbers** or **encryption settings**.

**What is a Connection String?**

- The **Connection String** is a string of characters that defines all the details needed to make an _application to allow connection to database or other data sources_.
- It typically includes the server _location_, _host_, _database name_, _user credentials_, and other optional settings such as the _port number_, _encryption methods_, or other parameters.
- This will enable application to access and interact with a database properly and thus ensure _proper authentication_ and _communication_ between the application and the server.

## Basic Format of a Connection String

```
postgresql://[user[:password]@][host][:port][/dbname][?param1=value1&param2=value2]
```

- **postgresql://** -> Identifies the protocol
- **user** -> Username for the database
- **password** -> Password for the user
- **host** -> The address of the PostgreSQL server (e.g., localhost or an IP address)
- **port** -> The port where the PostgreSQL is listening. Default is 5432
- **dbname** -> The name of the database you want to connect to
- **parameters** -> Additional connection options can be passed as URL parameters

## Examples of PostgreSQL Connection Strings

**Example 1:** Local Connection (default port)

```
postgresql://user:password@localhost/mydatabase
```

- This is a PostgreSQL connection URL used to connect to its database. This URL format is commonly used in applications to establish a connection with the specified PostgreSQL database.

**Example 2:** Remote Server Connection

```
postgresql://user:password@192.168.1.100:5432/mydatabase
```

**Example 3:** With SSL

```
postgresql://user:password@localhost/mydatabase?sslmode=require
```

## Server Connection Parameters

- **sslmode** -> Controls SSL Encryption (e.g., require, disable, verify-full)
- **connect_timeout** -> This specifies the number of seconds a program should wait to obtain a connection before it times out.
- **application_name** -> gives a name to the client connection that may help _track connections_ through server logs.

**Example:**

```
postgresql://user:password@localhost/mydatabase?
sslmode=require&connect_timeout=10&application_name=myapp
```

## Environment Variables for Connection Strings

- **PGHOST** -> Hostname of the PostgreSQL server.
- **PGPORT** -> Port Number (default is 5432).
- **PGUSER** -> Username for authentication.
- **PGPASSWORD** -> Password for authentication.
- **PGDATABASE** ->Database name.

# Related Notes

- [[PostgreSQL Administration - Table of Contents]]
- [[PostgreSQL Installation]]
- [[How to Purge and Reinstall the PostgreSQL]]
- [[PostgreSQL Troubleshooting]]

# Resources

- [GeekforGeeks - PostgreSQL Connection String](https://www.geeksforgeeks.org/postgresql/postgresql-connection-string/)
