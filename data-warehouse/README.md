# Azure Synapse Analytics

- formerly Azure SQL Data Warehouse (SQL DW)

- Massively Parallel Processing (MPP) Data Warehouse

- Connection Security - Firewall rules are used by both the server and the database to reject connection attempts from IP addresses that haven't been explicitly whitelisted.

- Authentication - SQL pool currently supports SQL Server Authentication with a username and password, and with Azure Active Directory.

- Authorization - Authorization privileges are determined by role memberships and permissions. Authorization privileges are determined by role memberships and permissions.

- Data Encryption - protects against the threat of malicious activity by encrypting and decrypting your data at rest. Associated backups and transaction log files are encrypted without requiring any changes to your applications when encrypting your database.

- Advanced Data Security - provides a set of advanced SQL security capabilities, including data discovery & classification, vulnerability assessment, and Advanced Threat Protection.

## Transparent Data Encryption (TDE)

- It helps protect against the threat of malicious activity by encrypting and decrypting your data at rest. When you encrypt your database, associated backups and transaction log files are encrypted without requiring any changes to your applications. TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.

## Granular access controls

- Granular Permissions let you control which operations you can do on individual columns, tables, views, schemas, procedures, and other objects in the database. Use granular permissions to have the most control and grant the minimum permissions necessary. 

- Database roles other than db_datareader and db_datawriter can be used to create more powerful application user accounts or less powerful management accounts. The built-in fixed database roles provide an easy way to grant permissions, but can result in granting more permissions than are necessary.

- Stored procedures can be used to limit the actions that can be taken on the database.

## Service Type

- Compute Optimized Gen1

- Compute Optimized Gen2

## Scalability

- Linear Scale on data warehouse unit

## Backup

- Use data warehouse snapshot to create a restore point
