https://www.youtube.com/watch?v=3RiVKs8GHYQ&list=PLT98CRl2KxKEUHie1m24-wkyHpEsa4Y70&index=1

Initial connection must be done between ansible server and the client. it is possible to configure ansible to accept the ssh prompt from the first connection


## making ssh key pair
- ls -la .ssh
- ssh-keygen -t ed25519 -C "jack default"
	- more secure than default and shorter key length
- ssh-copy-id -i .ssh/id_ed25519.pub ws1
- make a key for "ansible"
	- ssh-keygen -t ed25519 -C "ansible"
	- when asked for a path select a new final dir
		- this should now work
		- ssh -i .ssh/ansible.pub ws1
- to cash your pass phrase ssh-agent can be ran in the back ground
	- eval $(ssh-agent)
	- ssh-add
## running ad-hoc commands
- localhost gather facts
````ansible localhost -m setup```
- ping
``` 
ansible all --key-file ~/.ssh/ansible -i invintory -m ping
```
- ansible.cfg
```
[defaults]
inventory = inventory-path
private_key_file = ~/.ssh/ansible
```
- run with the new config
```
ansible all -m ping
ansible all -m hosts
ansible all -m gather_facts
ansible all -m gather_facts --limit 192.168.1.199
```

## running elevated commands
  -b become root -K ask for password 
```
ansible all -m yum -a update_cache=true --become --ask-become-pass

ansible all -m yum -a name=tmux --become --ask-become-pass

ansible all -m yum -a "name=tmux state=latest" --become --ask-become-pass

ansible all -m yum -a "upgrade=dist" --become --ask-become-pass
```

stooped on 06

## play books

- variables are written like and declared in inventory file
```      
name: "{{ httpd-package }}"

192.168.1.105 httpd-package=httpd php-package=php
```

- to run play books
```
ansible-playbook --ask-become-pass install_apache.yml
ansible-playbook -K install_apache.yml
```

- list tags in a play book
```
ansible-playbook --list-tags site.ym
```
- to run a tag play
- tags can be added to individual task/plays
```
ansible-playbook --tags centos --ask-become-pass site.yml
```
- when copying files the files directory is assumed
	- remote_src: yes is needed when not using the files dir 
- when registering a variable to a change state ansible takes the most resent variable setting
	```
	play 1=change register: test 
	 play 2=no change register: test
	echo $test = no change
	```
- alternately notify can be used to call up a new play book this play book wold be under the handlers dir for the role the play is happening on
- roles must be set in roles/rolename/tasks/main.yml
- templats must be in .j2 format
- Absolutely, here are 16 more Ansible interview 
   - `include` tasks and roles are dynamic, meaning they are processed during execution.
   - `import` tasks and roles are static, meaning they are processed during playbook parsing.

   - **Roles**: Reusable units of Ansible content, such as tasks, files, templates, and variables.
   - **Collections**: A distribution format for Ansible content that may include roles, modules, and plugins.

   - `state: present`: Ensures the package is installed.
   - `state: latest`: Ensures the package is installed and updated to the latest version.

  - Use the `ignore_errors` parameter or the `block/rescue` statements to handle errors and perform actions when tasks fail.

- The `register` keyword is used to store the output of a task in a variable, which can then be used in subsequent tasks.

  - Use the `--start-at-task` command-line option to begin execution at a specific task.

9. 
- use the `loop` keyword to iterate over a list of items within a task.

