Adding a admin on nagios
========================

In order to receive alert from nagios, a admin must be added to the ansible
configuration. This is currently managed in the private repository, in the file
group_vars/nagios/admins.yml

The admins variable contains groups, and then a list of mail to be notified of alerts.

We currently use only one group for everything, so the structure is the following::

    admins:
      default:
      - { mail: admin@example.org, pager: False}
      - { mail: admin-page@example.com, pager: True}

The pager variable control the formatting of the alert in order to be more suitable
for a text message, see the nagios role for details.

Upon commit, the `playbook/deploy_nagios.yml` playbook must be run as the private repository
do not have yet automated trigger for deployment.

Once the admin is added, do not forget to communicate the nagios_admin password written in the same file.
