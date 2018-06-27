Borg systemd scripts
====================

These are some systemd .service and .timer scripts that I use for
personal backups. Here is a rough procedure how to set them up:

1. Initialize a borg repo:

```
borg init --encryption none ~/Backups/borg/host-user-repo
```

2. Use a custom `borg-backup-topic.{service,timer}` pair of scripts to
set up *what* to back up and *how* often. Copy both to user's systemd
scripts and then enable/start timers:

```
sudo cp borg-backup-topic.service /etc/systemd/user
sudo cp borg-backup-topic.timer /etc/systemd/user

systemctl --user enable borg-backup-topic.timer
systemctl --user start borg-backup-topic.timer
```