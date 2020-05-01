Crontab
=======

In order to have :code:`crontab` recognize your environment variables, edit :code:`crontab` and add the following:

.. code-block::

   BASH_ENV="/home/ec2-user/.bashrc"

   * * * * * bash /home/ec2-user/my_script.sh >> /home/ec2-user/tmp/cron-log 2>&1


https://unix.stackexchange.com/a/362777/62141
