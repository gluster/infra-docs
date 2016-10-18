Adding a email alias
--------------------

Email alias are managed by ansible, in the private repository.

Step 1: Clone the private repository
====================================

Since we want to keep people email private, for spam and privacy reasons, 
the list of alias are stored in a private git repository::

    git clone ssh://salt-master.gluster.org/srv/git_repos/private gluster_private

Step 2: Add the alias
=====================

The aliases are stored as a yaml hash in host_vars/supercolony.gluster.org/email_aliases.yml
Format is quite straightforward, the key is the name of the alias, and the value is a list
of email where the alias is going to be redirected.

For example::

    mail_aliases:
        root:
        - michael
        - nigel@example.com

This redirect root@ to michael@ (who is later redirected to another email) and to nigel@example.com

Step 3: Trigger a deploy
========================

For technical reasons linked to the use of a second repository, ansible do not deploy automatically
on commit on that repository. So we either have to wait on automated run of ansible, or do it
manually with::

    su - ansible_admin
    ansible-playbook /etc/ansible/playbooks/deploy_postfix.yml
