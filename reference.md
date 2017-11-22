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
> with the exception of   views, stored procedures, and functions. 
> I also include any changes to static data and bootstrap data in change scripts.

