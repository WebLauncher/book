Advanced Configurations
=======================

There are cases when you would like custom configurations to be applied on different host names or other conditions are satisfied.

By importing conditional configurations files you can accomplish this. This functionality will include several configuration files when condition is matched.

addConfig($name,$hostnames)
---------------------------
::

	$this->addConfig('development','localhost');
	// this will import `config.development.php` when hostname is localhost

	$this->addConfig('development',array('localhost','127.0.0.1'));
	// this will import `config.development.php` when hostname is localhost or 127.0.0.1

	$this->addConfig('development',function($system){
		return isset($_REQUEST['dev']) && $_REQUEST['dev']=1;
	});
	// this will include `config.development.php` when you add to the url the parameter ?dev=1
	// $system is the alias of $this and can be used for checking settings but not for assigning configurations
	// the function defined shoul return true or false based if the file should be loaded or not

Custom configuration files are loaded in the order they are defined and only after the `config.php` file is included completely. They are not included at call time.