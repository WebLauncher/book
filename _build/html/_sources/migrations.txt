Migrations
==========

**WebLauncher Framework** has a build-in DB migration system. The migration functionality can handle two types of migration files. One is a 
SQL query run (this method does not have a reverse run) and the other is a ``Migration`` object class file where you can run queries and scripts 
to define your migration.

Configuring migrations
----------------------

Migrations list is defined in ``db\migrations.php`` file which returns an associative array in the structure of '$version'=>'$file_name'.
Note: ``$file_name`` should not have the extension added. See example::

	return array(
		'1'=>'migration_1',
		'2'=>'migration_2'
		...
	);
	// this will define 2 versions of the DB using the migrations

Defining a migration
--------------------

A **migration** is a file (sql or php file that contains a class that extends ``Migration``) located in the ``db/migrations/`` folder.

There are two ways of defining a migration:

1. Using a SQL file which contains the queries that need to be executed. This will look for ``$file_name.sql`` into the migrations folder. (this will not be executed on down migrations)
2. Using a php file which contains the definition of a class named ``$file_name`` that extends ``Migration`` class. ``Migration`` class also extends ``Base`` which is the model class so you have access to all the methods from the models. We recommend sticking to ``$this->query($sql)`` method and using the DbManager ``$this->db`` for handling migrations. See an example below::

	class migration_1 extends Migration{
		function up(){
			// define here all the queries that need to be run to upgrade the db version
			$this->query(sql);
			$data=$this->db->getAll(sql); // to retrieve data from db
		}

		function down(){
			// define here all methods that need to be run to downgrade the db version
		}

		function before($direction='up'){
			// define here code that needs to be executed before the method up() or down() are run
		}

		function after($direction='up'){
			// define here code that needs to be executed after the method up() or down() are run
		}
	}

When using the php way you can also define ``migration_1.up.sql`` and/or ``migration_1.down.sql`` for them to be run after methods ``up()`` and/or ``down()`` are run.

Running migrations
------------------

Migrations can be run using the browser url to you site by adding http://localhost/?a=migrate:all. This will run all found migrations that were not run.
The script requires write access to ``files`` folder so it can store the migrated versions of the DB.

Running migration up or down
----------------------------

To run up a migration in browser http://localhost/?a=migrate:up .

To run down a migration in browser http://localhost/?a=migrate:down .

To run up a migration with id 1 in browser http://localhost/?a=migrate:up:1 .

To run down a migration with id 1 in browser http://localhost/?a=migrate:up:1 .

Running migration from the php console (in development)
-------------------------------------------------------

When the console is in the root folder.

::

    php index.php --migrate
    // to migrate all
    php index.php --migrate up
    // to migrate up
    php index.php --migrate down
    // to migrate down
    php index.php --migrate [up|down] {ID}
    // to execute up or down migration {ID}
