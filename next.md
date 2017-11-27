# dbv => evolutionary database design => CI & CD => devops #

## [dbv](https://odetocode.com/blogs/scott/archive/2008/02/03/versioning-databases-branching-and-merging.aspx) ##

## [evolutionary database design](https://martinfowler.com/articles/evodb.html) ##

### database migrations ###
* <https://flywaydb.org/>
* <http://liquibase.org/>
* <https://github.com/mybatis/migrations>
* <http://dbdeploy.com/>
* [data migration tool](http://jailer.sourceforge.net/)

> Frameworks like [Liquibase](http://liquibase.org/) and 
> [Active Record Migrations](http://guides.rubyonrails.org/active_record_migrations.html) provide
> a DSL to apply database refactorings, allowing a standard way to apply database migrations.

> However these kinds of standardized refactorings don't work so well for databases since 
> the rules for dealing with data migration and legacy data are very dependent on a team's 
> specific context. So we prefer to handle database refactoring by writing scripts for 
> migration and focus on tools to automate how to apply them.

### All database changes are database refactorings ###

[A collection of database refactoring patterns and database development practices to enable evolutionary database development & Continuous Delivery](http://databaserefactoring.com/)

examples:

* <http://databaserefactoring.com/IntroduceNewColumn.html>
* <http://databaserefactoring.com/MakeColumnNonNullable.html>
* <http://databaserefactoring.com/SplitTable.html>
* <http://databaserefactoring.com/RenameTable.html>

## [continuous integration](https://martinfowler.com/articles/continuousIntegration.html) ##

### CI tools ###
* <https://www.gocd.org/>
* <https://snap-ci.com/>
* <https://jenkins.io/>
* <https://www.atlassian.com/software/bamboo>
* <https://travis-ci.com/>

## [continuous delivery](https://martinfowler.com/bliki/ContinuousDelivery.html)