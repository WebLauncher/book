Callback Methods
################

If you want to sneak in some logic just before or after a WebLauncher Framework
model operation, use model callbacks. These functions can be
defined in model classes. Be sure
to note the expected return values for each of these special
functions.

When using callback methods you should remember that behavior callbacks are
fired **before** model callbacks are.

process_row
===========

``process_row(array $row)``

This method is called for each row retrieved from the database. This is a very important callback that lets you do extra processing on each row retrieved
before actually sending the result of the ``get()``, ``get_cond()`` and ``get_all()`` methods.

As an example you would like to get the user information for each post retrieved from the database::

    function process_row($row){
        $row['user']=$this->models->users->get($row['user_id']);
        return $row;
    }

.. warning::

Please make sure you return the processed ``$row`` variable so that the function may pass the result further.

before_insert
=============

``before_insert(array &$data)``

Called before any insert operation. In ``$data`` is the reference to the data that needs to be inserted.
This callback can be used for doing some extra processing before each insert.

For example when inserting a post you would like the title to be striped from any html tags::

    function before_insert($data){
        $data['title']=strip_tags($data['title']);
    }

after_insert
============

``after_insert(array $data)``

Use this callback to do aditional processing or data insertions after a record has been inserted into DB using this model.

As an example after each post insertions you would like to increase a value ``no_posts`` in the users profile::

    function after_insert($data){
        $current_user_id=1;
        $current_user=$this->models->users->get($current_user_id);
        $this->models->users->update_field($current_user_id,'no_posts',$current_user['no_posts']++);
    }

before_update
=============

``before_update(array &$data, &$condition)``

This callback can be used to do some processing on the $data and $condition before each ``update()`` call.

after_update
============

``after_update(array $data, $condition)``

This method is called after any ``update()`` call. Can be used to do some extra updates on other models when an update happens on the current model.

before_delete
=============

``before_delete(integer &$id)``

This method is called before any ``delete()`` call. Can be used to do extra delete actions before the actual model delete call.

after_delete
=============

``after_delete(integer $id)``

This method is called after any ``delete()`` call. Can be used to do extra delete actions after the actual model delete call.

.. meta::
    :title lang=en: Callback Methods
    :keywords lang=en: querydata,query conditions,model classes,callback methods,special functions,return values,counterparts,array,logic,decisions
