Instalation
----------

From console level, launch the command composer* 

.. code-block:: bash

 $ composer require dframe/activitylog

Or download manual https://github.com/dframe/activityLog/releases


Saving logs
----------

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

First parm is responsible for connecting in example with MySQL that we should include in your project folder. Here you can find the code https://github.com/dframe/activityLog/tree/master/demo/app/Drivers 
As $loggedId we use for example user id.
