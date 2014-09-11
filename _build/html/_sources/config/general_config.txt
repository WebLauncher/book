General Configurations
======================

These general configurations will help the system determine how it should function.

**Page trace**::
	
	$page->trace = false;

If true shows a trace help page that helps debug the issues, default value false.
	
**Debug mode**::

	$page->debug = true;

Activates the display of errors, if false all error will be not shown.
	
**Live mode**::

	$page->live = false;
	
If true tells the system that the site is in production so it should stop running debug codes and start optimizing site, also activates cache if configured.
	
**Default Module**::

	$page->default_module = 'site/';
	
This tells the system which is the default module that it should render.
	
**Session Cookie Name**::
	
	$page->session_cookie = 'default_session_cookie';
	
Set it to an appropiate name to your site theme.


While no general configuration is required to be done and most settings have good default values to get you going easily, there might be the case you would like to changed these::
	
	$page->modules_folder = 'modules';
	// module folder to use, this is relative to site root folder
	
	$page->skins_folder = 'skins/';
	// skins folder to use, this is relative to site root folder
	
	$page->files_folder = 'files/';
	// files folder to use, this is relative to site root folder, this needs to have write permissions
	
	