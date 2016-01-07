Currently supported components:

- faf
- retrace-server

Using Vagrant
=============

Simplest way to get instances of abrt stack running is:

- ``git clone https://github.com/abrt/abrt-ansible.git``
- ``cd abrt-ansible``
- ``./fetch_remote_roles``
- ``vagrant up``

This will create virtual machines using
libvirt backend and provision them using Ansible
in similar way as described in the next section.

By default ``vagrant up`` will create multiple machines
with abrt service running inside.
You can also specify instance to run and provision:

- ``vagrant up faf``
- ``vagrant up rs``


Provisioning with Ansible
================================

Following steps can be used to deploy and configure faf instance:

- create a virtual machine (either Fedora or EL/CentOS)
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


Retrace server
==============

Retrace server provisioning is similar to previous section
except instead of passing ``faf_first_time`` setup to ``extra-vars``
we have to pass ``selinux=false`` as retrace server doesn't support SELinux.

- edit ``inventories/hosts`` and add your machine to ``[retrace_server]`` group
- ensure ssh access via key used by Ansible
- run ``./run --extra-vars="selinux=false"``


Notes
=====

``./run`` wrapper passes parameters to ``ansible-playbook`` so you can
add ``-vvv`` for debugging or limit host selection with::

       -l SUBSET, --limit=SUBSET
                  Further limits the selected host/group patterns.
