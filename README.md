# maxscale_sandbox
Some quick scripts to allow me to create a sandbox environment with MaxScale and several MySQL servers.

# Requirements:

Currently this is a very basic set of scripts and assumes that [MaxScale](https://mariadb.com/products/mariadb-maxscale) is going to be connected to a MySQL Sandbox setup.
The following assumptions are being made:
* Runs on CentOS 6/RHEL 6
* MaxScale installed rpm is v1.2.0 (and the init scripts need patching)
* [MySQL Sandbox](http://mysqlsandbox.net/) is installed
* The replication topology is a master and two slaves with one of the slaves replicating from MaxScale which in turn replicates from the master.
* MySQL Sandbox usually makes the MySQL servers listen to 127.0.0.1 on different ports. This script changes the listener address to the host's main ip. This is intended to make it possible to locate MaxScale on a different server (reachable by ssh) from the MySQL servers.
* The MySQL sandboxes are located at `$HOME/sandboxes`.
* The MaxScale binlogdir is located at `/maxscale/maxscale`.
* You need to download a MySQL 5.6 tarball such as `mysql-5.6.26-linux-glibc2.5-x86_64.tar.gz` for the sandbox to build from.

Many of these limitations are artificial and may be removed as time permits. Patches welcome.

# Usage:

Setup:
```
$ ./create_maxscale_sandbox /path/to/mysql-5.6.26-linux-glibc2.5-x86_64.tar.gz
Cleanup:
$ ./remove_maxscale_sandbox
```

# Binaries:
* `big_transaction - simple script to generate a "big" transaction for testing transaction safety.
* `check_slaves_running` - exit status 0 if the slaves are all running
* `check_slaves` - wrapper to $HOME/sandboxes/maxscale/check_slaves
* `create_maxscale_sandbox` - create a sandbox environment of MySQL master and 2 slaves with slave 2 replication from MaxScale and MaxScale replicating from the master
* `maxscale_show_slave_status` - run SHOW SLAVE STATUS on maxscale
* `maxscale_sql` - SQL connection to MaxScale binlog router port
* `my_ipaddress` - return my ip address
* `remove_maxscale_sandbox` - removes the MySQL sandboxes and stops MaxScale

