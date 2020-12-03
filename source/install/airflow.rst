Airflow
=======

.. code-block::

   conda create --name airflow -c conda-forge airflow-with-postgres
   conda activate airflow


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

    airflow initdb

Start the Airflow Scheduler and Web Server

.. code-block::

   airflow scheduler
   airflow webserver
   
Create the following files to control Airflow using `systemctl`

.. code-block::

   # contents of /etc/systemd/system/airflow-scheduler
   [Unit]
   Description=Airflow scheduler daemon
   After=network.target postgresql.service mysql.service redis.service rabbitmq-server.service
   Wants=postgresql.service mysql.service redis.service rabbitmq-server.service

   [Service]
   Environment=PATH=/home/curtis/miniconda3/envs/airflow/bin:$PATH:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin
   User=curtis
   Group=curtis
   Type=simple
   ExecStart=/home/curtis/miniconda3/envs/airflow/bin/airflow scheduler
   Restart=always
   RestartSec=5s

   [Install]
   WantedBy=multi-user.target

.. code-block:: 

   # contents of /etc/systemd/system/airflow-webserver.service
   [Unit]
   Description=Airflow webserver daemon
   After=network.target postgresql.service mysql.service redis.service rabbitmq-server.service
   Wants=postgresql.service mysql.service redis.service rabbitmq-server.service

   [Service]
   Environment=PATH=/home/curtis/miniconda3/envs/airflow/bin:$PATH:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin
   User=curtis
   Group=curtis
   Type=simple
   ExecStart=/home/curtis/miniconda3/envs/airflow/bin/airflow webserver -p 8085 --pid /home/curtis/airflow/airflow-webserver.pid
   Restart=on-failure
   RestartSec=5s
   PrivateTmp=true

   [Install]
   WantedBy=multi-user.target

Update `systemctl` configuration:

.. code-block::
   
   sudo systemctl daemon-reload
   
Check the status of Airflow

.. code-block:: 

   sudo systemctl status airflow-scheduler
   sudo systemctl status airflow-webserver
