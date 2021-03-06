Modules
=======

A module is a big part of an application, having some or more different configurations and design. While a simple 
application can be built using a single module there might be the case a large application requiring several modules. 
Example: the backend administration of a site, employee space etc.

WebLauncher Frameworks offers the possibility of creating several modules. You can also create several applications it will have the same result.

Structure of a module
---------------------

A module folder has the following structure::

	components/		// [required] the module components folder 
	models/			// [optional] the module models folder 
	objects/		// [optional] the objects folder (here you should store e-mail templates and other objects not related to the MVC structure)
	views/			// [required] the views folder that can be structured by skins
	config.php		// [optional] the module config file
	index.php		// [required] the module controller class (PageIndex extends Page)

Create a module
---------------

WebLauncher Framework offers a code builder that will automatically create a new module. 
Navigate to http://localhost/new_module?a=build-module and this should generate you a new module called 'new_module' if it's not existing.

.. warning::
	For this to work your web server has to have write permissions on the ``modules/`` folder and the ``$this->build_enabled`` configuration needs to be **true**.

To manually create a new module simply go into the ``modules/`` folder and add a new folder called 'new_module'. No space or starting numbers are allowed in the name of the folder. The name should be URL compliant.

The new module should be now accessible using http://localhost/new_module . Accessing this path should pop an error saying that you are missing the PageIndex class for in the ``index.php`` file in the modules.
Since your new module has now code you will have to create an ``index.php`` file and post the following code::

	class PageIndex extends Page {
		
	}
	
Now you have a new module class. However when accessing the module path you will still get a 404 error that the path is not on server. This is because your new module does not have the default
module component ``home``. The framework requires at least the ``home`` component for every the module. 

To check out more about components and how to build them go to :doc:`components section <components>`.

URL Access to modules 
---------------------

The modules should be now accessible using http://localhost/new_module .