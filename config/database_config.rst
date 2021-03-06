Database Configurations
=======================

Most online applications now days have a database in it's backend. Here are the settings that allow you to use a database connection::

	$this -> db_connections = array(0 => array(
		'host' => 'localhost',
		'user' => 'my_user',
		'password' => 'my_password',
		'dbname' => 'my_database_name',
		'type' => 'mysql' // this is the default value so no need to put it (Check out PDO for other DB type connections)
	));
	
While the system only uses by default the db connection located at index 0 in the $this->db_connections array, you can set several connections details. Connection will need to be initialised manually by your code.

WebLauncher Framework allows database table aliasing. Which means that you can give shorter name to the models that get associated with the db tables by using::

	$this -> tables = array(
		'pages' => 'my_site_pages',  // this will alias 'my_site_pages' table to 'pages' model
		...
	);
	
.. warning::

    In previous versions of the framework 'pages' would have to be replaced by 'tbl_pages'.