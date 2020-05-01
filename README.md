# irods-sandbox

Travis (.com) dev branch:
[![Build Status](https://travis-ci.com/githubfoam/lustre-sandbox.svg?branch=irods)](https://travis-ci.com/githubfoam/irods-sandbox)  

~~~~

KVM/Installation
https://help.ubuntu.com/community/KVM/Installation


~~~~

vagrant@vg-mgmt01 ~]$ history
    sudo yum update -y; sudo yum upgrade -y; sudo shutdown -r now
    3  sudo yum install postgresql-server -y
    4  sudo service postgresql initdb
    5  ls /var/lib/pgsql/data/pg_hba.conf
    6  sudo ls /var/lib/pgsql/data/pg_hba.conf
    7  sudo cp /var/lib/pgsql/data/pg_hba.conf /var/lib/pgsql/data/pg_hba.conf.bck
    8  sudo vi /var/lib/pgsql/data/pg_hba.conf
    9  sudo service postgresql start
   10  sudo su - postgres
   11  sudo adduser irodsrunner
   12  sudo chown -R irodsrunner:irodsrunner /var/lib/irods
   13  ls /etc/irods
   14  ls /etc/var/lib/irods
   15  export RENCI='ftp.renci.org/pub/irods/releases'
   16  wget ftp://$RENCI/4.1.10/centos7/irods-icat-4.1.10-centos7-x86_64.rpm
   17  sudo yum install -y wget
   18  sudo rpm --import https://packages.irods.org/irods-signing-key.asc
   19  wget -qO - https://packages.irods.org/renci-irods.yum.repo | sudo tee /etc/yum.repos.d/renci-irods.yum.repo
   20  sudo yum install epel-release
   21  sudo yum install irods-server irods-database-plugin-postgres
   22  history
   23  ls -l /var/lib/irods/iRODS/Vault
   24  ls /var/lib/irods/
   25  sudo python /var/lib/irods/scripts/setup_irods.py
   26  sudo iinit
   27  iinit
   28  sudo iinit
   29  iinit
   30  echo "Hello world" > test.txt
   31  cat test.txt
   32  iput -K test.txt
   33  ils -L test.txt
   34  history
   35  exit
   36  history

   https://github.com/EUDAT-Training/B2SAFE-B2STAGE-Training/blob/master/ExampleTrainings/iRODS-SysAdmin-Training/iRODS-CentOS-install.md
