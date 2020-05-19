# Odoo Community Installation Guide

## Server Preparation

Update first the server.

    $ sudo apt update

### Python

Usally, Python will be present in the server. Check the version to make sure it is compatible with the target version of Odoo Community.

    $ python3 --version
    Python 3.6.5

Odoo v13 requires python 3.6 or 3.7. Python 3.8 is not supported.

Check also that pip3 is installed:

    $ pip3 --version

If pip3 is not install, install it.

    $ sudo apt install python3-pip

### Git

Git should already be installed:

    $ git --version
    git version 2.17.1

If it is not installed, you can install it.

    $ sudo apt install git

### Postgres

Install postgres:

    $ sudo apt install postgresql postgresql-client

Create the postgres user, which has to be called the same as the user that runs odoo, in this case, the ubuntu user.

    $ sudo -u postgres createuser -s $USER

### Wkhtmltopdf

Go back to the tmp directory:

    $ cd /tmp

Install Wkhtmltopdf:

    $ wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb
    $ sudo apt install ./wkhtmltox_0.12.5-1.bionic_amd64.deb

## Install Odoo

Still with ubuntu user, create the odoo-current directory:

    $ sudo mkdir /opt/odoo
    $ sudo mkdir /opt/odoo/current
    $ sudo chown -R ubuntu:ubuntu /opt/odoo
    $ sudo chown -R ubuntu:ubuntu /opt/odoo/current/
    $ cd /opt/odoo/current

Clone the Community edition:

    $ git clone https://github.com/odoo/odoo.git

Create a configuration file:

    $ sudo nano /etc/odoo13.conf

Configure like this:

```
[options]
; This is the password that allows database operations:
admin_passwd = my_admin_passwd
db_host = False
db_port = False
db_user = ubuntu
db_password = False
addons_path = /opt/odoo/current/odoo/addons
```

Install the dependencies:

    $ sudo apt install python3-dev libxml2-dev libxslt1-dev libldap2-dev libsasl2-dev

Go to the installation directory:

    $ cd /opt/odoo/current/odoo

Create a swap file with root user:

    $ sudo -s
    # cd ~
    # dd if=/dev/zero of=tmpswap bs=1024 count=1M
    # chown root:root /home/ubuntu/tmpswap
    # chmod 0600 /home/ubuntu/tmpswap
    # mkswap tmpswap
    # swapon tmpswap

This is the source of this workaround: https://stackoverflow.com/questions/11289002/gcc-cc1-out-of-memory-allocating

Install the dependencies in the requirements:

    $ pip3 install setuptools wheel
    $ pip3 install -r requirements.txt

Test the installation:

    $ python3 odoo-bin -c /etc/odoo.conf

## Create a Systemd Unit File

Create the following file:

    $ sudo nano /etc/systemd/system/odoo.service

Copy this content:

```
[Unit]
Description=Odoo
Requires=postgresql.service
After=network.target postgresql.service

[Service]
Type=simple
SyslogIdentifier=odoo
PermissionsStartOnly=true
User=ubuntu
Group=ubuntu
ExecStart=/usr/bin/python3 /opt/odoo/current/odoo/odoo-bin -c /etc/odoo.conf
StandardOutput=journal+console

[Install]
WantedBy=multi-user.target
```
Run the following commands to start Odoo with ubuntu user:

    $ sudo systemctl daemon-reload
    $ sudo systemctl enable --now odoo
    $ sudo systemctl status odoo
