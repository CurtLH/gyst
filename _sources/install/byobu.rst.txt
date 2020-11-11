Byobu
=====

.. code-block::

   sudo apt install byobu

Follow `these directions <https://superuser.com/a/712613>`_ to run byobu whenever you open a new terminal window.

To install :code:`byobu` on an AWS EC2, follow `these direction <https://stackoverflow.com/a/30599606/3420371>`_.

Make sure to add the following to your :code:`.bash_profile`:

.. code-block::

   _byobu_sourced=1 . /usr/bin/byobu-launch
