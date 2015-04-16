Cache
#####

Caching is frequently used to reduce the time it takes to create or read from
other resources. Caching is often used to make reading from expensive
resources less expensive. You can easily store the results of expensive queries,
or remote webservice access that doesn't frequently change in a cache. Once
in the cache, re-reading the stored resource from the cache is much cheaper
than accessing the remote resource.

Caching in WebLauncher Framework is primarily facilitated by the `Stash <http://www.stashphp.com/>`_ library.
This library offer extensive functionality and extensibility for a numerous number of Caching Engines.

In WebLauncher Framework we have a class that facilitates the usage of this library (``CacheManager``).

In a component or model it can be called simply by using ``$this->cache``. This is a reference to the CacheManager instance. This uses the default configuration cache.

To specify a certain cache configuration you can use ``$this->cache('short')``. This gets the Cache Pool configured under the name 'short'.

`Stash <http://www.stashphp.com/>`_ library can be used in any module to configure your own custom cache system.


Configuring Cache
=================

You can configure cache in the configuration files. Read more about :doc:`config/cache_config`. 


Removing Configured Cache Engines
---------------------------------

to do

Writing to a Cache
==================

Use `Stash library documentation<http://www.stashphp.com/Basics.html#examples>`_ about saving data to a cache pool. 
Cache pools are returned either by `$this->cache` (default configuration) or `$this->cache('short')`.

In component or model example::

	// get the cache item
	// path/to/cache_item can be any string to help you identify the cache location
	$item=$this->cache->getItem('path/to/cache_item'); 
	
	// try to get cache item data
	$data=$item->get();
	
	// see if item is in cache
	if($item->isMiss()){
		// lock the cache item so other know you are processing this
		$item->lock();
	
		// get data from the source that you want to cache
		$data=longRunningFunction();
		
		// set data into cache, you can also specify a TTL period as a second argument
		$item->set($data);
	}
	
	// use data for other functinality
	doStuffWithData($data);
	
	

Writing Multiple Keys at Once
-----------------------------

to do

Read Through Caching
--------------------

to do

Reading From a Cache
====================

Use `Stash library documentation<http://www.stashphp.com/Basics.html#identifying-items>`_ about reading data from a cache pool. 
Cache pools are returned either by `$this->cache` (default configuration) or `$this->cache('short')`.

In component or model example::
	
	// get the cache item
	// path/to/cache_item can be any string to help you identify the cache location
	$item=$this->cache->getItem('path/to/cache_item'); 
	
	// try to get cache item data
	$data=$item->get();	

Reading Multiple Keys at Once
-----------------------------

to do


Deleting From a Cache
=====================

Use `Stash library documentation<http://www.stashphp.com/Basics.html#clearing-data>`_ about deleting data from a cache pool. 
Cache pools are returned either by `$this->cache` (default configuration) or `$this->cache('short')`.

In component or model example::

	// get the cache item
	// path/to/cache_item can be any string to help you identify the cache location
	$item=$this->cache->getItem('path/to/cache_item'); 
	
	// clear data from cache
	$item->clear();	

Deleting Multiple Keys at Once
------------------------------

to do

Clearing Entire Pool Cached Data
================================

Use `Stash library documentation<http://www.stashphp.com/Basics.html#emptying-the-entire-cache>`_ about clearing entire data from a cache pool. 
Cache pools are returned either by `$this->cache` (default configuration) or `$this->cache('short')`.

In component or model example::

	$this->cache->flush(); 
	
Running Maintenance
===================

Some caching systems require maintenance actions to occur. This can include things such as removing stale data or reindexing for improved performance.

Use `Stash library documentation<http://www.stashphp.com/Basics.html#running-maintenance>`_ about clearing entire data from a cache pool. 
Cache pools are returned either by `$this->cache` (default configuration) or `$this->cache('short')`.

In component or model example::

	$this->cache->purge(); 


Globally Enable or Disable Cache
================================