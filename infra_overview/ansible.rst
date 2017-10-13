Ansible
=======

Ansible is the configuration management tool used for the infra.

The main reasons to use it are familiarity by the community, ease of use, and
synergy with others projects using it.

Setup
-----

The current setup is using a trusted server that do the deployment based on git
commit. This is documented on `https://github.com/OSAS/ansible-role-ansible_bastion`.

The trusted server, is salt-master.gluster.org, mostly for historical reasons.

Salt bus usage
--------------

In order to keep both salt and ansible working for the time being, ansible is
using the salt bus to connect to server. This is done using custom code that
can be found on `https://github.com/OSAS/ansible-role-salt_transport`.

Running a playbook or a ansible ad-hoc command
----------------------------------------------

For historical reasons, ansible should be run with a specific user on
salt-master.gluster.org.  The specific user is set in order to restrict usage
of the ssh keys and/or salt bus access. There is work on going to let people in
a specific unix group do all the work with sudo, but this is not finished yet.

So to run anything, just connect as root, then use su to switch to
ansible_admin::

    su - ansible_admin

From here, ansible and ansible-playbook can be run directly::

    ansible all -m ping

Pushing a change
----------------

The setup uses 2 git repositories. The public repository is automatically
synced to github on push. The push of a commit also trigger a deployment to
apply changes right away.

To push for a change, start by cloning the repository::

    git clone https://github.com/gluster/gluster.org_ansible_configuration.git ansible_gluster_public
    git remote set-url --push ssh://salt-master.gluster.org/srv/git_repos/public

Then modify and push to the same repository. If you are in the group `admins`,
then you will be able to push.  If not, then you can send the patch on
gluster-infra mailling list.

Fetching a PR from github
-------------------------

If anyone opens a PR on github, you can merge it (after proper review) using the
following process, for the PR number 4. I will assume that the repository is setup
like as explained in the previous pragraph.

Then you can use the following commands to fetch and merge 1 specific PR (for example, the PR 4)::

    git fetch origin pull/4/head:pr_4
    git checkout master
    git cherry-pick pr_4
    git push

Running ansible from a admin workstation
----------------------------------------

In order to run a command on all the servers (or a subset), you can use the following command from
a git checkout, provided you have root access::

    ansible -i hosts -l some_group -m ping

You can also adjust if you want to use sudo with -u and -K.
