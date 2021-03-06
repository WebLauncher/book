.. WebLauncher Framework documentation master file, created by
   sphinx-quickstart on Thu May 08 18:56:29 2014.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome To WebLauncher Framework Book
=================================================

This book is mostly appliable to 2.7+ releases of the framework. Most of the functionalities are also available in pre 2.7 releases. To be sure that the functionalities are available check the API Docs of those releases.

**WebLauncher** framework is built with the ideea of keeping things simple and easy to implement. 
Use this documentation to get familiar with the development tehniques used to implement a website or app using this framework.

Requirements
------------

Apache 2.2+

PHP 5.3.3+ [Recomended 5.4+ or 5.5+]

**Apache Modules**

Required

``mod_rewrite``

Recomended [production]

``mod_security``

``mod_filter``

``mod_deflate``

``mod_expires``

**PHP Extras**

Required

``PDO``

``GD``

``MCrypt``

``curl``

``mb_string``

Recomended [production]

``APC`` or ``EAccelerator`` or ``OPCache``

``SOAP``

``Posix``

``mb_regex``

Contents
--------

.. toctree::
   :maxdepth: 3
   
   overview
   install
   getting-started
   update
   configurations
   migrations
   modules
   components	
   controllers
   models
   views
   cache