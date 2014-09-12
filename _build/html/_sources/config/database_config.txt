Database Configurations
=======================

Most online aplications nowdays have a database in it's backend. Here are the settings that allow you to use a database connection::

	$page -> db_connections = array(0 => array(
		'host' => 'localhost',
		'user' => 'my_user',
		'password' => 'my_password',
		'dbname' => 'my_database_name',
		'type' => 'mysql' // this is the default value so no need to put it (Check out PDO for other DB type connections)
	));
	
While the system only uses by default the db connection located at index 0 in the $page->db_connections array, you can set several connections details. Connection will need to be initialised manually by your code.