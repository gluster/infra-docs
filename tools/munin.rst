Munin
=====

Munin is our primary graphing solution. We used it mostly because it is packaged
and easy to deploy.

* URL: http://munin.gluster.org/munin/

Deployment
==========

Munin was deployed using ansible, with the `ansible-role-munin <https://gitlab.com/osas/ansible-role-munin.git>`
role. It should be deployed on all ansible managed systems, which at the time of writing of this documentation,
mean all FreeBSD and Linux systems except gerrit and jenkins.

