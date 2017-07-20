# [Kontena](https://kontena.io/) Ansible

<br />

<p align="center">
    <a href="https://kontena.io/">
        <img src="https://kontena.io/images/kontena-logo.svg" width="280">
    </a>
</p>

<br />
<br />

This Ansible configs automatically installing `Kontena Master`, `Kontena Node` and `Kontena CLI`.

## How to use

1. Install dependencies:
`ansible-galaxy install -r requirements.yml`
2. Write you hosts to `inventory/hosts` file.
3. Run it.
```
ansible-playbook playbooks/start.yml
```

## Options

#### Install docker on all hosts 

```
ansible-playbook playbooks/start.yml --tags=docker
```

#### Install Kontena Agent on all hosts 

```
ansible-playbook playbooks/start.yml --tags=kontena_agent
```

#### Install Kontena Master on all hosts 

```
ansible-playbook playbooks/start.yml --tags=kontena_master
```

#### Install Docker & Kontena Master

```
ansible-playbook playbooks/start.yml --limit=master
```

#### Install Docker & Kontena Agent (to nodes)

```
ansible-playbook playbooks/start.yml --limit=nodes
```

#### Install Kontena CLI

```
ansible-playbook playbooks/start.yml --limit=cli
```

## TODO

* [ ] create separate repo for `kontena-master` role & register her to the ansible-galaxy
* [ ] create separate repo for `kontena-node` role & register her to the ansible-galaxy
* [x] write role for installing `kontena-cli` on GNU/Linux (yes, I'm so lazy for lift my fingers above the keyboard...)
* [ ] automatically uninstall all installed packages: `docker`, `kontena-master`, `kontena-node` and `kontena-cli`
* [ ] write tests

## Support of OS

For now supports:
* Ubuntu 16.04 LTS
* Ubuntu 14.04 LTS

## Vagrant

I specially inserted ssh public key to VM (see `Vagrantfile`), that allow to work us with VM like as with remote server (without separate configuration of Ansible for this).
It requires some preliminary action. Such as:

```
ssh-keygen -f ~/.ssh/known_hosts -R 10.110.0.10
ssh-keygen -f ~/.ssh/known_hosts -R 10.110.0.11
```

After, `ssh root@10.110.0.10` type `yes` and exit from VM. Repeat for `10.110.0.11`.

If you are know how to do more beautiful solution, I'm ready for instructions/PR ;)

## License

MIT
