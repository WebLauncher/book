Model Attributes
################

Model attributes allow you to set properties that can override the
default model behavior.

table
=====

The ``table`` property is a string that specifies the name of
the database table to use to bind your model class to the
related database table. 

Example usage::

    class Example extends Base {
        public $table = 'example_1';
    }

.. _model-primaryKey:

id_field
========

Each table normally has a primary key, ``id``. You may change which
field name the model uses as its primary key. This is common when
setting WebLauncher Framework to use an existing database table.

Example usage::

    class Example extends Base {
        // example_id is the field name in the database
        public $id_field = 'the_id';
    }

order_field
===========

The collumn in the table that should provide order functionality. (Usually an integer type from 0->)

Default: 'order'

active_field
============

The collumn in the table that should provide if the row is active or not.

process
=======

This tells the model if it should call the `process_row` method. 

.. meta::
    :title lang=en: Model Attributes
    :keywords lang=en: alternate table,default model,database configuration,model example,database table,default database,model class,model behavior,class model,plural form,database connections,database connection,attribute,attributes,complete list,config,WebLauncher Framework,api,class example
