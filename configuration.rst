Saving logs
^^^^^^^^^^

Activity logs can be use arbitrary. Datas that could be save are loosely. Thanks to picking to logns, you can easily make new interpreter that can read him in certain way.
Below are examples of using.

We have to define using of Activity log. Here we make it in abstract controller.

.. code-block:: php

 namespace Controller;

 use Dframe\ActivityLog\Activity;

 abstract class Controller extends \Dframe\Controller
 {
     public function start()
     {   

         /** 
          * @param Object $driver
          * @param Int $loggedId
          */
         $this->activity = new Activity($this->loadModel('ActivityLog/Drivers/Log'), $this->baseClass->session->get('id', 0));
     }

First parm is responsible for connecting in example with MySQL that we should include in Model folder. Here you can find the code https://github.com/dframe/activityLog/blob/master/example/app/Model/ActivityLog/Drivers/Log.php
As $loggedId we use user id.
