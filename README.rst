Currently supported components:

- faf
- retrace-server

Component specific how-to
-------------------------

faf
~~~

Using Vagrant
=============

Simplest way to get a faf instance running is:

- ``git clone https://github.com/abrt/abrt-ansible.git``
- ``cd abrt-ansible``
- ``./fetch_remote_roles``
- ``vagrant up``

This will create a Fedora virtual machine using
libvirt backend and provision it using Ansible
in similar way as described in the next section.

Provisioning with Ansible
================================

Following steps can be used to deploy and configure faf instance:

- create a virtual machine (either Fedora or EL)
- edit ``inventories/hosts`` to use hostname or IP address of your testing machine
- use ``ssh-copy-id`` to copy correct ssh key to the testing machine's root account
  (there's a ``private_key_file`` configuration option in ``conf/config`` which
  specifies a private key file ansible uses)
- run ``./run --extra-vars="faf_first_time_setup=true"``
  this will ensure that the PostgreSQL database is created and populated with minimal
  data required by faf
- point your browser to the hostname or IP address of your testing machine to verify the installation
- proceed with further configuration of your new instance, for all available configuration options
  see ``group_vars/all`` file.
- it's recommended to use ``host_vars/<domain>`` to set configuration options for your machines.

Running database migrations:

- ``./run --extra-vars="faf_migrate_db=true"``
