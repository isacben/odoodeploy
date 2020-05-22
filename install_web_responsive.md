# Make Odoo Community Mobile Friendly

We will install the *web* repository from OCA, which has the *web_responsive* module.

Move to the *current* directory.

    $ cd /opt/odoo/current

Clone the repository

    $ git clone -b 13.0 https://github.com/OCA/web.git

Add the repository path to the addons parameter in the odoo.conf file

    $ sudo vi /etc/odoo.conf

Modify the following line to add the path to *'web'*:

    addons_path = /opt/odoo/current/odoo/addons,/opt/odoo/current/web

Restart odoo:

    $ sudo systemctl status odoo

In odoo, go to Settings > Activate developer mode.

Go to Apps, and Update the list of applications.

Look for the web responsive module and install it.
