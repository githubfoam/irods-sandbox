# irods-sandbox

~~~~

sudo yum update -y
sudo yum install postgresql-server -y && sudo service postgresql initdb

sudo cat /var/lib/pgsql/data/pg_hba.conf|grep "host    all             all             127.0.0.1/32            ident"
sudo sed -i 's%host    all             all             127.0.0.1/32            ident%host    all             all             127.0.0.1/32            md5%g' /var/lib/pgsql/data/pg_hba.conf

sudo cat /var/lib/pgsql/data/pg_hba.conf|grep "host    all             all             127.0.0.1/32            md5"


sudo cat /var/lib/pgsql/data/pg_hba.conf|grep "host    all             all             ::1/128                 ident"
sudo sed -i 's%host    all             all             ::1/128                 ident%host    all             all             ::1/128                 md5%g' /var/lib/pgsql/data/pg_hba.conf
sudo cat /var/lib/pgsql/data/pg_hba.conf|grep "host    all             all             ::1/128                 md5"

sudo service postgresql start && sudo service postgresql status

[vagrant@vg-irods01 ~]$ sudo su - postgres
-bash-4.2$ psql
psql (9.2.24)
Type "help" for help.

postgres=# create database "ICAT";
CREATE DATABASE
postgres=# create user irods with password 'irods';
CREATE ROLE
postgres=# grant all privileges on database "ICAT" to irods;
GRANT
postgres=# \q
-bash-4.2$ exit
logout
[vagrant@vg-irods01 ~]$


sudo rpm --import https://packages.irods.org/irods-signing-key.asc
sudo yum install wget -y
wget -qO - https://packages.irods.org/renci-irods.yum.repo | sudo tee /etc/yum.repos.d/renci-irods.yum.repo
sudo yum install epel-release -y && sudo yum install irods-server irods-database-plugin-postgres -y
sudo python /var/lib/irods/scripts/setup_irods.py



[vagrant@vg-irods01 ~]$ sudo python /var/lib/irods/scripts/setup_irods.py
Warning: Hostname `vg-irods01` should be a fully qualified domain name.
Updating /var/lib/irods/VERSION.json...
The iRODS service account name needs to be defined.
iRODS user [irods]:
iRODS group [irods]:

+--------------------------------+
| Setting up the service account |
+--------------------------------+

Creating Service Group: irods
Creating Service Account: irods
Setting owner of /var/lib/irods to irods:irods
Setting owner of /etc/irods to irods:irods
iRODS server's role:
1. provider
2. consumer
Please select a number or choose 0 to enter a new value [1]:
Updating /etc/irods/server_config.json...

+-----------------------------------------+
| Configuring the database communications |
+-----------------------------------------+

You are configuring an iRODS database plugin. The iRODS server cannot be started until its database has been properly configured.

ODBC driver for postgres [PostgreSQL]:
Database server's hostname or IP address [localhost]:
Database server's port [5432]:
Database name [ICAT]:
Database username [irods]:

-------------------------------------------
Database Type: postgres
ODBC Driver:   PostgreSQL
Database Host: localhost
Database Port: 5432
Database Name: ICAT
Database User: irods
-------------------------------------------

Please confirm [yes]: yes
Database password:irods
Updating /etc/irods/server_config.json...
Listing database tables...
Salt for passwords stored in the database:irods
Updating /etc/irods/server_config.json...

+--------------------------------+
| Configuring the server options |
+--------------------------------+

iRODS server's zone name [tempZone]:
iRODS server's port [1247]:
iRODS port range (begin) [20000]:
iRODS port range (end) [20199]:
Control Plane port [1248]:
Schema Validation Base URI (or off) [file:///var/lib/irods/configuration_schemas]:
iRODS server's administrator username [rods]:

-------------------------------------------
Zone name:                  tempZone
iRODS server port:          1247
iRODS port range (begin):   20000
iRODS port range (end):     20199
Control plane port:         1248
Schema validation base URI: file:///var/lib/irods/configuration_schemas
iRODS server administrator: rods
-------------------------------------------

Please confirm [yes]:
iRODS server's zone key:TEMPORARY_zone_key
iRODS server's negotiation key (32 characters):TEMPORARY_32byte_negotiation_key
Control Plane key (32 characters):TEMPORARY__32byte_ctrl_plane_key
Updating /etc/irods/server_config.json...

+-----------------------------------+
| Setting up the client environment |
+-----------------------------------+


iRODS server's administrator password:irods
Updating /var/lib/irods/.irods/irods_environment.json...

+--------------------------+
| Setting up default vault |
+--------------------------+

iRODS Vault directory [/var/lib/irods/Vault]:
+-------------------------+
| Setting up the database |
+-------------------------+

Listing database tables...
Creating database tables...

+-------------------+
| Starting iRODS... |
+-------------------+

Validating [/var/lib/irods/.irods/irods_environment.json]... Success
Validating [/var/lib/irods/VERSION.json]... Success
Validating [/etc/irods/server_config.json]... Success
Validating [/etc/irods/host_access_control_config.json]... Success
Validating [/etc/irods/hosts_config.json]... Success
Ensuring catalog schema is up-to-date...
Updating to schema version 2...
Updating to schema version 3...
Updating to schema version 4...
Updating to schema version 5...
Updating to schema version 6...
Catalog schema is up-to-date.
Starting iRODS server...
Success

+---------------------+
| Attempting test put |
+---------------------+

Putting the test file into iRODS...
Getting the test file from iRODS...
Removing the test file from iRODS...
Success.

+--------------------------------+
| iRODS is installed and running |
+--------------------------------+

[vagrant@vg-irods01 ~]$

test iRODS,login with the irods admin account rods

[vagrant@vg-irods01 ~]$ iinit
 ERROR: environment_properties::capture: missing environment file. should be at [/home/vagrant/.irods/irods_environment.json]
One or more fields in your iRODS environment file (irods_environment.json) are
missing; please enter them.
Enter the host name (DNS) of the server to connect to: 127.0.0.1
Enter the port number: 1247
Enter your irods user name: rods
Enter your irods zone: tempZone
Those values will be added to your environment file (for use by
other iCommands) if the login succeeds.

Enter your current iRODS password:
[vagrant@vg-irods01 ~]$

[vagrant@vg-irods01 ~]$ echo "Hello irods" > test.txt
[vagrant@vg-irods01 ~]$ iput -K test.txt
[vagrant@vg-irods01 ~]$ ils -L test.txt
  rods              0 demoResc           12 2020-05-02.11:38 & test.txt
    sha2:Z/ArRB1MdW0YN2eBK57uakdVKZPirnC7tYezD9R0ULs=    generic    /var/lib/irods/Vault/home/rods/test.txt
[vagrant@vg-irods01 ~]$


~~~~

~~~~

The integrated Rule-Oriented Data System (iRODS) is open source data management software
https://github.com/irods/irods

~~~~
