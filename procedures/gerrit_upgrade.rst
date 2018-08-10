Gerrit Upgrade
==============

Upgrade Steps
-------------
* Send email to gluster-devel, gluster-infra, and automated-testing announcing
  the start of the outage window.
* Put an outage page for Apache. Modify the apache config with this line::

   ErrorDocument 500 "Sorry, our script crashed. Oh dear"

* Stop the port 22 port forward to prevent accidental pushes::

   systemctl stop xinetd

* Stop gerrit.::

   su - review
   cd review.gluster.org
   bin/gerrit.sh stop

* Back up Gerrit DB and files into `~/review` inside the `review` user's home
  directory.
* Download the latest version of gerrit into `/review/review.gluster.org`
* Run `java -jar gerrit-x.x.x.war init` (press enter for most prompts).
* Make sure you upgrade all the prompted plugins
* Upgrade Github auth plugin to latest available on ci.gerritforge.com
* Upgrade events-log to latest available.
* There is a good chance you need to do a full re-index::

   java -jar /review/review.gluster.org/bin/gerrit.war reindex

* Run bin/gerrit.sh run to confirm that there are no errors.
* Ctrl + C the terminal and start Gerrit from systemd.
* Start the SSH proxy via xinetd
* Restart Apache without the error page

Post Upgrade Testing
--------------------
The following are them minimum pieces to verify after a Gerrit upgrade:
* Use the UI to browse changes. Verify diffs are visible. Problems here usually
  mean that there's an Apache configuration issue.
* Logout and login. Any problems here usually point to a Github library
  mismatch.
* Verify that all the user names are visible and not just account numbers.
* Push a test review and verify that the push goes through.
* Verify that Jenkins voting work as expected for this change.
* Verify that git protocol clones work.
* Verify that git.gluster.org works as expected.
