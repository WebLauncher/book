Install
#######

WebLauncher is fast and easy to install. The minimum requirements are a webserver and a copy of WebLauncher, that’s it! While this manual focuses primarily on setting up on Apache (because it’s the most commonly used), you can configure WebLauncher to run on a variety of web servers such as LightHTTPD or Microsoft IIS.

Requirements
============

- HTTP Server. For example: Apache. mod_rewrite is required.
- PHP 5.3.+ or greater.

Technically a database engine isn’t required, but we imagine that most applications will utilize one. WebLauncher supports a variety of database storage engines:

- MySQL (4 or greater)
- PostgreSQL (under development)
- Microsoft SQL Server (under development)
- SQLite (under development)

.. note::

    All built-in drivers require PDO. You should make sure you have the
    correct PDO extensions installed.
    
License
=======

WebLauncher is licensed under the MIT license. This means that you are free to
modify, distribute and republish the source code on the condition that the
copyright notices are left intact. You are also free to incorporate WebLauncher
into any commercial or closed source application.

Downloading WebLauncher
=======================

All current releases of WebLauncher are hosted on
`GitHub <https://github.com/WebLauncher/framework>`_. GitHub houses both WebLauncher
itself as well as many other plugins for WebLauncher. The WebLauncher
releases are available at
`GitHub tags <https://github.com/WebLauncher/framework/tags>`_.

Alternatively you can get fresh off the press code, with all the
bug-fixes and up to the minute enhancements.
These can be accessed from GitHub by cloning the
`GitHub`_ repository::

    git clone git://github.com/WebLauncher/framework.git


Permissions
===========

WebLauncher uses the ``cache/`` directory for a number of different
operations. A few examples would be Model descriptions, cached
views and session information.

As such, make sure the directory ``cache/`` and all its subdirectories in your WebLauncher installation
are writable by the web server user.

One common issue is that the cache/ directories and subdirectories must be writable both by the web server and the command line user.
On a UNIX system, if your web server user is different from your command line user,
you can run the following commands just once in your project to ensure that
permissions will be setup properly::

   HTTPDUSER=`ps aux | grep -E '[a]pache|[h]ttpd|[_]www|[w]ww-data|[n]ginx' | grep -v root | head -1 | cut -d\  -f1`
   setfacl -R -m u:${HTTPDUSER}:rwx cache
   setfacl -R -d -m u:${HTTPDUSER}:rwx cache

Setup
=====

Setting up WebLauncher can be as simple as slapping it in your web
server's document root, or as complex and flexible as you wish.
This section will cover the three main installation types for
WebLauncher: development, production, and advanced.

-  Development: easy to get going, URLs for the application include
   the WebLauncher installation directory name, and less secure.
-  Production: Requires the ability to configure the web server's
   document root, clean URLs, very secure.
-  Advanced: With some configuration, allows you to place key
   WebLauncher directories in different parts of the filesystem, possibly
   sharing a single WebLauncher core library folder amongst many WebLauncher
   applications.

Congratulations! You are ready to :doc:`create your first WebLauncher
application <getting-started>`.

.. meta::
    :title lang=en: Installation
    :keywords lang=en: apache mod rewrite,microsoft sql server,tar bz2,tmp directory,database storage,archive copy,tar gz,source application,current releases,web servers,microsoft iis,copyright notices,database engine,bug fixes,lighthttpd,repository,enhancements,source code,WebLauncher,incorporate
