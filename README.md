Setting up a music server
========================

Description
-----------

Setting up a Music Server on a Single Board Computer (SBC) like raspberry pi or odroid c2.
The Music Server runs mopidy as Backend Server and rompr as Frontend.
Alternative frontends can be used. (Iris, ncmpcpp ...)
Services are run in docker container.
These scripts prepare the SBCs.

Prerequisites
-------------

Ansible is needed on your workstation.
Best setup in a virtual python environment.
https://virtualenvwrapper.readthedocs.io/en/latest/

Scripts are tested on a fresh install of rasbian and a minimal ubuntu image for the odroid.
Other then that not much testing has been done yet.

Configuration
------------

Edit the file set_env.sh and run

   source set_env.sh

Setup ssh
---------

From your workstation copy ssh credentials to the server.

   ssh-copy-id <user>@<ip-address>

If a host is reinstalled and has a different key in ‘known_hosts’, this will result in an error message until corrected. If a host is not initially in ‘known_hosts’ this will result in prompting for confirmation of the key, which results in an interactive experience if using Ansible, from say, cron. You might not want this.

If you understand the implications and wish to disable this behavior, you can do so by editing /etc/ansible/ansible.cfg or ~/.ansible.cfg:

[defaults]
host_key_checking = False
Alternatively this can be set by the ANSIBLE_HOST_KEY_CHECKING environment variable:

$ export ANSIBLE_HOST_KEY_CHECKING=False

You can also insert this in the configuration file set_env.sh.

Running the playbooks
---------------------

Edit the host file to for ip and user of the server to be installed.

There are playbooks for
 - rasbian
 - odroid
 - hummingboard (cuby)

Playbooks can be edited for soundcards etc.

Run the playbok

  ansible-playbook -i hosts  odroid_headless.yml 

THats all.
