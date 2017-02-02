# Setting A Linux Server to Host Catalog App

## General Information
1. IP Address
`35.166.190.110`
1. SSH port
`2200`
1. URL to application: http://ec2-35-166-190-110.us-west-2.compute.amazonaws.com/


## List of software and dependencies installed
1. LAMP (Linux, Apache, MySQL, Python)
	1. Apache - `sudo apt-get install apache2`
	1. mod_wsgi and python-setuptools helper package - `sudo apt-get install python-setuptools libapache2-mod-wsgi`
	1. PostgreSQL - `sudo apt-get install postgresql`
	1. Python (2.7.6) - automatically installed
1. python pip -  `sudo apt-get install python-pip`
1. Git - `sudo apt-get install git-all`
1. virtualenv to keep the application and its dependencies isolated from the main system. - `sudo pip install virtualenv`
1. psycopg2 - `pip install -U psycopg2`
1. SQLAlchemy - `pip install Flask-SQLAlchemy`
1. oauth2client - `pip install --upgrade oauth2client`


## Configuration Changed and References used
1. Update software and install LAMP Reference: [Udacity Blog on Installing LAMP](http://blog.udacity.com/2015/03/step-by-step-guide-install-lamp-linux-apache-mysql-python-ubuntu.html)
1. Initial set up of server to disable root login, create user `grader` with `sudo` permission and change `ssh` port from 22 to 2200. Reference: [Digital Ocean](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-12-04)
1. Configured local timezone to UTC - Reference: [Ubuntu Time](https://help.ubuntu.com/community/UbuntuTime#Using_the_Command_Line_.28terminal.29)
1. Created authorized keys at `/home/grader/.ssh`. Reference: [Udacity Forum](https://discussions.udacity.com/t/permission-denied-publickey-after-adding-grader-user-and-changing-ssh-port/207087/7)
1. Changed owner and give permission to `grader` to access public key for ssh:
	1. `chown grader:grader /home/grader/.ssh`
	1. `chmod 700 /home/grader/.ssh`
	1. `chown grader:grader /home/grader/.ssh/authorized_keys`
	1. `chmod 600 /home/grader/.ssh/authorized_keys`
1. Configured the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)
1. Set up Flask App - Reference: [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps)
1. Set up and secure PostgreSQL: create user `catalog` and prevent remote login. Reference: [Digital Ocean](https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps)
1. Set up PostgreSQL with Flask - Reference: [Kill The Yak](http://killtheyak.com/use-postgresql-with-django-flask/)

## Further Notes
1. May need to specify full path of the `client_secrets.json` file when using `json.loads()` to read it.
1. Use the command `sudo tail /var/log/apache2/error.log` to read the latest error log (very useful!)