Cache Configurations
====================

There are several configuration related to caching data or pages.

To enable Stash library cache use::

	$this->cache_enabled=true;
	// default it is false
	
To enable page caching (this applies only for Smarty generated pages)::
	
	// to disable or enable page caching
	$this->page_cache_enabled=true;
	// default it is false
	
To configure data cache for Stash library use::

	// to configure caching options
	$this->cache_options=array(
		'short'=>array(
			'type'='file', 
			// other types are 'sqlite','apc','memcached','redis','composite'
			
			 
			'options'=>array(
				'path'=>'path/to/store/cache'
			),
			// read more in Stash library about drivers options.
			
			
			'default'=>true 
			// tell the system if this pool should be used as default and can be accesed by $this->cache  
		)
	);
	
There are several cache drivers supported by `Stash <http://www.stashphp.com/Drivers.html>`_.

By default the system creates a file system cache pool if no other configuration is provided when $this->cache_enabled is true. Cache files are stored in the `cache/_system/` folder.
To clear cache manually just remove that folder.