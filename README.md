Ansible role for Jetty installation
=========

Installs Jetty web-server from tarball.

It's inspired by [puppet-jetty](https://github.com/maestrodev/puppet-jetty) module and tries to do the same things but for Ansible.

Role Variables
--------------

* `jetty_version`

  Version of Jetty that will be installed. (Default is `9.2.3.v20140905`.)

* `jetty_host`

  What host to listen on. By default it listens on all interfaces.

* `jetty_port`

  HTTP port to listen on. By default it listens on port `8080`.

* `jetty_src_dir`

  Directory where tarball will be saved after downloading. (Default is `/usr/src`.)

* `jetty_dst_dir`

  Directory where Jetty distribution will be extracted. (Default is `/opt`.)

* `jetty_java_options`

  Extra options for Java.

* `jetty_user_create`

  Whether to create system account for Jetty or not. (Default is `true`.)

* `jetty_user_login`

  User name under which Jetty will run. (Default is `jetty`.)

* `jetty_user_homedir`

  Home directory of Jetty user. Used only when `jetty_user_create` is `true`. (Default is `/opt/jetty`.)

* `jetty_group_create`

  Whether to create group account for Jetty or not. (Default is `true`.)

* `jetty_group_name`

  Group name under which Jetty will be run. (Default is `jetty`.)

Actions role
------------

* downloads Jetty's distribution to `jetty_src_dir`
* creates user/group if enabled
* unpacks distribution to `jetty_dst_dir` and sets owner
* creates symlink (`jetty_dst_dir`/jetty) to distribution directory
* creates symlink (`/var/log/jetty`) to directory with log files
* creates init script (`/etc/init.d/jetty`)
* creates configuration file (`/etc/default/jetty`)
* runs Jetty
* adds Jetty to start on boot

How to install
--------------

    ansible-galaxy install php-coder.jetty

For more installation's options/variants read the documentation: http://docs.ansible.com/galaxy.html

Dependencies
------------

* [php-coder.oraclejdk](https://galaxy.ansible.com/list#/roles/2093)

Example Playbook
----------------

Example of usage with default parameters:

    - hosts: all
      roles:
         - php-coder.jetty

Example of usage with custom host/port and Java options:

    - hosts: all
      roles:
         - {
             role: php-coder.jetty,
             jetty_host: '127.0.0.1',
             jetty_port: 9090,
             jetty_java_options: '-XX:+UseCompressedOops -Dsun.rmi.dgc.client.gcInterval=86400000 -Dsun.rmi.dgc.server.gcInterval=86400000',
           }


Example of usage with existing user and group:

    - hosts: all
      roles:
         - {
             role: php-coder.jetty,
             jetty_user_create: false,
             jetty_user_login: 'www-data',
             jetty_group_create: false,
             jetty_group_name: 'www-data'
           }

License
-------

GPLv2

Author Information
------------------

Slava Semushin (slava.semushin@gmail.com)
