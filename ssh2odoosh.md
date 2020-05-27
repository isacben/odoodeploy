# How to connect to Odoo.sh via SSH

*This procedure is for Linux.*

## In your local environment (laptop)

First generate a pair of privet and public keys:

    $ ssh-keygen -t rsa -b 4096 -C "email@example.com"

You can save the key in the user's home:

    /home/isacben/.ssh/id_rsa

And you can either set a passphrase or leave it black.

The keys will be saved in the following files:

    /home/isacben/.ssh/id_rsa.
    /home/isacben/.ssh/id_rsa.pub.

Add your SSH key to the ssh-agent:

    $ eval "$(ssh-agent -s)"
    $ ssh-add ~/.ssh/id_rsa

Now, copy the public key. You can see the content like this:

    $ cat /home/isacben/.ssh/id_rsa.pub

## In Odoo.sh

Now, put the public key in the Odoo.sh container.

Create the following directory:

    $ mkdir -p ~/.ssh

Go to that directory and create the following file:

    $ vi authorized_keys

Paste the contents of the public key and save the file.

## Connect to the Odoo.sh container

Now you can connect to the Staging or Production containers. For example:

    ssh <user>@<sub-domain>.odoo.com

You can get the user and host from the Odoo.sh project.
