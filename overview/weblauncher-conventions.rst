WebLauncher Conventions
#######################

We are big fans of convention over configuration. While it takes a
bit of time to learn WebLauncher's conventions, you save time in the
long run: by following convention, you get free functionality, and
you free yourself from the maintenance nightmare of tracking config
files. Convention also makes for a very uniform system development,
allowing other developers to jump in and help more easily.

WebLauncher's conventions have been distilled from years of web
development experience and best practices. While we suggest you use
these conventions while developing with WebLauncher, we should mention
that many of these tenets are easily overridden – something that is
especially handy when working with legacy systems.

Modules Conventions
===================

Modules are big parts of an app that might require several custom configurations and/or seession handlers. The default module is called site/ and can be found in the /modules/site/ folder.

The stucture of a module is the following:

- ``components``			(components of the module | required)
- ``models`` 				(models of the module | not required)
- ``views`` 				(general views and layouts | required | this can be also structured in skins)
	- ``index.tpl``			(general layout of the module | required)
	- ``404.tpl``			(404 error layout | not required)
	- ``noscript.tpl``		(no javascript section template | not required)
	- ``restricted.tpl``	(restricted area template | not required)
- ``config.php``			(custom module configuration file | not required)
- ``index.php``				(module controller class named PageIndex | required)

Components Conventions
======================

Components are in WebLauncher parts of applicaiton functionality. Each component can have several sub-components located in the ``components`` folder. 

A component structure is like this:

- ``components`` 			(sub-components folder | not required)
- ``views`` 				(views folder for this component | required - also configurable by skin)
- ``models`` 				(custom models folder | not required)
- ``{component_name}.php`` 	(controller class file | required)

A new component can be easily built using ?a=build in the url. For this to work the $page->build_enabled need to be true. 

Controller Conventions
======================

Controller class names are simple to use and follow (ex. home_page - is the controller for the home component). We used lower case writting for fast codding purposes.

The first method you write for a controller might be the
``index()`` method. When a request specifies a controller but not
an action, the default WebLauncher behavior is to execute the
``index()`` method of that controller. For example, a request for
http://www.example.com/apples/ maps to a call on the ``index()``
method of the ``apples_page``, whereas
http://www.example.com/apples/view/ maps to a call on the
``action_view()`` method of the ``apples_page``. Another way to call an action of a controller is by using http://www.example.com/apples?a=view .

You can also use the request method specific actions:

- get_action_view()
- post_action_view()
- delete_action_view()
- put_action_view()

To pass several parameters to the actions you can use http://www.example.com/apples/view/1 which will call action_view($id).

URL Considerations for Controller Names
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As you've just seen, single word controllers map easily to a simple
lower case URL path. For example, ``apples_page`` (which would
be defined in the file name 'apples.php' located under modules/site/components/apples/apples.php) is accessed
from http://example.com/apples.

Multiple word controllers *can* be any 'inflected' form which
equals the controller name so:


-  /redApples
-  /RedApples
-  /Redapples
-  /redapples

will all resolve to the index of the reedapples_page controller. However,
the convention is that your URLs are lowercase and underscored,
therefore /red\_apples/go\_pick is the correct form to access the
``red_apples::action_go_pick`` action.

Model and Database Conventions
==============================

Model class names are lower case and correspond to the database table name to which they have access. This is for simplicity and fast codding.

Ex.

	books => db table books
	
	books_authors => db table books_authors

View Conventions
================

View template files are named after the controller functions they
display, in an underscored form. The action_get() function of the
cars_page class will look for a view template in
/modules/site/components/cars/get.tpl.

The basic pattern is
/modules/{module}/components/{component1}/components/{component2}/views/underscored\_function\_name.ctp.

By naming the pieces of your application using WebLauncher conventions,
you gain functionality without the hassle and maintenance tethers
of configuration. Here's a final example that ties the conventions
together:

-  Database table: "persons"
-  Model class: "persons", found at /modules/site/models/persons.php
-  Controller class: "persons_page", found at /modules/site/components/persons/persons.php
-  View template, found at /modules/site/components/persons/views/persons.tpl

Using these conventions, WebLauncher knows that a request to
http://example.com/persons/ maps to a call on the index() function
of the persons_page, where the persons model is automatically
available (and automatically tied to the 'persons' table in the
database), and renders to a file. None of these relationships have
been configured by any means other than by creating classes and
files that you'd need to create anyway.

.. meta::
    :title lang=en: WebLauncher Conventions
    :keywords lang=en: web development experience,maintenance nightmare,index method,legacy systems,method names,php class,uniform system,config files,tenets,apples,conventions,conventional controller,best practices,maps,visibility,news articles,functionality,logic,WebLauncher,developers
