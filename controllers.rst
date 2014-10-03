Controllers
###########

Controllers are the 'C' in MVC. After routing has been applied and the correct
controller has been found, your controller's action is called. Your controller
should handle interpreting the request data, making sure the correct models
are called, and the right response or view is rendered. Controllers can be
thought of as middle man between the Model and View. You want to keep your
controllers thin, and your models fat. This will help you more easily reuse
your code and makes your code easier to test.

Commonly, a controller is used to manage the logic around a single model. For
example, if you were building a blog, you might have a
``posts_page`` controller managing your posts and an ``category_page`` managing your
categories. However, it's also possible to have controllers work with more than
one model. To keep the code clean you should name the controller according to the name 
of the primary model it handles.

Your application's controllers extend the ``Page`` class, which in turn
extends the core :php:class:`_Page` class.

Controllers provide a number of methods that handle requests. These are called
*actions*. By default, each public method which starts with ``action_`` in
a controller is an action, and is accessible from a URL. An action is responsible
for interpreting the request and creating the response. Usually responses are
in the form of a rendered view, but there are other ways to create responses as
well.

The 'Page' Controller
=====================

As stated in the introduction, the ``Page`` class is the
parent class to all of your application's controllers.
``Page`` itself extends the :php:class:`_Page` class included in the
WebLauncher core library. 

Controller attributes and methods created in your ``Page``
will be available to all of your application's controllers.

While normal object-oriented inheritance rules apply, WebLauncher
does a bit of extra work when it comes to special controller
attributes. The components and helpers used by a
controller are treated specially. In these cases, ``Page``
value arrays are merged with child controller class arrays. The values in the
child class will always override those in ``Page``.

Request parameters
==================

When a request is made to a WebLauncher application, WebLauncher's uses :ref:`routes-configuration` to find and
create the correct controller. The request data is encapsulated in a request
object. WebLauncher puts all of the important request information into the
``$this->request`` property. See the section on
:ref:`weblauncher-request` for more information on the WebLauncher request object.

Controller actions
==================

Controller actions are responsible for converting the request parameters into a
response for the browser/user making the request. WebLauncher uses conventions to
automate this process and remove some boilerplate code you would otherwise need
to write.

By convention, WebLauncher renders a view with an inflected version of the action
name. Returning to our blog example, our ``posts_page`` might contain the
``action_view()``, ``action_share()``, and ``action_search()`` actions. The controller would be found
in ``/modules/site/components/posts/posts.php`` and contain::

        # /modules/site/components/posts/posts.php

        class posts_page extends Page {
            public function action_view($id) {
                //action logic goes here..
            }

            public function action_share($customerId, $recipeId) {
                //action logic goes here..
            }

            public function action_search($query) {
                //action logic goes here..
            }
        }

The view files for these actions would be ``/modules/site/components/posts/views/view.tpl``,
``/modules/site/components/posts/views/share.tpl``, and ``/modules/site/components/posts/views/search.tpl``. The
conventional view file name is the lowercased and underscored version of the
action name.

Controller actions generally use :php:meth:`~Page::set()` to create a
context that :php:class:`View` uses to render the view. Because of the
conventions that WebLauncher uses, you don't need to create and render the view
manually. Instead, once a controller action has completed, WebLauncher will handle
rendering and delivering the View.

If for some reason you'd like to skip the default behavior, both of the
following techniques will bypass the default view rendering behavior.

* If you return a string, or an object that can be converted to a string from
  your controller action, it will be used as the response body.
* You can return a PHP class object with the completely created
  response that has a __toString() magic method implemented.
* Any array data returned will be json_encode'd.

In order for you to use a controller effectively in your own application, we'll
cover some of the core attributes and methods provided by WebLauncher's controllers.

.. _controller-life-cycle:

Request Life-cycle callbacks
============================

.. php:class:: Controller

WebLauncher controllers come fitted with callbacks you can use to
insert logic around the request life-cycle:

.. php:method:: on_init()

    This function is executed before every action in the controller.
    It's a handy place to check for an active session or inspect user
    permissions.

    .. note::

        The on_init() method will be called for missing actions,
        and scaffolded actions.

.. php:method:: on_load()

    Called after controller action logic, but before the view is
    rendered. This callback is not used often, but may be needed if you
    are calling :php:meth:`~Page::render()` manually before the end of a given action.

.. php:method:: index()

    This function is executed when an action is not provided in the request.

.. _controller-methods:

Controller Methods
==================

For a complete list of controller methods and their descriptions
visit the `WebLauncher API`.

Interacting with Views
----------------------

