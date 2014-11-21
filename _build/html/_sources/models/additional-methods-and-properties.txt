Additional Methods and Properties
#################################

While WebLauncher Framework's model functions should get you where you need to
go, don't forget that model classes are just that: classes that
allow you to write your own methods or define your own properties.

Any operation that handles the saving and fetching of data is best
housed in your model classes. This concept is often referred to as
the fat model.

::

    class example extends Base {
        public function getRecent() {            
            return $this->get_all(1,5,'datetime','desc');
        }
    }

This ``getRecent()`` method can now be used within the controller.

::

    $recent = $this->models->example->getRecent();

:php:meth:`Model::join($table,$condition,$type='left')`
=================================

Joins the current model with another model

    $result = $this->models->example->join('example1','example.id=exampl1.id','left')->get_all();
    

:php:meth:`Model::query(string $query_to_prepare = '', array $args = array())`
=============================================================================

Executes a query prepared to escape the values given using PDO drivers.

:php:meth:`Model::exists($field_or_id, $value = null) `
==============================

Returns true if a record with the particular ID exists::
	
	$this->models->example->exists(1);
	
Returns true if a record with a particular field and value exists::
	
	$this->models->example->exists('id',1);

You can provide more fields and values as long as the number of fields are values are the same::

	$this->models->example(array('field1'=>'value1','field2'=>'value2')

Returns the number of rows affected by the last query.

:php:meth:`Model::get($id)`
===========================================

Returns the record as associative array with the given id::

	$this->models->example->get(1); // returns a record from the example table in DB
	
You can also get the all the records with the ID in an array of ids::

	$this->example->get(array(1,2,3)); // returns a list of example records from DB

:php:meth:`Model::last_id()`
================================

Returns the ID of the last record this model inserted.

.. meta::
    :title lang=en: Additional Methods and Properties
    :keywords lang=en: model classes,model functions,model class,interval,array
