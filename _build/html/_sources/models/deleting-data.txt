Deleting Data
#############

WebLauncher Framework's Model class offers a few ways to delete records from your database. Thought this is not a recommended action
in real projects( you should use a deleted flag in the table) we offer this functionality as described below.

.. _model-delete:

delete
======

``delete(integer $id, boolean $callbacks=true);``

Deletes the record identified by $id::

  $this->models->posts->delete(1);
  // deletes post with id=1

This method has some callback which you can customize with hoocks ``before_delete()`` and ``after_delete()``.

.. _model-delete_cond:

delete_cond
===========

``delete_cond(mixed $condition)``

Delete records identified by the given condition::

	$this->models->posts->delete_cond('title="Old Title"');

.. meta::
    :title lang=en: Deleting Data
    :keywords lang=en: doc models,custom logic,callback methods,model class,database model,callbacks,information model,request data,deleteall,fragment,leverage,array,WebLauncher Framework,failure,recipes,benefit,delete,data model
