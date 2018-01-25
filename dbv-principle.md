according to [the post about dbv](https://blog.codinghorror.com/get-your-database-under-version-control/ "get your database under version control")

***

# [WHEN WORK WITH DB](https://odetocode.com/blogs/scott/archive/2008/01/30/three-rules-for-database-work.aspx) #

> * never user a shared database server for development work.
> * always have a **single, authoritative source** for your schema.
> * always version your database.

# [YOU NEED A BASELINE](https://odetocode.com/blogs/scott/archive/2008/01/31/versioning-databases-the-baseline.aspx) #

1. The first step in versioning a database is to generate a baseline schema. 

	This is the starting point for versioning a database. After you've published the baseline to an authoritative source, any changes to the schema require a schema change script.
	
2. I like to keep all of the SQL needed to create tables, constraints, defaults, and primary indexes in a single file. Any views, stored procedures, and functions are scripted one per file.

3. Before you baseline the database you need to add a table to record these schema changes.
		
		CREATE TABLE [dbo].[SchemaChanges](
		   [ID] [int] IDENTITY(1,1) NOT NULL,
		   [MajorReleaseNumber] [varchar](2) NOT NULL,
		   [MinorReleaseNumber] [varchar](2) NOT NULL,
		   [PointReleaseNumber] [varchar](4) NOT NULL,
		   [ScriptName] [varchar](50) NOT NULL,
		   [DateApplied] [datetime] NOT NULL,

		    CONSTRAINT [PK_SchemaChangeLog] 
		        PRIMARY KEY CLUSTERED ([ID] ASC)
		)

# [HOW TO DEAL WITH CHANGES](https://odetocode.com/blogs/scott/archive/2008/02/02/versioning-databases-change-scripts.aspx) #

> By "change", I mean a change to a table, index, key, constraint, or any other object that requires DDL, 
> with the **exception** of   views, stored procedures, and functions. 
> I also include any changes to static data and bootstrap data in change scripts.

> Once a script is published into source control, it cannot be changed!
> Once someone updates their database with an update script, they should never have to run the same script on that same database.

> Always backup a production database before applying a change script. 

> For instance, if for some reason we moved column A from the table_a to the table_b, the update script will also need to 
> move and **preserve the data**. Data manipulation is often the trickiest part of change scripts and where they need 
> the most testing.

***

[perhaps you need implent it in a idempotent way](https://haacked.com/archive/2006/07/05/bulletproofsqlchangescriptsusinginformation_schemaviews.aspx/)

here is another atricle which talking about [Evolutionary Database Design](https://martinfowler.com/articles/evodb.html),and [a reading notes](https://github.com/AlfredWCF/dbv-note/blob/master/evolutionary-db-design.md) about it.

# [VIEWS, STORED PROCEDURES, FUNCTIONS, AND TRIGGERS](https://odetocode.com/blogs/scott/archive/2008/02/02/versioning-databases-views-stored-procedures-and-the-like.aspx) #

> script every view, stored procedure, and function into a separate file, then commit the files to source control.

**Jobs in SQL Server and Event scheduler in mysql**

When apply some changes, do as follows:

> 1. The tool applies new schema changes by comparing the available schema change files to the SchemaChangeLog records in the database. 
> 2. The tool will DROP all stored procedures, views, and functions in the database. 
> 3. The tool will run all of the scripts needed to add the views, stored procedures, and functions back into the database. 

# [BRANCHING AND MERGING](https://odetocode.com/blogs/scott/archive/2008/02/03/versioning-databases-branching-and-merging.aspx) #

You have a new baseline(eg: baseline v2.0 than baseline v1.0) which covers baseline v1.0 and all the changes until release our new feature branch.