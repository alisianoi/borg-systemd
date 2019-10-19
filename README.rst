Borg systemd scripts
====================

These are some systemd .service and .timer scripts that I use for
personal backups. Here is how to set them up and monitor them.

How to add new backup repo
--------------------------

1. Initialize a borg repo:

.. code-block:: bash

   borg init --encryption none ~/Backup/borg/host-user-repo

2. Use a custom `borg-backup-topic.{service,timer}` pair of scripts to
set up *what* to back up and *how* often. Copy both to user's systemd
scripts and then enable/start timers:

.. code-block:: bash

   sudo cp borg-backup-topic.service /etc/systemd/user
   sudo cp borg-backup-topic.timer /etc/systemd/user

   systemctl --user enable borg-backup-topic.timer
   systemctl --user start borg-backup-topic.timer

How to check that backups are working
-------------------------------------

.. warning::
   If you are running services with superuser privileges, repeat all
   the subsequent commands *without* the `--user` switch.

Make sure the timers are enabled and running:

.. code-block:: bash

   systemctl --user list-timers --all

Make sure the services are ok:

.. code-block:: bash

   systemctl --user status borg-backup-topic
