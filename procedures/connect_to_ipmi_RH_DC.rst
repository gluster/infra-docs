Connecting to the admin remote interface in the community cage
==============================================================


The 4 servers in the DC are:
- pleometrosis.rht.gluster.org
- haplometrosis.rht.gluster.org
- myrmicinae.rht.gluster.org
- formicary.rht.gluster.org

Each of them is connected on the admin network.

Here is a summary of the ip address:

============= =========== ===============
Server        IP          Admin interface
haplometrosis 172.24.0.11 172.24.0.1
pleometrosis  172.24.0.12 172.24.0.2
myrmicinae    172.24.0.13 172.24.0.3
formicary     172.24.0.14 172.24.0.4
============= =========== ===============

Step 1: Setting up a tunnel with ssh
------------------------------------

Depending on the operation, you will need to connect to one server
in order to make a ssh tunnel for the others.

If you want to connect to pleometrosis admin interface, use this::

    ssh -N -L 5900:172.24.0.2:5900 -L 8080:172.24.0.2:8080 haplometrosis.rht.gluster.org

If you want to connect to haplometrosis admin interface, then use this::

    ssh -N -L 5900:172.24.0.1:5900 -L 8080:172.24.0.1:8080 pleometrosis.rht.gluster.org

If you want to connect to myrmicinae admin interface, then use this::

    ssh -N -L 5900:172.24.0.3:5900 -L 8080:172.24.0.3:8080 -L 8443:172.24.0.3:8443 pleometrosis.rht.gluster.org

If you want to connect to formicary admin interface, then use this::

    ssh -N -L 5900:172.24.0.4:5900 -L 8080:172.24.0.4:8080 -L 8443:172.24.0.4:8443 pleometrosis.rht.gluster.org

Step 2: Connecting to the web interface
---------------------------------------

Just use a browser and go to http://127.0.0.1:8080/

Connect using the login/password provided by the infra team.

iDrac (for Dell servers) will redirect you to a https connexion, with a self signed certificate.
Adding the ssl certificate key and/or a proper certificate is planned to be done later.

Step 3: Connecting to VNC
-------------------------

Supermicro and Dell use a java applet for that. Make sure that iced tea is installed and properly
configured on your system.

On the web interface, you can click on the preview of the console to start
the VNC interface. If the browser download the launch.jnlp file, then you
have to open it with /usr/bin/javaws.
