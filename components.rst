Components
==========

A **component** is a small part of an application that serves for handling a part of the application functionality. Each module has at least one component ``home``. 
The ``home`` component is required for the module to work. 

.. note::
	Ex. In a blog application you should have ``post`` component to handle the display/edit of a post.
	
Components can be hierachically organised. Each component can have one or more sub-components.

.. note::
	Ex. The ``post`` component can have ``view`` and ``edit`` sub-components.
	
Structure of a component
------------------------

A component folder has the following structure::

	components/  		// [optional] this folder contains the sub-components of the current component
	models/				// [optional] this folder can contain the models defined for this controller
	views/				// [required] this folder contains the views that can be structured by skins
	component.php		// [required] this is the controller class that serves this component `component`
	
Each component has a controller class that controls the functionality flow. :doc:`Read more about controllers</controllers>`.

Create a component
------------------

WebLauncher Framework offers a code builder that will automatically create a new component. 
Navigate to http://localhost/new_module/new_component?a=build and this should generate you a new component ``new_component`` if it's not existing.

.. warning::
	For this to work your web server has to have write permissions on the ``modules/new_module/components/`` folder and the ``$this->build_enabled`` configuration needs to be **true**.

To manually create a new component simply go into the ``modules/new_module/components/`` folder and add a new folder called 'new_component'. No space or starting numbers are allowed in the name of the folder. The name should be URL compliant.

The new component should be now accessible using http://localhost/new_module/new_component . Accessing this path should pop a 404 error.
Since your new component has no controller code you will have to create an ``new_component.php`` file and post the following code::

	class new_component_page extends Page {
		
	}
	
Now you have a new component class. However this new component won't have any view defined. For this component to have a default view defined create the folder ``views/`` in your 
new component folder and add a new file called ``new_component.tpl`` in that folder.

Now you should have a fully functional component. 

To check out more about controllers go to :doc:`controller section <controllers>`.


URL Access to a component
-------------------------

Each component can be accesed via the url given in the browser. Here is an example:

.. note::
	To access the ``post`` component of the module ``blog`` of an application hosted at ``localhost`` you use:
	
	http:://localhost/blog/post/
	
You will be able to access that controller for coding by accessing the appropiate folder on the path described by the url. 

.. warning::
	When using routes in configurations you might find the controllers only by checking out the configured routes.