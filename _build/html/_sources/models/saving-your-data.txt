Saving Your Data
################

WebLauncher Framework makes saving model data a snap. Data ready to be saved
should be passed to the model's ``save()`` method using the
following basic format::

    Array
    (
        [fieldname1] => 'value',
        [fieldname2] => 'value'
    )

Here's a quick example of a controller action that uses a WebLauncher Framework
model to save data to a database table::

    public function edit($id) {
        if(isset($_POST['id'])){
            $data=array();
            $data['id']=$_POST['id'];
            $data['title']=$_POST['title'];
            $data['content']=$_POST['content'];
            $id=$this->models->posts->save($data);
        }

        // If no form data, find the post to be edited
        // and hand it to the view.
        $this->assign('post', $this->models->posts->get($id));
    }

When save is called the function will execute ``insert()`` or ``update()`` depending if the id is passed in thee $data array.

There are a few other save-related methods in the model that you'll
find useful:

:php:meth:`Model::insert($data, $callbacks=true)`
=================================================

``Model::insert()`` can be used to specifically insert data into the table linked to the model::

    $data=array(
        'title'=>'Testing',
        'content'=>'content of the post');
    $post_id=$this->models->posts->insert($data);

:php:meth:`Model::insert_multiple($fields, $params)`
====================================================

``Model::insert_multiple()`` can be used to specifically insert multiple data rows into the table linked to the model::

    $fields=array('title','content');
    // this are the collumns to be inserted
    
    $data=array();
    $data[]=array(
        'title'=>'Testing',
        'content'=>'content of the post 1');
    $data[]=array(
        'title'=>'Testing 1',
        'content'=>'content of the post 2');
    $this->models->posts->insert_multiple($fields,$data);

This method is only recommended if you don't need the last inserted id of the rows inserted. Otherwise please use ``insert()``.


:php:meth:`Model::update($data,$condition='', $callbacks=true)`
===============================================================

``Model::update()`` can be used to specifically update data from the table linked to the model::

    $id=1;
    $data=array(
        'title'=>'Testing',
        'content'=>'content of the post');
    $post_id=$this->models->posts->update($data,'id='.$id);
    // by using a different condition you can update more than one row from the table

You can also provide the id directly in the data array like this, then no condition is required::

    $data=array(
        'id'=>1,
        'title'=>'Testing',
        'content'=>'content of the post');
    $post_id=$this->models->posts->update($data);

:php:meth:`Model::update_field($id, $field, $value)`
====================================================

``Model::update_field()`` can be used to specifically update a certain field in a row(s) with the given id(s)::

    $this->models->posts->update_field(1,'title','New Title');
    // this will update the post with id =1 title to the new value

    $this->models->posts->update_field(array(1,2),'title','New Title');
    // this will update the post with id=1 and post with id=2 title to the new value

:php:meth:`Model::update_field_cond($field, $value, $condition)`
================================================================

``Model::update_field_cond()`` can be used to specifically update a certain field in a row(s) found with the given condition::

    $this->models->posts->update_field_cond('title','New Title','title="Old Title"');
    // this will update the post with title="Old Title" title to the new value


.. meta::
    :title lang=en: Saving Your Data
    :keywords lang=en: doc models,validation rules,data validation,flash message,null model,table php,request data,php class,model data,database table,array,recipes,success,reason,snap,data model

