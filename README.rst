Ansible recipes for configuring and deploying ABRT stack
========================================================

Currently supported:

- faf

Component specific how-to
-------------------------

faf
~~~

Following steps can be used to deploy and configure faf instance:

- create a virtual machine (either Fedora or EL)
- go to `faf/` directory
- edit `inventories/devel_hosts` to use hostname or IP address of your testing machine
- use `ssh-copy-id` to copy correct ssh key to the testing machine's root account
  (there's a `private_key_file` configuration option in `conf/devel_config` which
  specifies a private key file ansible uses)
- edit `group_vars/devel` and uncomment `first_time_setup`,
  this will ensure that the PostgreSQL database is created and populated with minimal
  data required by faf
- run `./devel`
- point your browser to the hostname or IP address of your testing machine to verify the installation
- if the installation succeeded edit `group_vars/devel` and disable `first_time_setup`
- proceed with further configuration of your new instance, for all available configuration options
  see `group_vars/all` file.

Following steps can be repeated for setting up `staging` and/or `prod` instances.
