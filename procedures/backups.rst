Adding and restoring backups
============================

backups are done by rdiff-backup, on backups.int.rht.gluster.org.
The server connect to the remote server with ssh, so there should be
a way to access it. The VM is currently running on formicary.rht.gluster.org,
and is not accessible from the internet.

Adding a directory to be backed up
----------------------------------

To add a new directory, the file playbooks/deploy_backups.yml must be modified.
The role 'backups' take a list as a argument, with the directory, the size to be set aside
for backups, the maximal age of the files to keep, and the server and user to connect by ssh.

For example, to make a copy of all data from /etc/ since 20 days from server.example.org, assuming this
will take 30G and using root, it should be like this::

    - directory: /etc
      age_max: "20D"
      size: "30G"
      server: "server.example.org"
      user: root

Make sure that the data to be copied are in suitable format for restoration (SQL dump).

The role will automatically install a ssh key, limit it for usage, and add a logical volume of
the specified size on the backups server.

Restoring files from backups
----------------------------

To restore a file, just copy it from the server to the target.

if the file is no longer present, it can be restored using rdiff-backup. Refer to the man pages
for usage.
