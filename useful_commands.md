# commands

- reset desktop if updating aplication shortcuts
``` 
sudo update-desktop-database 
```

- reversing ip to dns
```
nslookup
```

- xport a firefox instance from one host to another
``` 
 Xhost +
 ssh ws
 export DISPLAY=ws2:0.0
 firefox -p
```

- enable root login usualy with puppet but will work if file path is changed to the sshd_config on local host

```
find /etc/puppetlabs/code/environments/production/modules/stig_rhel7/files/ -type f -exec sed -i 's/PermitRootLogin no/PermitRootLogin yes/g' {} +

or

sed -i 's/PermitRootLogin no/PermitRootLogin yes/g' ssh_config*
```

- extending storage for a vm spacificly used for extending a repo

  - remove all snapshots
	- extend the volume in vcenter
```
pvresize /deb/sdb
lvextend -l +100%FREE /dev/vg1/repos
xfs_growfs /var/www/html/repos
```

- creating a new repo
```
reposync --repoid=rhel-server-rhscl-7-rpms --newest-only --download_path=rhel-server-rhscl-7-rpms-20240730
```



### rpm

- extracting a rpm and its path completely in current directory
```rpm2cpio myrpmname*.rpm | cpio -idmv```
- update selinux for a rpm repo
```
chown -R apche:apache /var/www/html/rpmrepo
chcon -R system_u:object_r:httpd_sys_content_t:s0 /var/www/html/rpmrepo
```

### ipa
```
ipa user-add username --first=fname --last=lname --gidnumber=15

ipa user-mod username --password

ipa group-add-member groupname --users=username

ipa group-find --all | awk '/^ Group name:/ {print $3} /^ GID:/ {print $2}'

ipa user-unlock username
```

### puppet

- clear bad certs on a client
``` 
client# rm -rf /etc/puppetlabs/puppet/ssl/
Client# puppet agent -t

or

Client# rm -rf /etc/puppetlabs/puppet/ssl && puppet agent -t
```

- clear bad cert on server
```
puppet-server# puppetserver ca clean --cername=ws1.fqdn
```




