Planet
======

Planet.gluster.org is the blog aggregator of the gluster community.

This is based on middleman, a ruby fremawork to build static website. 

Setup
-----

The website is served out of the main webserver, `supercolony.gluster.org`.
The planet is built on `webbuilder.int.rht.gluster.org` on a regular basis specified in the
configuration, see `https://github.com/gluster/gluster.org_ansible_configuration/blob/master/playbooks/deploy_webbuilder.yml`.

To debug the build, please take a look at the ansible module documentation, on `https://github.com/OSAS/ansible-role-web_builder`.
