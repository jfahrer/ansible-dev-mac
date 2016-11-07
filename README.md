# dev-mac
This project uses ansible to create a ready-to-code OS X box (tested with El Capitan)!

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

# TODO
* Setup the development user
* Setup postgres

## git-pir
We should make sure that /usr/local/bin exist and is writeable

## iterm-preferences
Add params to installl biplist
 - Don't install
 - use pip / easy_install
 - become or don't become