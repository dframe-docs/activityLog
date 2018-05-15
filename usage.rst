Simple logs
====

The simplest log is action log. He has not any parms. The only one is that the user has refreshed the page.

First we need an interpreter, that we include in file **app/Libs/Extensions/ActivityLog/Action.php**

.. code-block:: php

 namespace Libs\Extensions\ActivityLog;

 class Action
 {

     public function __construct()
     {
         return $this;
     }

 }


Next, we can write first log.
 
.. code-block:: php

 $this->activity->log('Refresh Page')->entity('\Libs\Extensions\ActivityLog\Action'))->push();


Logs with parms
====

Now, try to make a log with some parms. However before begin, we have to have appropriate Interpreter.

.. code-block:: php

 namespace Libs\Extensions\ActivityLog;

 class Change
 {

     public function interpreter($key)
     {
         $this->interpreter = array(
             'users' => array('id', 'firstname', 'lastname')
         );
 
         return $this->interpreter[$key];
     }

     public function build($before, $after)
     {

         if (!empty(array_diff_key($before, $after))) {
             throw new \Exception("Keys in array MUST be same", 1);
         }
 
         foreach ($after as $key => $value) {
             if ($before[$key] == $value) {
                 unset($before[$key]);
                 unset($after[$key]);
             }
         }
         
         $this->changes = array('before' => $before, 'after' => $after);
         return $this;
     }

 }

Foregoing interpreter is able to logs 3 parms (id, firstname and lastname). It is important to read if we want to log more informations, just put more parms.
 
.. code-block:: php
 
 $before = array(
     'firstname' => 'Before Change'
 );
  
 $after = array(
     'firstname' => 'After Change'
 );
  
 $dataId = '1';
 $this->activity->log('Update Data')->entity('\Libs\Extensions\ActivityLog\Change', array($before, $after))->on('data.id', $dataId)->push();


