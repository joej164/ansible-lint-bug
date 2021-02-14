# ansible-lint-bug

repo to try and duplication ansible lint bug

The issue appears to be when a requirements.yml file is in the root of the repo

Do the following to replicate

- Install Vagrant (i used Virtual Box on a Mac)
- Clone the repo
- Type `vagrant up`
- Type `vagrant ssh`
- Type `cd /vagrant`
- Type `ansible-lint`

Then you'll get the following message, i added the echo to show the exit command

```
[vagrant@localhost vagrant]$ ansible-lint
Running ansible-galaxy install --roles-path .cache/roles -vr requirements.yml
Running ansible-galaxy collection install -p .cache/collections -vr requirements.yml
[vagrant@localhost vagrant]$ echo $?
1
```

If you run the first command...

```
[vagrant@localhost vagrant]$ ansible-galaxy install --roles-path .cache/roles -vr requirements.yml
No config file found; using defaults
Starting galaxy role install process
[WARNING]: - PaloAltoNetworks.paloaltonetworks (v2.4.1) is already installed - use --force to change version to unspecified
```

If you run the second command...

```
[vagrant@localhost vagrant]$ ansible-galaxy collection install -p .cache/collections -vr requirements.yml
No config file found; using defaults
ERROR! Expecting requirements file to be a dict with the key 'collections' that contains a list of collections to install
```