Controllers interact with views in a number of ways. First, they
are able to pass data to the views, using :php:meth:`~Page::assign()`. You can also
decide which view class to use, and which view file should be
rendered from the controller.

.. php:method:: assign(string $var, mixed $value)

    The :php:meth:`~Controller::assign()` method is the main way to send data from your
    controller to your view. Once you've used :php:meth:`~Page::assign()`, the variable
    can be accessed in your view::

        // First you pass data from the controller:

        $this->assign('color', 'pink');

        // Then, in the view, you can utilize the data:
        ?>

        You have selected <?php echo $color; ?> icing for the cake.

    The :php:meth:`~Controller::assign()` method also takes an associative array as its first
    parameter. This can often be a quick way to assign a set of
    information to the view::

        $data = array(
            'color' => 'pink',
            'type' => 'sugar',
            'base_price' => 23.95
        );

        // make $color, $type, and $base_price
        // available to the view:

        $this->assign($data);

Rendering a specific view
~~~~~~~~~~~~~~~~~~~~~~~~~

In your controller, you may want to render a different view than
the conventional one. You can do this by calling
:php:meth:`~Page::render()` directly. Once you have called :php:meth:`~Page::render()`, WebLauncher
will not try to re-render the view::

    class posts_page extends Page {
        public function action_my_action() {
        	$this->view='custom_file';
        
        	// or
            $this->render('custom_file');
        }
    }

This would render ``/modules/site/components/posts/views/custom_file.tpl`` instead of
``/modules/site/components/posts/views/custom_file.tpl``

Flow Control
------------

.. php:method:: redirect(mixed $url, integer $status, boolean $exit)

    The flow control method you'll use most often is :php:meth:`~Page::redirect()`.
    This method takes its first parameter in the form of a
    WebLauncher-relative URL. When a user has successfully placed an order,
    you might wish to redirect them to a receipt screen.::

        public function action_place_order() {
            // Logic for finalizing order goes here
            if ($success) {
                return $this->redirect(
                    $this->paths['root_module']
                );
            }
        }

    You can also use a relative or absolute URL as the $url argument::

        $this->redirect('/orders/thanks');
        $this->redirect('http://www.example.com');

    The second parameter of :php:meth:`~Page::redirect()` allows you to define an HTTP
    status code to accompany the redirect. You may want to use 301
    (moved permanently) or 303 (see other), depending on the nature of
    the redirect.

    The method will issue an ``exit()`` after the redirect unless you
    set the third parameter to ``false``.

    If you need to redirect to the referer page you can use::

        $this->redirect($this->referer());

Other Useful Methods
--------------------

.. php:method:: add_message(string $type='success', string $message)

    This method saves the message into the session for it to be displayed at the render time. 

.. php:method:: referer()

    Returns the referring URL for the current request. Parameter
    ``$default`` can be used to supply a default URL to use if
    HTTP\_REFERER cannot be read from headers. So, instead of doing
    this::

        class users_page extends Page {
            public function action_delete($id) {
                // delete code goes here, and then...
                if ($this->referer() != '/') {
                    return $this->redirect($this->referer());
                }
                return $this->redirect($this->paths['current']);
            }
        }

.. php:method:: validate(string $form_id)

   Use this method to check the validity of a form id ($form_id). Although most of the forms are automatically checked by
   the internal form validation system sometimes is better to check twice.

.. php:method:: add_validator(string $form_id, string $field_name, string $rule, string $message)

   This method adds a form validator to a given field in a form. Checkout the ``form validation page``.

.. php:method:: mail(string $template, mixed $params=array())

   Send e-mail using EmailManager. Checkout ``sending an e-mail page``.


Controller Attributes
=====================

For a complete list of controller attributes and their descriptions
visit the `WebLauncher API`.

.. php:attr:: title

    Page title

.. php:attr:: view
	
	The view to be used for the current action.
	
.. php:attr:: system
	
	Direct access to System class for helper methods and attributes.
	
.. php:attr:: models

	Direct access to System::models for accesing the models.
	
.. php:attr:: paths

	Direct access to System::paths for using generated URL/Directories paths.
	
.. php:attr:: db

	Direct access to the current DbManager object for executing DB queries.
	
.. php:attr:: user

	Direct access to the current signed in user data as array.
	
.. php:attr:: session
	
	Direct access to the session array. You can also use $_SESSION variable.
	
.. php:attr:: forms

	Direct access to System::forms FormsManager object.
	
.. php:attr:: parent

	Access to the parent component controller class.
	
.. php:attr:: subpage
	
	Access to the child component requested.