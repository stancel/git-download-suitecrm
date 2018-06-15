git-download-suitecrm
=========

Ansible role that downloads and installs a chosen release of SuiteCRM to the default document root for the Apache webserver.

Requirements
------------

Need to have a Debian based Linux (Ubuntu, Debian, etc.) setup with MySQL and Apache already setup and configured on the same server. This role uses the default `/var/www/html` document root path to install the SuiteCRM software. 

Role Variables
--------------

Choose the git tagged release that you would like to download and install. No default value set.
```
	tagged_release_version: "v7.10.6"
```
The default git repo to use when downloading and installing SuiteCRM. This is the default but can be changed if you have a forked/modified git repo that you would prefer to use.
```
	git_repo: "https://github.com/salesagility/SuiteCRM.git"
```
If you are using your own forked repo an want to use a branch instead of a tagged release then fill in a value and comment out the "tagged_release_version" variable 
```
	git_branch: "my-super-special-branch"
```
The database to create when setting up SuiteCRM. The default value is "suitecrm".
```
	db_name: "suitecrm"
```
The DB user to create when to be used by the SuiteCRM application. No default value set.
```
	db_user: "suitecrmDbUser"
```
The password for the DB user being created. o default value set.
```
	db_password: "some-really-secure-password"
```
The root password for your MySQL, MariaDB or Percona Server DB instance to create the DB and user.
```
	mysql_root_password: "your MySQL root password"
```

Dependencies
------------

	- stancel.apache-webserver

Example Playbook
----------------

	- hosts: your_new_crm_server
	  vars_files:
	    - vars/main.yml
	  roles:
	    - { role: stancel.git-download-suitecrm }


or 


	- hosts: your_new_crm_server 
	  vars:
		tagged_release_version: "v7.10.6"
		db_user: "suitecrmDbUser"
		db_password: "some-really-secure-password"
		mysql_root_password: "your MySQL root password"
	  roles:
	    - { role: stancel.git-download-suitecrm }

License
-------

GPLv3

Author Information
------------------

Brad Stancel
