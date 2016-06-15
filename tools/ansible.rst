Ansible
=======

Ansible is the configuration management tool used for the infra.

The main reasons to use it are familliarity by the community, ease of use,
and sinergy with others projects using it.

Setup
-----

The current setup is using a trusted server that do the deployment based on git
commit. This is documented on `https://github.com/OSAS/ansible-role-ansible_bastion`.

The trusted server, is salt-master.gluster;org, mostly for historical reason

Salt bus usage
--------------

In order to keep both salt and ansible working for the time being, ansible is using
the salt bus to connect to server. This is done using custom code that can be found on 
`https://github.com/OSAS/ansible-role-salt_transport`.

Running a playbook or a ansible ad-hoc command
----------------------------------------------

For historical reasons, ansible should be run with a specific user on salt-master.gluster.org.
The specific user is set in order to restrict usage of the ssh keys and/or salt bus access. There
is work on going to let people in a specific unix group do all the work with sudo, but this is not 
finished yet.

So to run anything, just connect as root, then use su to switch to ansible_admin::

    su - ansible_admin

From here, ansible and ansible-playbook can be run directly::

    ansible all -m ping

Pushing a change
----------------

The setup use 2 git repositories. The public repository is automatically synced to github upon push.
The push of a commit also trigger a deployment to apply changes right away. 

To push for a change, start by cloning the repository::
    
    git clone ssh://salt-master.gluster.org/srv/git_repos/public ansible_gluster_public

Then modify and push to the same repository. If you are in the group `admins`, then you will be able to push.
If not, then you can send the patch on gluster-infra mailling list.

