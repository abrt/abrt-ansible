Currently supported components:

- faf

Component specific how-to
-------------------------

faf
~~~

Following steps can be used to deploy and configure faf instance:

- create a virtual machine (either Fedora or EL)
- go to ``faf/`` directory
- edit ``inventories/hosts`` to use hostname or IP address of your testing machine
- use ``ssh-copy-id`` to copy correct ssh key to the testing machine's root account
  (there's a ``private_key_file`` configuration option in ``conf/config`` which
  specifies a private key file ansible uses)
- run ``./run --extra-vars="first_time_setup=true"``
  this will ensure that the PostgreSQL database is created and populated with minimal
  data required by faf
- point your browser to the hostname or IP address of your testing machine to verify the installation
- proceed with further configuration of your new instance, for all available configuration options
  see ``group_vars/all`` file.

Running database migrations:

- ``./run --extra-vars="migrate_db=true"``
