\# Linux Command Cheat Sheet



| Linux Command | What It Does | When to Use It |

|---|---|---|

| `pwd` | Shows the folder you are in | When you are lost and need to know your location |

| `ls` | Lists files and folders | To see what is inside a folder |

| `ls -la` | Lists everything with details, including hidden files | To check permissions, owners and hidden files |

| `cd` | Changes folder | To move to another directory |

| `mkdir` | Creates a new folder | When setting up a project or lab folder |

| `rmdir` | Removes an empty folder | To clean up folders you no longer need |

| `touch` | Creates an empty file | To quickly make a new file |

| `cp` | Copies files or folders | To make a backup before editing something |

| `mv` | Moves or renames files | To rename a file or put it in a new place |

| `rm` | Deletes files | To remove files you no longer need, carefully, there is no recycle bin |

| `cat` | Prints a file on screen | To read short files |

| `less` | Reads a long file page by page | To read logs without flooding the screen |

| `head` | Shows the first lines of a file | To peek at the start of a file or log |

| `tail` | Shows the last lines of a file | To see the newest log entries |

| `tail -f` | Follows a file as it grows | To watch a log live while something runs |

| `grep` | Searches for text inside files | To find a keyword or error in a file |

| `find` | Searches for files by name, size or type | When you know a file exists but not where |

| `wc -l` | Counts lines in a file | To count log entries or results |

| `sort` | Sorts lines of text | To put output in order |

| `echo` | Prints text or writes it to a file | To test commands or add a line to a file |

| `nano` | Simple text editor in the terminal | To edit files without leaving the terminal |

| `chmod` | Changes file permissions | To make a script runnable or lock a file down |

| `chown` | Changes file owner | When the wrong user owns a file |

| `sudo` | Runs a command as administrator | When a command needs admin rights |

| `whoami` | Shows your current user | To confirm which account you are using |

| `id` | Shows your user ID and groups | To check what groups and rights you have |

| `man` | Opens the manual for a command | When you forget how a command works |

| `history` | Lists commands you typed before | To find and repeat an earlier command |

| `uname -a` | Shows system and kernel information | To record which system you are on |

| `ps aux` | Lists running processes | To see what is running on the machine |

| `top` | Shows live CPU and memory use | To find what is slowing the machine down |

| `kill` | Stops a process by its ID | To close a stuck program |

| `df -h` | Shows disk space in readable sizes | To check if a disk is nearly full |

| `du -sh` | Shows how big a folder is | To find what is using your space |

| `ip a` | Shows network interfaces and IP addresses | To find the IP of a machine |

| `ping` | Tests if another machine replies | To check that two machines can talk |

| `traceroute` | Shows the path packets take to a target | To see where a connection slows or stops |

| `nslookup` | Looks up a domain name's IP | To check that DNS is working |

| `dig` | Detailed DNS lookup | To see DNS records in more detail |

| `ss -tuln` | Lists open listening ports | To see which services are waiting for connections |

| `ssh` | Logs in to another machine securely | To control a VM or server remotely |

| `scp` | Copies files between machines over SSH | To send a file to or from a VM |

| `apt update` | Refreshes the list of available packages | Before installing new software on Ubuntu or Kali |

| `apt install` | Installs a package | To add a new tool |

