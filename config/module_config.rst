Module Configurations
=====================

You can do most configurations to the framework using **modules config** files (**config.php** located under each module folder). These will only apply to the current module.

If you only have one module in the site you can just do these configuration directly into the **global config file** (**php.config.php**).

Here are some mostly module area used ones::
	
	$this->title="my site default title";
	// sets the default title of the site
	
	$this->module_user_type='user';
	// this is used by the Authentication module to determine which user type logs in
	