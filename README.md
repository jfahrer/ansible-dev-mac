# dev-mac
This project uses Ansible to create a ready-to-code macOS box (tested with High Sierra)!

There is no central machine that can talk to all macs. Instead the idea is to run the playbook manually on all machines.
New machines can be bootstrapped over ssh with a separate playbook.

## Execute the playbook
```sh
cd ~/workspace/ansible-dev-mac && ansible-playbook -K --limit $(hostname) dev-mac.yml
```

## Adding hosts
### Bootstrapping a blank machine
```sh
ansible-playbook -k -K -e "bootstrap_ip=10.0.1.24 bootstrap_user=julian osx_hostname=julians-wanelobook" bootstrap.yml
```
This will install Xcode, Homebrew and Ansible on a blank machine. It also generates ssh keys, clones the repos and copies the vault key over to the machine.

### Manually setting up a new machine
* Install Homebrew
  `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

* Install ansible
  `brew install ansible`

* Clone the repo
  `git clone https://github.com/jfahrer/ansible-dev-mac`

* Clone the credentials repo
  `git clone https://github.com/jfahrer/ansible-dev-mac-credentials`

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
  * rspec expectations cheat-sheet
* Sign in to chrome
* Setup 1password
* Enable shiftit
* Install todoist


## Installing requirements
```sh
ansible-galaxy install -r requirements.yml
```
Requirements are kept in the git repo to make the playbook work with `ansible-pull`
