# DB2Audit

These are queries to to help assist with retrieving users inside of a DB2 database and the permissions these users are assigned. The queries are designed to only read data and will not modify or create data inside of the database.

## Server Groups

This will show the names of the server groups granted SYSADM, SYSCTRL, SYSMAINT, and SYSMON.

``` SQL
GET DATABASE MANAGER CONFIGURATION
````

## System Privileges

This will show all privileges granted to users, groups, and roles of the database.

```` SQL
SELECT *
FROM SYSIBMADM.PRIVILEGES
````

## Authorization IDs

This will show all AuthIDs and their type.

```` SQL
SELECT *
FROM SYSIBMADM.AUTHORIZATIONIDS
````

## DBADM

This will show all users granted various administrator-type authorities.

```` SQL
SELECT DISTINCT GRANTEE, GRANTEETYPE, DBADMAUTH, 
SECURITYADMAUTH, ACCESSCTRLAUTH, DATAACCESSAUTH
FROM SYSCAT.DBAUTH
WHERE DBADMAUTH = 'Y' OR
SECURITYADMAUTH = 'Y' OR
ACCESSCTRLAUTH = 'Y' OR
DATAACCESSAUTH = 'Y'
````
