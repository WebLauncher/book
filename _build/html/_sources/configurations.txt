Configurations
==============

Configurations in WebLauncher framework usually refers to applying some available configurations to the main class (System) and/or it's sub-classes.

For configuring the framework settings you can use the **global config file** (``config.php``) and the **modules config** files (``config.php`` located under each module folder). Also environment based configuration files can be configured.

Using $this variable you can set several settings $thisbase, e-mail, authentication ...) for the framework to use.

While the **global config file** is not restricted to any configuration limitations the **modules config** should be only used to set some minor modules related configurations.

The path to the **global config file** can be modified if required using *SYSTEM_CONFIG_PATH* constant in the ``index.php`` file located in the root of the site. For security reasons this should be moved outside of web public location.
This needs to be a global path. Do not use realtive paths. See example below::

	define('SYSTEM_CONFIG_PATH','/home/account/');

The name of the **global config file** can be modified if required using *SYSTEM_CONFIG_FILE* constant in the ``index.php`` file::

	define('SYSTEM_CONFIG_FILE','my_conf.php');
	
Using **$this->addConfig('{name}', '{hostname}')** you can add per hostname based configuration files that will be loaded if the hostname is matched. Script will try to load 'config.{name}.php' file if existent.

Examples::

	$this->addConfig('test',array('test.com','test1.com'));
	// this will look for the file 'config.test.php' in the root of the folder when the hostname is (www.)test.com or (www.)test1.com
	
	$this->addConfig('development','mylocalhost');
	// this will use the development config for 'mylocalhost' host as well as the previous and default defined values.

Read the following sections to find out more about configurations:

.. toctree::
   :maxdepth: 3
   
   config/general_config
   config/module_config
   config/database_config
   config/email_config
   config/templates_config
   config/cache_config
   config/advanced_config