# Dankbot

A Slack Bot that scrapes memes from subreddits and posts them to slack

## Steps to run

### Clone into directory
```
cd /opt
sudo mkdir dankbot && sudo chown <user>:<user> dankbot
git clone git@github.com:levi-rs/dankbot.git
```

### Setup INI file
```
cd /opt/dankbot
cp dankbot/dankbot.ini.sample dankbot/dankbot.ini
```

Edit the INI file to fillin the missing token, username, and password fields:
```
(.venv35)➜  dankbot git:(master) ✗ cat dankbot/dankbot.ini.sample
[slack]
token: <put here>
channel: #random

[reddit]
subreddits: dankmemes, fishpost

[mysql]
username: <username>
password: <password>
```

### Add an entry to your crontab:
Edit the crontab with your favorite editor
```
sudo vi /etc/crontab
```
And add an entry like so:
```
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the 'crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow usernamecommand
17 *17* * *17root    cd / && run-parts --report /etc/cron.hourly
25 6* * *25roottest -x /usr/sbin/anacron || ( cd / && run-parts --report
/etc/cron.daily )
47 6* * 7roottest -x /usr/sbin/anacron || ( cd / && run-parts --report
/etc/cron.weekly )
52 61 * *61roottest -x /usr/sbin/anacron || ( cd / && run-parts --report
/etc/cron.monthly )
#
*/5 10-18 * * 1-5 root cd /opt/dankbot && python3 dankbot/cli.py
```

This will run dankbot once every 5 minutes, Monday to Friday, between 9 AM and
5 PM CST
