# Constraints--SQL
Constraints- SQL

                     I CREATE TABLES 
					 ---------------
Create the following below tables.

A. dbo.Customer
Columns:
CustID (int, null)
CustName (varchar(50), null)
EntryDate (datetime, null)

B. dbo.SalesReps
Columns:
RepID (int, null)
RepName (varchar(50), null)
HireDate (datetime, null)

C. dbo.Sales
Columns:
SalesID (int, null)
CustID (int, null)
RepID (int, null)
SalesDate (datetime, null)
UnitCount (int, null)
VerificationCode (varchar(50), null)*/

/*
1A. Table dbo.Customer*/

CREATE TABLE dbo.Customer
(
CustID INT NULL,
CustName VARCHAR(50) NULL,
EntryDate DATETIME NULL
)

/*
1B. Table dbo.SalesReps*/

CREATE TABLE dbo.SalesReps
(
RepID INT NULL,
RepName VARCHAR(50) NULL,
HireDate DATETIME NULL
)

/*
1C. Table dbo.Sales*/

CREATE TABLE dbo.Sales
(
SalesID INT NULL,
CustID INT NULL,
RepID INT NULL,
SalesDate DATETIME NULL,
UnitCount INT NULL,
VerificationCode VARCHAR(50) NULL
)

/*
II CONSTRAINTS
--------------

Create Primary keys on all 3 tables
1A. Create Primary Key on table Customer*/

ALTER TABLE Customer
ALTER COLUMN CustID INT NOT NULL

ALTER TABLE Customer
ADD CONSTRAINT PK_Customer_CustID PRIMARY KEY (CustID)

/*
1B. Create Primary Key on table SalesReps*/

ALTER TABLE SalesReps
ALTER COLUMN RepID INT NOT NULL

ALTER TABLE SalesReps
ADD CONSTRAINT PK_SalesReps_RepID PRIMARY KEY (RepID)

/*
1C. Create Primary Key on table Sales*/

ALTER TABLE Sales
ALTER COLUMN SalesID INT NOT NULL

ALTER TABLE Sales
ADD CONSTRAINT PK_Sales_SalesID PRIMARY KEY (SalesID)

/*

All 3 tables should have IDENTITY columns as the PRIMARY KEY’s. They must start at 100
and increment by 2.
ANSWER: PLEASE REFER THE WORD DOCUMENT FOR THE ANSWER ie SUNILKUMAR SUKUMARAN - 105. CONSTRAINTS.doc */

/*
3. Create a Unique Key on dbo.Sales.VerficationCode */

ALTER TABLE Sales
ADD CONSTRAINT UC_Sales_VerificationCode UNIQUE (VerificationCode)

/*
4. Create a relationship between the Customer / SalesRep & the Sales Table

4A. Create a relationship between the Customer & Sales Table */

ALTER TABLE Sales
ADD CONSTRAINT FK_CustomerSales_CustID
FOREIGN KEY (CustID) REFERENCES Customer(CustID)

/*
4B. Create a relationship between the SalesReps & Sales Table*/

ALTER TABLE Sales
ADD CONSTRAINT FK_SalesRepsSales_RepID
FOREIGN KEY (RepID) REFERENCES SalesReps (RepID)

/*
5. No nulls will be allowed in the following tables.columns

A. dbo.Sales.SalesDate

B. dbo.Sales.VerificationCode

5A. NOT NULL CONSTRAINT on the column dbo.Sales.SalesDate*/

ALTER TABLE Sales
ALTER COLUMN SalesDate DATETIME NOT NULL

/*
5B. Create NOT NULL CONSTRAINT on the column dbo.Sales.VerificationCode*/
ALTER TABLE Sales
DROP CONSTRAINT UC_Sales_VerificationCode

ALTER TABLE Sales
ALTER COLUMN VerificationCode VARCHAR(50) NOT NULL

/*
6. The following tables.columns will default to GetDate() if no Date is given.

A. dbo.Customer.EntryDate

B.dbo.SalesRep.HireDate

c.dbo.Sales.SalesDate*/

/*
6A. Create DEFAULT Constraint on column dbo.Customer.EntryDate where the default value is GetDate()*/

ALTER TABLE Customer
ADD CONSTRAINT DF_Customer_EntryDate
DEFAULT GETDATE() FOR EntryDate

/*
6B. Create DEFAULT Constraint on column dbo.SalesRep.HireDate where the default value is GetDate()*/

ALTER TABLE SalesReps
ADD CONSTRAINT DF_SalesReps_HireDate
DEFAULT GETDATE() FOR HireDate

/*
6C. Create DEFAULT Constraint on column dbo.Sales.SalesDate where the default value is GetDate()*/

ALTER TABLE Sales
ADD CONSTRAINT DF_Sales_SalesDate
DEFAULT GETDATE() FOR SalesDate

/*
7. dbo.Sales.UnitCount should not allow NULLS or Zero’s*/

ALTER TABLE Sales
ADD CONSTRAINT CHK_Sales_UnitCount CHECK (UnitCount IS NOT NULL AND UnitCount <> 0);

/*

Run the following script to ensure the Constraints have been added correctly*/
INSERT INTO dbo.Customer (CustName)
SELECT 'Ali' UNION
SELECT 'Anand' UNION
SELECT 'Alex' UNION
SELECT 'Jack' UNION
SELECT 'Nina' UNION
SELECT 'Joel' UNION
SELECT 'Keon' UNION
SELECT 'James' UNION
SELECT 'Mike' UNION
SELECT 'Sai' UNION
SELECT 'Terry'

INSERT INTO dbo.SalesReps (RepName)
SELECT 'Joseph' UNION
SELECT 'Jermaine' UNION
SELECT 'Marshall' UNION
SELECT 'Marvin' UNION
SELECT 'Mitchell' UNION
SELECT 'Johnson' UNION
SELECT 'Robert' UNION
SELECT 'Rachel' UNION
SELECT 'Rene' UNION
SELECT 'Brandy'UNION
SELECT 'Dirk'

INSERT INTO dbo.Sales (CustID, RepID,UnitCount,VerificationCode)
SELECT 100,120,1,'Ver01' UNION
SELECT 102,118,2,'Ver02' UNION
SELECT 104,116,3,'Ver03' UNION
SELECT 106,114,4,'Ver04' UNION
SELECT 108,112,5,'Ver05' UNION
SELECT 110,110,1,'Ver06' UNION
SELECT 112,108,2,'Ver07' UNION
SELECT 114,106,3,'Ver08' UNION
SELECT 116,104,4,'Ver09' UNION
SELECT 118,102,5,'Ver10' UNION
SELECT 120,100,6,'Ver11'
