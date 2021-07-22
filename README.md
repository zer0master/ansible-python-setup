# ansible-python-setup
Role to ensure python and specified modules are installed system-wide

## Background

This role is used for several setups in my home lab; you may find it useful. The following assumptions are in play:
* any modules specified are installed system-wide as root
* `python3` usage is assumed
* `pip3` is installed and then upgraded via `ansible.builtin.pip`
* define anything else via `extra_modules`

## Prerequisites

Ubuntu 20 installed. Anything beyond `pip3` should be supplie using the typical ansible variable mechanisms, subject to precedence. I tend to use a custom inventory file in the repo base; you're free to chart your own path.

Though it wasn't as obvious as I'd hoped, the following command is needed to create the correct role structure or any attempt to install it using galaxy later will fail in spite of a correctly formatted `requirements.yml` in the repo base. The command involved turned out to be:
```
$ ansible-galaxy role init --offline -vvvv --init-path ansible-python-setup python-setup
```
Using `--offline` foregoes trying to create a role in the official Galaxy directory, along with the use of API keys and such.

The `certupdate_nginx/meta/main.yml` file then needs to be fleshed out to at least a minimum level. At that point the working tasks and other sundries can be populated in the repo and re-used, assuming things are reasonably thought out.

## Usage

To use this in the context of a playbook, add the following section to `requirements.yml`, setting the name to a more user-friendly value (eg., `python-setup`) if you like:
```
- name: python-setup
  src: git+https://github.com/zer0master/ansible-python-setup.git
  scm: git
```
Use that same name value under your `roles` key in your playbook, then install the role(s) with:
```
ansible-galaxy role install -vv --role-file requirements.yml --roles-path roles/
```

## TODOs

.
