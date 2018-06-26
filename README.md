Borg systemd scripts
====================

These are some systemd .service and .timer scripts that I use for
personal backups. Here is a rough procedure how to set them up:

1. Initialize a borg repo:

```
borg init --encryption none ~/Backups/borg/hostname-username-topic
```

2. Use a custom `borg-backup-topic.{service,timer}` pair of scripts to
set up *what* to back up and how often. Then copy/enable/start them:

```
sudo cp borg-backup-topic.service /etc/systemd/user
sudo cp borg-backup-topic.timer /etc/systemd/user

systemctl --user enable borg-backup-topic.service
systemctl --user enable borg-backup-topic.timer

systemctl --user start borg-backup-topic.timer
```

3. TODO: set up another `.{service,timer}` pair to prune the archive.