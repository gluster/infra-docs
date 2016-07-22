Adding a new mailling list
--------------------------

For now, the lists are still managed in salt. This is expected to change
in the future, and due to that, the process is not as streamlined
as it could be.

Step 1: Adding the list to the aliases file
===========================================

In order to add the alias, you need to modify the file mailing_lists.sls
in the salt public pillar repository. Refer to the documentation of salt for
accessing it.

The file is just a yaml file with a array of mailling list that will be created.

Once the file is committed, salt should create the list. However, it seems some various
problem prevent it from working properly for the time being, so we need to create it manually.


Step 2: Create the list
=======================

To verify that the list is created, please connect to lists.gluster.org, and check with
the list_lists command::

    /usr/lib/mailman/bin/list_lists

If the list appear, then all is good. If not, you need to create it manually with this command::

    /usr/lib/mailman/bin/newlist NAME ADMIN NAME

By convention, ADMIN should be the list-admin alias for gluster.org, and the password should be the same
as the name of the list.

All people in the list-admin alias will get the notification (in practice, this mean people who are on the root
alias), so you can forward it to the user who requested the list.
At minima, you should make sure they change the password. They do not need to give it to anyone since
there is a master password for all lists and it can be reset using traditional CLI tools of mailman 2.
