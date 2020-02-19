Airflow
=======

.. code-block::

   $ conda create --name airflow -c conda-forge airflow-with-postgres
   $ conda activate airflow


Follow `these directions <https://vujade.co/install-apache-airflow-ubuntu-18-04/>`_ to create a new user and database for airflow. In my situation, I named both the user and the database "airflow".

Make the following changes to `~/airflow/airflow.cfg`:

.. code-block::

   sql_alchemy_conn = postgresql+psycopg2://airflow@localhost:5432/airflow
   broker_url = amqp://airflow@localhost:5672//
   result_backend = amqp://airflow@localhost:5672//

Add the following line to your `.bashrc` file:


.. code-block::

    export AIRFLOW_HOME=~/airflow

Initalize the Airflow database for the first time

.. code-block::

    $ airflow initdb

Start the Airflow Scheduler and Web Server

.. code-block::

   $ airflow scheduler
   $ airflow webserver
