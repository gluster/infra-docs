Adding a new mailling list
--------------------------

In order to add a list, you need to modify the file playbooks/deploy_postfix.yml
in the ansible repository. The variable mailing_lists containt the lists, and
you just need to add the name of the list there.

Once the list is created (ie, after the push), people in the list-admin alias will
get the password by email and need to forward the mail to the owner of the list to configure
it.
