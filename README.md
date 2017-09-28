# dev-mac
This project uses ansible to create a ready-to-code OS X box (tested with Sierra)!

# Setting up a new machine
* Install XCode
  `xcode-select --install`

* Install Homebrew 
  `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

* Install ansible
  `brew install ansible`

* Clone the repo
```bash
git clone https://github.com/jfahrer/ansible-dev-mac dev-mac
```

* Add the vault password file
```bash
cd dev-mac
echo WHATEVER_THE_PASSWORD_IS > ./vault_pass.txt
```

# Manual steps
* Add alfred workflows
  * github (https://github.com/gharlan/alfred-github-workflow/releases)
  * stack overflow (https://github.com/deanishe/alfred-stackoverflow)
  * dash (via the integrations)
* Download dash docsets
  * docker
  * ansible
  * rails
  * ruby
  * rspec expectations cheatsheet
* Setup 1password

## git-pir
We should make sure that /usr/local/bin exist and is writeable


# TODO
* Setup the development user
  * github keys
* Setup postgres
* Move git-pair wrapper into the dotfiles
* fix iterm-preferences
* mouse repeat rate
