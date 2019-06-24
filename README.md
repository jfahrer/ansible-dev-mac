# dev-mac
This project uses Ansible to create a ready-to-code macOS box (tested with High Sierra)!

There is no central machine that can talk to all macs. Instead the idea is to run the playbook manually on all machines.
New machines can be bootstrapped over ssh with a separate playbook.

## Execute the playbook
```sh
cd ~/workspace/ansible-dev-mac && ansible-playbook -K --limit $(hostname) dev-mac.yml
```

#### Update settings and secrets only
```sh
cd ~/workspace/ansible-dev-mac && ansible-playbook -K --limit $(hostname) --tags settings dev-mac.yml
```

#### Install Ruby versions and gems only
```sh
cd ~/workspace/ansible-dev-mac && ansible-playbook -K --limit $(hostname) --tags ruby dev-mac.yml
```

#### Install brew packages and vim plugins
```sh
cd ~/workspace/ansible-dev-mac && ansible-playbook -K --limit $(hostname) --tags software dev-mac.yml
```

## Adding hosts
Add the new host to the inventory. You should use whatever `hostname` returns for your machine as the name in the inventory. Ansible will talk to the host via a `local` connection. Also make sure to set the `osx_hostname` variable in the host specific vars files. Otherwise we will set the hostname of the machine to whatever `inventory_hostname` returns.

### Bootstrapping a blank machine
```sh
ansible-playbook -k -K -e "bootstrap_ip=10.0.1.24 bootstrap_user=julian osx_hostname=julians-wanelobook" bootstrap.yml
```
This will install Xcode, Homebrew and Ansible on a blank machine. It also generates ssh keys, clones the Ansible and secrets repos and copies the vault key over to the machine.

You can override the secrets repo that will be used with `-e "ansible_repos_credential_repo_url=ssh://git@github.com/jfahrer/ansible-dev-mac-secrets.git"`
You can set `ansible_repos_vault_password_file` to use a custom file for the vault password that will transferred to the host.

### Manually setting up a new machine
* Install Homebrew
  `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

* Install ansible
  `brew install ansible`

* Clone the repo
  `git clone https://github.com/jfahrer/ansible-dev-mac`

* Clone the secrets repo
  `git clone https://github.com/jfahrer/ansible-dev-mac-secrets`

* Setup the vault password
  `cd ansible-dev-mac && echo WHATEVER_THE_VAULT_KEY_IS > vault_password.txt`

## Manual steps after running the playbook
* Show remaining battery in %
* Set modifier key for caps to control
* Increase key repeat rate and delay
* Remove the shortcuts C-up/down/left/right that are mapped to Mission Control
* Add alfred workflows
  * github (https://github.com/gharlan/alfred-github-workflow/releases)
  * stack overflow (https://github.com/deanishe/alfred-stackoverflow)
  * dash (via the integrations)
* Download dash docsets
  * docker
  * ansible
  * rails
  * ruby
  * elixir
  * bootstrap
  * rspec expectations cheat-sheet
* Sign in to chrome
* Setup 1password
* Enable shiftit
* Install Todoist, Bear, Shush and Healthier from the AppStore


## Installing requirements
```sh
ansible-galaxy install -r requirements.yml
```
Requirements are kept in the git repo to make the playbook work with `ansible-pull`
