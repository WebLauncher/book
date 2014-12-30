Extensions
##########

Model extensions are a way to organize some of the functionality
defined in WebLauncher Framework models. They allow us to separate and reuse logic that
creates a type of behavior, and they do this without requiring inheritance. For
example creating tree structures. By providing a simple yet powerful way to
enhance models, behaviors allow us to attach functionality to models by defining
a simple class variable. That's how behaviors allow models to get rid of all the
extra weight that might not be part of the business contract they are modeling,
or that is also needed in different models and can then be extrapolated.

As an example, consider a model that gives us access to a database table which
stores structural information about a tree. Removing, adding, and migrating
nodes in the tree is not as simple as deleting, inserting, and editing rows in
the table. Many records may need to be updated as things move around. Rather
than creating those tree-manipulation methods on a per model basis (for every
model that needs that functionality), we could simply tell our model to use the
:php:class:`BaseTree`, or in more formal terms, we tell our model to behave
as a Tree. This is known as attaching a behavior to a model. With just one line
of code, our WebLauncher Framework model takes on a whole new set of methods that allow it to
interact with the underlying structure.

WebLauncher Framework already includes extensions for tree structures, soap web services and others. 
In this section, we'll cover the basic usage pattern for adding behaviors to models, how to use WebLauncher Framework's built-in behaviors,
and how to create our own.

In essence, Extensions are
`Mixins <http://en.wikipedia.org/wiki/Mixin>`_ with callbacks.

There are a number of Extensions included in WebLauncher Framework. To find out more about each
one, reference the chapters below:

.. include:: /core-libraries/toc-behaviors.rst
    :start-line: 10

Using Extensions
================

Behaviors are attached to models through the ``$extends`` model class
variable::

    class categories extends Base {
        public $extends = array('Tree');
    }

This example shows how a Category model could be managed in a tree
structure using the BaseTree extender. Once a extension has been
specified, use the methods added by the behavior as if they always
existed as part of the original model::

    // get a category
    $this->models->categories->get(1);

    // Use behavior method, children():
    $kids = $this->models->categories->get_children();

Some extensions may require or allow settings to be defined when the
extension is attached to the model. Here, we tell our BaseTree extension
the name of the "parent_id" field in the underlying
database table::

    class categories extends Base {
        public $extends = array('Tree')
        public $parent_id_field='parent_id';
    }

We can also attach several extension to a model. There's no reason
why, for example, our categories model should only behave as a tree,
it may also need internationalization support::

    class categories extends Base {
        public $extends = array(
            'Tree',
            'Translate'
        );
    }

So far we have been adding extensions to models using a model class
variable. That means that our extensions will be attached to our
models throughout the model's lifetime. However, we may need to
"detach" extensions from our models at runtime. Let's say that on
our previous Category model, which is acting as a Tree and a
Translate model, we need for some reason to force it to stop acting
as a Translate model::

    // Detach a extension from our model:
    $this->models->categories->Extensions->unload('Translate');

That will make our categories model stop extending Translate
model from thereon. We may need, instead, to just disable the
Translate extension from acting upon our normal model operations:
our gets, our saves, etc.

Just as we could completely detach a extensions from a model at
runtime, we can also attach new behaviors. Say that our familiar
categories model needs to start extending a Christmas model, but
only on Christmas day::

    // If today is Dec 25
    if (date('m/d') === '12/25') {
        // Our model needs to behave as a Christmas model
        $this->models->categories->extend('Christmas');
    }

.. meta::
    :title lang=en: Extensions
    :keywords lang=en: tree manipulation,manipulation methods,model behaviors,access control list,model class,tree structures,php class,business contract,class category,database table,bakery,inheritance,functionality,interaction,logic,WebLauncher Framework,models,essence
