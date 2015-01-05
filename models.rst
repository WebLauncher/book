Models
######

Models are the classes that form the business layer in your application.
They should be responsible for managing almost everything
regarding your data, its validity, and its interactions, as well as the evolution
of the information workflow in your domain.

Usually, model classes represent data and are used in WebLauncher applications
for data access. They generally represent a database table but can be used 
to access anything that manipulates data
such as files, external web services, or others.

A model can be associated with other models. For example, a Post
may be associated with an Author as well as a list of Comments.

This section will explain what features of the model can be
automated, how to override those features, and what methods and
properties a model can have. It will explain the different ways to
build associations for your data. It will describe how to get, save, and delete
data.

Understanding Models
====================

A Model represents your data model. In object-oriented programming,
a data model is an object that represents a thing such as a car, a
person, or a house. A blog, for example, may have many blog posts
and each blog post may have many comments. The Blog, Post, and
Comment are all examples of models, each associated with another.

Here is a simple example of a model definition in WebLauncher::

    class posts extends Base {
    
    }

With just this simple declaration, the ``posts`` model is endowed
with all the functionality you need to create queries and to
save and delete data. These methods come from WebLauncher Framework's
Model class by the magic of inheritance. The ``posts`` model
extends the application model, Base, which in turn extends WebLauncher Framework's
internal _Base class. It is this core _Base class that bestows the
functionality onto your ``posts`` model. 

The intermediate class, Base, is empty. If you haven't
created your own, it is taken from the WebLauncher Framework core folder. Overriding
the Base allows you to define functionality that should be made
available to all models within your application. To do so, you need
to create your own ``Base.php`` file that resides in the Model folder,
as do all other models in your application.

Back to our ``posts`` model. In order to work on it, create the PHP file in the
``/modules/site/models/`` directory. By convention, it should have the same name as the class,
which for this example will be ``posts.php``.

.. note::

    WebLauncher Framework will dynamically create a model object for you if it cannot
    find a corresponding file in /modules/site/models. This also means that if
    your model file isn't named correctly (for instance, if it is named 
    post.php or Post.php rather than posts.php), 
    WebLauncher Framework will use an instance of Base rather
    than your model file (which WebLauncher Framework assumes is missing). If
    you're trying to use a method you've defined in your model, or a
    behavior attached to your model, and you're getting SQL errors that
    are the name of the method you're calling, it's a sure sign that
    WebLauncher Framework can't find your model and you need to check the file
    names, your application cache, or both.

.. note::

    Some class names are not usable for model names. For instance,
    "File" cannot be used, since "File" is a class that already exists in the
    WebLauncher Framework core.


When your model is defined, it can be accessed from within your
:doc:`Controller <controllers>`. WebLauncher Framework will automatically
make the model available for access when its name matches that of
the controller:: 

    class posts_page extends Page {
    	public function index() {
        	//grab all posts and pass it to the view
            $posts = $this->models->posts->get_all();
            $this->assign('posts', $posts);
        }
    }

This shows how to use models that are already linked. To understand how associations are
defined, take a look at the :doc:`Associations section <models/associations-linking-models-together>`

More on models
==============

.. toctree::
    :maxdepth: 1

    models/associations-linking-models-together
    models/retrieving-your-data
    models/saving-your-data
    models/deleting-data
    .. models/data-validation
    models/callback-methods
    models/extensions
    .. models/datasources
    models/model-attributes
    models/additional-methods-and-properties
    .. models/virtual-fields
    .. models/transactions


.. meta::
    :title lang=en: Models
    :keywords lang=en: information workflow,csv file,object oriented programming,model class,model classes,model definition,internal model,core model,simple declaration,application model,php class,database table,data model,data access,external web,inheritance,different ways,validity,functionality,queries
