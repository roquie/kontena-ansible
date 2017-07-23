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
ansible-playbook -i inventory/your playbooks/start.yml --tags=docker
```

#### Install Kontena Agent on all hosts 

```
ansible-playbook -i inventory/your playbooks/start.yml --tags=kontena_agent
```

#### Install Kontena Server on all Master hosts 

```
ansible-playbook -i inventory/your playbooks/start.yml --tags=kontena_server
```

#### Install Docker & Kontena Master

```
ansible-playbook -i inventory/your playbooks/start.yml --limit=master
```

#### Install Docker & Kontena Agent (to nodes)

```
ansible-playbook -i inventory/your playbooks/start.yml --limit=nodes
```

#### Install Kontena CLI

```
ansible-playbook -i inventory/your playbooks/start.yml --limit=cli
```

## TODO

* [x] create separate repo for `kontena-server` role & register her to the ansible-galaxy
* [x] create separate repo for `kontena-agent` role & register her to the ansible-galaxy
* [ ] create separate repo for `kontena-cli` role & register her to the ansible-galaxy
* [x] write role for installing `kontena-cli` on GNU/Linux (yes, I'm so lazy for lift my fingers above the keyboard...)
* [ ] automatically uninstall all installed packages: `docker`, `kontena-master`, `kontena-node` and `kontena-cli`
* [ ] write tests (for `kontena-server` and `kontena-agent` they are ready)

## Supported OS

For now supports:
* Ubuntu 16.04 LTS
* Ubuntu 14.04 LTS

## Vagrant

* `cd /path/to/project`
* `ansible-galaxy install -r requirements.yml`
* `vagrant up` 

## License

MIT
