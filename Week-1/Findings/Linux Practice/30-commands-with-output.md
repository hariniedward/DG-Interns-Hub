\# Task 2: 30 Commands with Output (Ubuntu-lab)



| # | Command | What it does | Output (short) |

|---|---|---|---|

| 1 | whoami | Shows current user | ubuntu |

| 2 | hostname | Shows machine name | ubuntu-lab |

| 3 | pwd | Shows current folder | /home/ubuntu |

| 4 | uname -r | Shows kernel version | 7.0.0-38-generic |

| 5 | uptime | Shows running time and load | up 12 min, 2 users, load 0.00 |

| 6 | df -h | Shows disk space | / is 8.1G, 60% used |

| 7 | free -h | Shows memory | 1.6Gi total, 1.2Gi available |

| 8 | sudo adduser --disabled-password --gecos "" alice | Creates user alice | User created, uid 1001 |

| 9 | sudo adduser --disabled-password --gecos "" bob | Creates user bob | User created |

| 10 | sudo adduser --disabled-password --gecos "" carol | Creates user carol | User created |

| 11 | sudo groupadd developers | Creates group | Group created (gid 1004) |

| 12 | sudo groupadd analysts | Creates group | Group created |

| 13 | sudo usermod -aG developers alice | Adds alice to group | usermod: no changes |

| 14 | sudo usermod -aG developers bob | Adds bob to group | usermod: no changes |

| 15 | sudo usermod -aG analysts carol | Adds carol to group | usermod: no changes |

| 16 | id alice | Shows user and groups | uid=1001(alice) ... 1004(developers) |

| 17 | getent group developers | Lists group members | developers:x:1004:alice,bob |

| 18 | sudo mkdir /srv/shared | Creates shared folder | No output (success) |

| 19 | sudo chown root:developers /srv/shared | Sets owner and group | No output (success) |

| 20 | sudo chmod 2770 /srv/shared | Sets permissions with SGID | No output (success) |

| 21 | ls -ld /srv/shared | Shows folder permissions | drwxrws--- 2 root developers ... /srv/shared |

| 22 | sudo -u alice touch /srv/shared/alice-note.txt | alice creates a file | Success, no output |

| 23 | sudo -u carol touch /srv/shared/test.txt | carol tries to create a file | Permission denied (expected) |

| 24 | find /etc -name "\*.conf" -type f, then head -5 | Finds .conf files | 5 paths, e.g. /etc/ucf.conf |

| 25 | grep "ubuntu" /etc/passwd | Searches text in a file | ubuntu:x:1000:1000:ubuntu:/home/ubuntu:/bin/bash |

| 26 | ps aux, then head -5 | Lists running processes | systemd (PID 1), kthreadd, and others |

| 27 | sudo ss -tulpn | Lists listening ports | sshd on port 22, DNS on 53 |

| 28 | crontab - (add job) | Schedules a job every minute | No output (success) |

| 29 | crontab -l | Shows the cron jobs | \* \* \* \* \* date >> /home/ubuntu/cron-test.log |

| 30 | cat /home/ubuntu/cron-test.log | Shows the cron result | 8 date lines, 12:35 to 12:42 |



Extras: sudo -v (cached sudo login) and crontab -r (removed the job after the test).

