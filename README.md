# DB2Audit

These are queries to help assist with retrieving users inside of a DB2 database and the permissions these users are assigned. The queries are designed to only read data and will not modify or create data inside of the database.

## Database Information

Running both queries will show database configuration information, including security settings and the names of the server groups granted SYSADM, SYSCTRL, SYSMAIN, and SYSMON.

```` SQL
GET DATABASE CONFIGURATION
GET DATABASE MANAGER CONFIGURATION
````

## Database Version

This will return the version of the DB2 database. 

```` SQL
db2level
````

## Groups

This will return all users contained in each system group. 

```` SQL
cat /etc/group > group.txt
````

## Users

This will return all user accounts. 

```` SQL
cat /etc/passwd > accounts.txt
````

## Instance Owner

This will return the authorization ID of the instance owner.

```` SQL
db2 "values SYSPROC.AUTH_GET_INSTANCE_AUTHID()"
````

## Authorization IDs

This will return a list of all users, roles and groups that exist in the database catalog.

```` SQL
SELECT *
FROM SYSIBMADM.AUTHORIZATIONIDS
````

## System Privileges

This will show all privileges granted to users, groups, and roles of the database.

```` SQL
SELECT *
FROM SYSIBMADM.PRIVILEGES
````

## Role Authorizations

This will show the roles granted to users, groups, or roles.

```` SQL
SELECT *
FROM SYSCAT.ROLEAUTH
````

## Database Level Authorities

This will show all users granted various administrator-type authorities.

```` SQL
SELECT DISTINCT GRANTEE, GRANTEETYPE, DBADMAUTH, 
SECURITYADMAUTH, ACCESSCTRLAUTH
FROM SYSCAT.DBAUTH
WHERE DBADMAUTH = 'Y' OR
SECURITYADMAUTH = 'Y' OR
ACCESSCTRLAUTH = 'Y' OR
````
