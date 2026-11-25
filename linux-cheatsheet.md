# Linux Cheatsheet

> A practical reference for navigating, managing, and troubleshooting Linux systems from the command line.

## Table of Contents
- [File & Directory Operations](#file--directory-operations)
- [Permissions](#permissions)
- [Viewing & Editing Files](#viewing--editing-files)
- [Searching](#searching)
- [Process Management](#process-management)
- [System Information](#system-information)
- [Networking](#networking)
- [Disk Usage](#disk-usage)
- [Users & Groups](#users--groups)
- [Archiving & Compression](#archiving--compression)
- [Package Management](#package-management)
- [Services](#services)

## File & Directory Operations

| Command | Description |
| --- | --- |
| `pwd` | Print the current working directory. |
| `ls` | List files in the current directory. |
| `ls -la` | List all files with detailed metadata, including hidden files. |
| `cd /path/to/dir` | Change to a specified directory. |
| `cd -` | Return to the previous working directory. |
| `mkdir -p path/to/dir` | Create a directory and any missing parent directories. |
| `touch file` | Create an empty file or update its timestamp. |
| `cp source destination` | Copy a file or directory. |
| `cp -r source-dir destination-dir` | Recursively copy a directory. |
| `mv source destination` | Move or rename a file or directory. |
| `rm file` | Remove a file. |
| `rm -rf directory` | Recursively remove a directory without prompts. |
| `ln -s target link` | Create a symbolic link. |
| `file path` | Identify a file's type and format. |

## Permissions

| Command | Description |
| --- | --- |
| `chmod 644 file` | Set read/write owner and read-only group and other permissions. |
| `chmod +x script.sh` | Add execute permission for all applicable users. |
| `chmod -R 755 directory` | Recursively set directory permissions. |
| `chown user file` | Change a file's owner. |
| `chown user:group file` | Change a file's owner and group. |
| `chown -R user:group directory` | Recursively change ownership. |
| `umask 027` | Set the default permission mask for new files. |
| `sudo command` | Run a command with elevated privileges. |
| `getfacl file` | Display file access control lists. |
| `setfacl -m u:user:r file` | Grant a user an ACL read permission. |

## Viewing & Editing Files

| Command | Description |
| --- | --- |
| `cat file` | Print a file to standard output. |
| `less file` | Browse a file interactively. |
| `head -n 20 file` | Show the first 20 lines of a file. |
| `tail -n 20 file` | Show the last 20 lines of a file. |
| `tail -f file` | Follow new lines appended to a file. |
| `nl -ba file` | Print a file with all lines numbered. |
| `wc -l file` | Count the lines in a file. |
| `sort file` | Sort lines lexicographically. |
| `uniq -c file` | Count adjacent duplicate lines. |
| `nano file` | Edit a file with the Nano editor. |
| `vim file` | Edit a file with Vim. |

## Searching

| Command | Description |
| --- | --- |
| `grep 'pattern' file` | Search a file for a pattern. |
| `grep -R 'pattern' directory` | Recursively search files under a directory. |
| `grep -n 'pattern' file` | Include matching line numbers in search results. |
| `grep -i 'pattern' file` | Search without case sensitivity. |
| `grep -v 'pattern' file` | Show lines that do not match a pattern. |
| `find . -name '*.log'` | Find matching names below the current directory. |
| `find . -type f -size +100M` | Find regular files larger than 100 MB. |
| `find . -mtime -1` | Find paths modified within the last day. |
| `locate filename` | Search the system file-name database. |
| `command -v executable` | Show the executable selected by the shell. |

## Process Management

| Command | Description |
| --- | --- |
| `ps aux` | List all running processes with detailed information. |
| `top` | Monitor processes and system resource usage interactively. |
| `htop` | Monitor processes with an enhanced interactive interface. |
| `pgrep -af name` | Find processes by name and show their commands. |
| `pidof process` | Print process IDs for a program. |
| `kill PID` | Request graceful termination of a process. |
| `kill -9 PID` | Forcefully terminate a process. |
| `pkill -f pattern` | Signal processes whose full command matches a pattern. |
| `jobs -l` | List jobs launched by the current shell. |
| `bg %1` | Resume a stopped job in the background. |
| `fg %1` | Bring a shell job to the foreground. |
| `nohup command &` | Run a command immune to hangup signals. |

## System Information

| Command | Description |
| --- | --- |
| `uname -a` | Display kernel and system information. |
| `hostnamectl` | Show or configure the system hostname. |
| `uptime` | Show system uptime and load averages. |
| `date` | Print the current date and time. |
| `whoami` | Print the effective current username. |
| `env` | Display the current environment variables. |
| `free -h` | Display memory and swap usage in human-readable units. |
| `lscpu` | Display CPU architecture and processor details. |
| `lsblk` | List block devices and mount points. |
| `dmesg -T` | Display kernel messages with readable timestamps. |

## Networking

| Command | Description |
| --- | --- |
| `ip addr` | Display network interfaces and IP addresses. |
| `ip route` | Display the kernel routing table. |
| `ip link set eth0 up` | Enable a network interface. |
| `ping -c 4 host` | Send four connectivity test packets. |
| `ss -tulpn` | List listening TCP and UDP sockets with processes. |
| `curl -I https://example.com` | Fetch only HTTP response headers. |
| `wget URL` | Download a resource from a URL. |
| `dig example.com` | Query DNS records for a domain. |
| `traceroute host` | Trace the network path to a host. |
| `ssh user@host` | Open a secure remote shell session. |
| `scp file user@host:/path` | Copy a file over SSH. |

## Disk Usage

| Command | Description |
| --- | --- |
| `df -h` | Show filesystem free space in human-readable units. |
| `du -sh directory` | Show the total size of a directory. |
| `du -h --max-depth=1` | Show sizes of immediate subdirectories. |
| `lsblk -f` | Show block devices, filesystems, and labels. |
| `mount` | Display currently mounted filesystems. |
| `mount /dev/sdb1 /mnt` | Mount a filesystem at a directory. |
| `umount /mnt` | Unmount a filesystem. |
| `ncdu` | Explore disk usage interactively. |

## Users & Groups

| Command | Description |
| --- | --- |
| `id user` | Display a user's UID, GID, and group memberships. |
| `who` | List users currently logged in. |
| `last` | Show recent login history. |
| `useradd -m user` | Create a user with a home directory. |
| `passwd user` | Set or change a user's password. |
| `usermod -aG group user` | Add a user to a supplementary group. |
| `userdel -r user` | Remove a user and its home directory. |
| `groupadd group` | Create a group. |
| `groups user` | List the groups to which a user belongs. |

## Archiving & Compression

| Command | Description |
| --- | --- |
| `tar -cf archive.tar directory` | Create an uncompressed tar archive. |
| `tar -xf archive.tar` | Extract a tar archive. |
| `tar -czf archive.tar.gz directory` | Create a gzip-compressed tar archive. |
| `tar -xzf archive.tar.gz` | Extract a gzip-compressed tar archive. |
| `tar -cjf archive.tar.bz2 directory` | Create a bzip2-compressed tar archive. |
| `tar -xjf archive.tar.bz2` | Extract a bzip2-compressed tar archive. |
| `gzip file` | Compress a file with gzip. |
| `gunzip file.gz` | Decompress a gzip file. |
| `zip -r archive.zip directory` | Create a ZIP archive recursively. |
| `unzip archive.zip` | Extract a ZIP archive. |

## Package Management

| Command | Description |
| --- | --- |
| `sudo apt update` | Refresh package metadata on Debian-based systems. |
| `sudo apt upgrade` | Upgrade installed Debian packages. |
| `sudo apt install package` | Install a Debian package and dependencies. |
| `sudo apt remove package` | Remove a Debian package. |
| `sudo apt autoremove` | Remove unused Debian package dependencies. |
| `sudo yum install package` | Install a package on yum-based systems. |
| `sudo yum update` | Update packages on older RPM-based systems. |
| `sudo dnf install package` | Install a package with DNF. |
| `sudo dnf upgrade` | Upgrade packages with DNF. |
| `rpm -qa` | List installed RPM packages. |

## Services

| Command | Description |
| --- | --- |
| `systemctl status service` | Show the current status of a systemd service. |
| `sudo systemctl start service` | Start a systemd service. |
| `sudo systemctl stop service` | Stop a systemd service. |
| `sudo systemctl restart service` | Restart a systemd service. |
| `sudo systemctl reload service` | Reload a service configuration without stopping it. |
| `sudo systemctl enable service` | Enable a service at boot. |
| `sudo systemctl disable service` | Disable a service at boot. |
| `systemctl is-active service` | Check whether a service is active. |
| `systemctl list-units --type=service` | List loaded service units. |
| `journalctl -u service` | View logs for a systemd service. |
| `journalctl -u service -f` | Follow live logs for a systemd service. |
