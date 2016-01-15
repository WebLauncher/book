Retrieving Your Data
####################

As stated before, one of the roles of the Model layer is to get data from multiple types of storage.
The WebLauncher Framework Model class comes with some functions that will help you search for this data, sort it,
paginate it, and filter it. The most common function you will use in models is :php:meth:`Model::get_all()`

.. _model-get_all:

get_all
=======

:php:meth:`get_all($from='',$to='',$order='',$order_direction='',$condition='',$calculate_rows=false)`

Function ``get_all`` is used to retrieve multiple rows from the databse.

$from, $to is for configuring LIMIT for the query used.
$order, $order_direction is for configuring order of rows retieved (array can be passed also for multiple order and directions)
$condition is the condition to be used for the WHERE part or the query created.
$calculate_rows if it is set to true will calculate the total possible number of rows found using the contition sent without applying LIMIT. The value will be saved in $this->total_rows, where $this is the model object

Example::

	$this->models->example->get_all(0,10,'test','desc','field1=1',true);
	// gets first 10 rows from model example ordered by column test and where field1=1

get_cols
========

:php:meth:`get_cols($cols=array(),$from='',$to='',$order='',$order_direction='',$condition='',$calculate_rows=false)`

Function ``get_colls`` is used to retrieve multiple rows from the databse and select only the culumns required.

$from, $to is for configuring LIMIT for the query used.
$order, $order_direction is for configuring order of rows retieved (array can be passed also for multiple order and directions)
$condition is the condition to be used for the WHERE part or the query created.
$calculate_rows if it is set to true will calculate the total possible number of rows found using the contition sent without applying LIMIT. The value will be saved in $this->total_rows, where $this is the model object

.. _model-get:

get
===

:php:meth:`get($id='')`

This will return one result or many results if provided an array of ids. This method will return the row with the id given or the rows with the ids given. 

.. _model-count_all:

count_all
=========

:php:meth:`count_all($condition)`

Returns an integer value. This function will count the rows found applying the condition given. 

.. _model-find-all:

get_cond
========

:php:meth:`get_cond($condition)` 

Returns the first found row identified by the condition given.

.. _model-get_field:

get_field
=========

:php:meth:`get_field($id, $field)` 

Returns the field requested for a given row identified by the id given.

.. _model-find-threaded:

get_field_cond
==============

:php:meth:`get_field_cond($field, $cond)` 

Returns the field/column requested for a given row identified by the condition given.

.. _model-find-neighbors:

.. meta::
    :title lang=en: Retrieving Your Data
    :keywords lang=en: upper case character,array model,order array,controller code,retrieval functions,model layer,model methods,model class,model data,data retrieval,field names,workhorse,desc,neighbors,parameters,storage,models
