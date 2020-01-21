Blocking a email from gerrit
============================

On a regular basis, people are leaving RH (or others companies), and as a matter of fact
in some juridictions, their work email is redirected to their management, who is in turn
flooded by Gerrit notifications. 

We receive from time to time requests from people to not receive email from Gerrit. After
some research, we found out that this would requires fiddling with Gerrit DB directly and/or fiddling
with patches submitted, both operations being time consuming and error prones. On top of that,
the various laws around the world regarding personal email (like a email sent to a single person), 
social medias accounts (such as Github, under some juridictions) and personal sysadmin responsability
make that kind of change hazardous at best.

So it was decided to instead blacklist email on the gerrit server mail server directly.

Step 1: Clone the private repository
====================================

Since we want to keep people email private, for spam and privacy reasons,
the list of blocked email are stored in a private git repository::

    git clone ssh://ant-queen.int.rht.gluster.org/srv/git_repos/private gluster_private

Step 2: Add the email to the list
=================================

The emails are stored as a yaml dictionnary in host_vars/gerrit-prod.rht.gluster.org/drop.yml
For example::

    mails_to_drop_private:
    - neo@bigcorp.example.com
    - morpheus@nebuchadnezzar.example.org

Email sent by gerrit to those adresses are going to be dropped at the SMTP server level. 

Step 3: Trigger a deploy
========================

For technical reasons linked to the use of a second repository, ansible do not deploy automatically
on commit on that repository. So we either have to wait on automated run of ansible, or do it
manually with::

    su - ansible_admin
    ansible-playbook /etc/ansible/playbooks/playbooks/deploy_gerrit.yml

