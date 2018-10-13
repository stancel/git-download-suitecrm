git-download-suitecrm
=========

Ansible role that downloads and installs a chosen release of SuiteCRM. 

Requirements
------------

Need to already have MySQL / MariaDB / Percona Server and your webserver (Apache or Nginx) already setup and configured. The defaults assume a Debian based Linux (Ubuntu, Debian, etc.) with a default webserver document root of `/var/www/html` to install the SuiteCRM software. You can override those default variables if that is not the case.

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
If you are using your own forked repo an want to use a branch instead of a tagged release then fill in a value and comment out the `tagged_release_version` variable. Default value is an empty string "".  
 
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
The password for the DB user being created. No default value set.

```
	db_password: "some-really-secure-password"
```
The root password for your MySQL, MariaDB or Percona Server DB instance to create the DB and user.

```
	mysql_root_password: "your MySQL root password"
```
The Document Root or file path where the files will be stored and served up by your webserver. The default path is `/var/www/html` and assumes you are running Apache2 on Debian or Ubuntu.

First part => *web_files_path:* is the root directory of your webserver

Second part =>  *web_directory_for_suitecrm:* is the suiteCRM directory inside the root directory

!Be aware of the starting / !

```
    web_files_path: "/var/www"
    web_directory_for_suitecrm: "/html"
```
The linux username used by your webserver. The default value is `www-data` which assumes Apache is used on a Debian or Ubuntu linux.

```
	web_user: "www-data"
```
The linux group used by your webserver. The default value is `www-data` which assumes Apache is used on a Debian or Ubuntu linux.

```
	web_group: "www-data"
```

Manage package with apt, you can disable the installation of package
```
	manage_packages: true
```

The php.ini configurations, to allow or not the setting of these items, useful if your server is already setup with different values, default are true```
```
	configure_mysqli_allow_local_infile: true
	configure_memory_limit: true
	configure_post_max_size: true
	configure_upload_max_filesize: true
	configure_max_input_time: true
	configure_max_execution_time: true
```

Install Composer or not, default is true, disable it if you already have composer installed
```
	install_composer: true
```

Is this a "new", "upgrade" or "restore" installation? "new" and "upgrade" installs install files from Git, "restore" skips any git deployments and expect a later role to restore files to the needed directory. Default is "new".
```
	installation_type: "new"
```

Is this instance to be used for a "dev", "qa" or "prod" environment? Only "prod" environments will deploy the SuiteCRM schedulers. Default is "prod".
```
	environment_type: "prod"
```

Dependencies
------------

None

Example Playbook
----------------

Copy and edit *defaults/main.yml* to your *vars/main.yml*

	- hosts: your_new_crm_server
	  vars_files:
	    - vars/main.yml
	  roles:
	    - { role: stancel.git-download-suitecrm }


or just pass the variables in the playbook


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

[Brad Stancel](https://github.com/stancel) 

Contributors
------------------

[Bouteillier Nicolas](https://github.com/nicolas-san)

