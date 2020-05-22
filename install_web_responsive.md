# Make Odoo Community Mobile Friendly

We will install the *'web'* repository from OCA, which has the *web_responsive* module.

1. Move to the *'current'* directory

    $ cd /opt/odoo/current

2. Clone the repository

    $ git clone -b 13.0 https://github.com/OCA/web.git

3. Add the repository path to the addons parameter in the odoo.conf file

    $ sudo vi /etc/odoo.conf

4. Modify the following line to add the path to *'web'*:

    addons_path = /opt/odoo/current/odoo/addons,/opt/odoo/current/web

5. Restart odoo:

    $ sudo systemctl status odoo

6. In odoo, go to Settings > Activate developer mode.

7. Go to Apps, and Update the list of applications.

8. Look for the web responsive module and install it.
