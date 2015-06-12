Ansible Playbooks for DRACs
======
This collection of playbooks automates common DRAC tasks.  It has been tested on DRAC v5 and some newer versions.

You'll need to have [ansible installed](http://docs.ansible.com/intro_installation.html) to use these playbooks.

See below for setup, a description of each, and how to run them.


## Playbooks
In general you can run `ansible-playbook` with the name of the playbook YAML file.

All commands have these common arguments (see `ansible-playbook -h` for more info):

`-f #` - run # threads at once (ansible default is currently 5)  
`-i <inventory file>` - path to ini-style inventory file (see example-hosts)  
`-l <group>` - group or host in inventory file to limit operations to  

Example:

`ansible-playbook -f 15 -i example-hosts -l google ping.yml`

### ping
Tests basic pingability of the DRAC from the local system.  Running the above example should result in some successful and some failed pings.

### racadm
Checks to see if racadm is runnable.

### racreset
Runs a racreset on each DRAC

### only-allow-ssh
Limit DRAC services to ssh.

**NOTE:** This playbook will execute `racadm racreset` at the end of a successful run.  You may want to test this on a single DRAC first. :)

### debug
Connects and exits printing full response from the remote.

The debug playbook is useful as a quick "status" check.  The tasks will almost always succeed but the output will tell you if the DRAC is responding, etc.

## Debugging
To add debug output to any task add the following:
```yaml
  register: result
- debug: var=result
```

See the `debug.yml` playbook for a complete example.  

## TODO
- add tests (need a remote drac simulator!)
- handle more failure cases
- add cipher0 check/fix
- conditionally update settings (check first, apply only if needed..maybe we can add custom drac facts?)
- find cases where we show success but actually failed still :(
- add link to RS-specific info on how to generate drac-hosts inventory