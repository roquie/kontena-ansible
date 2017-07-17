# [Kontena](https://kontena.io/) Ansible

<br />

<p align="center">
    <a href="https://kontena.io/">
        <img src="https://kontena.io/images/kontena-logo.svg" width="280">
    </a>
</p>

<br />
<br />

This Ansible configs automatically installing `Kontena Master` and `Kontena Node`.

## Bug

For now, Kontena have a bug with Docker 17.x inside Kontena Agent service. Just does not service started.
So, if you want use `Kontena Master` and `Kontena Agent` services on same host, use `docker.io` docker version.
If master server does not have Kontena Agent service, you may install Docker 17.x.  

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

## TODO

* [ ] create separate repo for `kontena-master` role & register her to the ansible-galaxy
* [ ] create separate repo for `kontena-node` role & register her to the ansible-galaxy
* [ ] write role for installing `kontena-cli` on GNU/Linux
* [ ] write tests

## Support of OS

For now support only Ubuntu 16.04 LTS.

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
