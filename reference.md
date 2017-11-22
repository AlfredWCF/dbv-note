  according to [the post](https://blog.codinghorror.com/get-your-database-under-version-control/ "get your database under version control")
# when in development about DB [](https://odetocode.com/blogs/scott/archive/2008/01/30/three-rules-for-database-work.aspx)
	* never user a shared database server for development work.
	* always have a single, authoritative source for your schema.
	* always version your database.
# you need a baseline [](https://odetocode.com/blogs/scott/archive/2008/01/31/versioning-databases-the-baseline.aspx)
	* The first step in versioning a database is to generate a baseline schema. This is the starting point for versioning a database. After you've published the baseline to an authoritative source, any changes to the schema require a schema change script.
  	* I like to keep all of the SQL needed to create tables, constraints, defaults, and primary indexes in a single file. Any views, stored procedures, and functions are scripted one per file.
	* Before you baseline the database you need to add a table to record these schema changes.