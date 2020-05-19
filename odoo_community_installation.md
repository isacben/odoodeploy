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

## Install Odoo

Still with ubuntu user, create the odoo-current directory:

    $ sudo mkdir /opt/odoo
    $ sudo mkdir /opt/odoo/current
    $ sudo chown -R ubuntu:ubuntu /opt/odoo
    $ sudo chown -R ubuntu:ubuntu /opt/odoo/current/
    $ cd /opt/odoo/current

Clone the Community edition:

    $ git clone https://github.com/odoo/odoo.git



