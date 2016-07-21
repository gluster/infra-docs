Requesting a Loaner Machine
===========================

If you wish to debug a test failure on our test environment, you can request
a loaner build node.

How to Request
--------------

* File a `bug`_ asking for a loaner machine.
* Mention the operating system version and version (For example: NetBSD 7).
* Attach your SSH public key to this bug. You will be granted access via SSH
  keys.
* Once the machine is setup, you can run your tests. Before returning the
  machine, please delete any temporary files or folders you use for testing.
* After you have finished testing, please comment on the bug. The machine will
  be returned to the pool in 7 days unless you specify that you want it for
  more time.

How to Handle a Loaner Request
------------------------------

* Find an idle machine and disable it from Jenkins. Mention the bug number in
  the reason.
* Add the requester's SSH key on the machine as the Jenkins user. Do not close
  the bug.
* When the machine is returned, remove the requester's SSH keys from the
  Jenkins user and delete any temporary files placed for testing.
* Return the machine to Jenkins pool.
* Close the bug after the machine is returned to the Jenkins pool.

.. _bug: https://bugzilla.redhat.com/enter_bug.cgi?product=GlusterFS&component=project-infrastructure

