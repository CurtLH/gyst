SSH Config
==========

Using a :code:`.ssh/config` file, you store IP addresses for remote machines that you regularily connect to.

https://linuxize.com/post/using-the-ssh-config-file/

.. code-block::

  Host aws-dev
          HostName dev.example.com
          User ec2-user
          IdentityFile ~/.ssh/key.pem

  Host aws-bastion
          User ec2-user
          Hostname bastion.example.com
          Localforward 5432 db.rds.amazonaws.com:5432
          IdentityFile ~/.ssh/key.pem
