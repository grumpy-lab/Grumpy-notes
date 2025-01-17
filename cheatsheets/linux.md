#cheatsheets #Linux

## Commands

### File & Directory Basics

```bash
# List files in the current directory.
ls

# List files in the current directory with details.
ls -alh

# Change current directory.
cd

# Show current directory.
pwd

# Create an empty directory.
mkdir

# Copy file.
cp <src-filename> <dst-filename>

# Copy directory.
cp -Rf <src-dirname> <dst-dirname>

# Move file or directory.
mv <src-filename> <dst-filename>

# Remove file.
rm <filename>

# Remove an empty directory.
rmdir <dirname>

# Remove a non-empty directory.
rm -Rf <dirname>

# Create a new empty file.
touch <filename>

# Find files.
find . -iname <filename-regex>

# Find all files.
find . -type f
```

### File Content

```bash
# Print file content.
cat <filename>

# Search texts in file.
grep <text> <filename>

# Search regex pattern in file.
grep -e <regex-pattern> <filename>

# Show first few lines in file.
head -n <line-count> <filename>

# Show last few lines in file.
tail -n <line-count> <filename>

# Follow file changes.
tail -f <filename>
```

### File Access

```bash
# Change file access. An example of access-code is 600.
chmod <access-code> <filename>

# Change file owner.
chown <owner>[:<group>] <filename>
```

### Package & Compress

```bash
# Pack a directory into a tar file.
tar -cvf <tar-filename>.tar <dirname>

# Unpack a tar file.
tar -xvf <tar-filename>.tar

# Zip a file.
zip <zip-filename> file1 file2 file3 ...

# Unzip a file.
unzip <zip-filename>
```

### Disk

```bash
# Show free disk spaces for each block device.
df -alh

# Display the disk usage of files under the current directory.
du -h ./*

# Show block devices.
lsblk
```

### Process

```bash
# List process.
ps aux

# Kill a process with SIGTERM.
kill <pid>

# Kill a process with SIGKILL (the strongest killing signal).
kill -9 <pid>

# List all processes in a terminal UI.
top

# List all processes in an advanced terminal UI.
htop
```

### Networking

```bash
# Download data from url.
curl <url>

# Download data from url to local file.
curl <url> -o <filename>

# List all ports opened.
netstat -an

# List network configuration.
ifconfig

# Ping network connectivity.
ping
```

### User

```bash
# Add a new user.
sudo adduser <username>

# Delete a user.
sudo deluser <username>
```

### Packages

```bash
# Install packages on ubuntu or debian.
sudo apt install <package-name>[=<version>]

# Uninstall packages from ubuntu or debian.
sudo apt-get --purge remove <package-name>

# extract a rpm in current directory with its expected paths
rpm2cpio myrpmname*.rpm | cpio -idmv
```

### System

```bash
# Display information about your system.
uname -a

# Display Linux release information
lsb_release -a

# Show hostname.
hostname

# Reboot system now.
sudo reboot now

# Shutdown system now.
sudo shutdown -h now
```

### Services

```bash
# List all units.
systemctl list-units

# List all service units.
systemctl list-units --type=service

# Start a service.
sudo systemctl start <service-name>

# Restart a service.
sudo systemctl restart <service-name>

# Stop a service.
sudo systemctl stop <service-name>

# Check a service status.
sudo systemctl status <service-name>

# Enable a service to start as system starts.
sudo systemctl enable <service-name>
```

## Configuration Files

|File Path|Scope|File Use|
|---|---|---|
|`/boot/grub/grub.cfg`|global|the generated grub file|
|`/etc/bash.bashrc`|global|global config file for bash|
|`/etc/default/grub`|global|config used by update-grub to generate /boot/grub/grub.cfg|
|`/etc/dhcp/dhclient.conf`|global|DCHP client configs|
|`/etc/fstab`|global|startup mount configs|
|`/etc/hostname`|global|hostname|
|`/etc/hosts`|global|static dhcp entries|
|`/etc/mime.types`|global|MIME types and filename extensions associated with them|
|`/etc/motd`|global|log in prompt message|
|`/etc/profile`|global|commands for the login shell to execute|
|`/etc/resolv.conf`|global|DNS server config|
|`/etc/sudoers`|global|configs for sudoers|
|`/etc/timezone`|global|local timezone|
|`~/.bashrc`|user|bash startup config for non-login shell|
|`~/.editor`|user|sets the default editor for the user|
|`~/.gitconfig`|user|sets the default configs for git|
|`~/.profile`|user|shell startup commands|
|`~/.ssh/config`|user|user ssh config|
|`~/.vimrc`|user|vim config|
|`~/.emacs`|user|emacs config|
|`~/.xinitrc`|user|xmanager config|