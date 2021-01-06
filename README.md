# Ansible task for setting up Mac book

# Environment
- macOS Catalina 10.15.7
- ansible 2.10.4

# Features 

## roles
  - **homebrew**
    - install package
  - **homebrew_cask**
    - install package
    - homebrew_cask module does not work for [the isse](https://github.com/geerlingguy/ansible-role-homebrew/issues/148), I create the task to install homebrew cask. Probably, it works if you upgrade the version of Ansible.
  - **mas**
    - [mas-cli](https://github.com/mas-cli/mas)
    - before using this role, you should sign into App Store manually.
    - `mas install` command will not allow you to install (or even purchase) an app for the first time: use the `mas purchase` command in that case. So, I made a task to purchase Mac app(mas_purchase_temp.yml).
  - **osx_defaults**
    - change setting of ScreenShot and Finder etc.
  - **zshconfig**
    - install [Prezto](https://github.com/sorin-ionescu/prezto) and [Powerlevel10k](https://github.com/romkatv/powerlevel10k)
    - After executing ansible playbook, you should use iTerm2 to set up themes.
      - If you use iTerm2, you can set up install font and congifure `.p10k.zsh` automatically.
  - **vscode**
    - setting keybinding and setting.json
    - Before executing this task, you should set to use `code` command.
      - [Visual Studio Code on macOS](https://code.visualstudio.com/docs/setup/mac)
    - For checking extensions of VScode installed your machine, you should excute this command: ` code --list-extensions` 
  - **git**
    - Configure `.gitignore` and `.gitconfig`
    - Set your user name, e-mail used in Github to `git_user` and `git_email` variables in `./groups_vars/local.yml`
  - **github**
    - generate ssh keys and register public key to Github by using access token for sshconnection.
    - Before executing this task, you should get Access token from Github.
      - [Creating a personal access token](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/creating-a-personal-access-token)
    - After executing this task, you should check to connect Github. Please execute command: `ssh -T git@github.com`
  - **anyenv**
    - install [anyenv](https://github.com/anyenv/anyenv), [anyenv-update](https://github.com/znz/anyenv-update) and [anyenv-git](https://github.com/znz/anyenv-git)
    - install anyenv plugins written in `./groups_vars/local.yml`.(Here, `nodenv` is only installed)

# Usage

## Before executing Ansible playbook

install homebrew and Ansible.
```
chmod 755 ./setting.sh
sh ./setting.sh
```

check to execute simple Ansible command
```
$ ansible -m ping localhost
```

Specify homebrew packages, Mac App, VScode extensions, git user name, e-mail for Github, Github Access token in  `./groups_vars/local.yml`.

For executing mas role, you should sign into the Mac App Store app manually.


## check if excuting playbook successfully

syntax-check and specify tags
```
ansible-playbook main.yml --syntax-check -t homebrew
```

dry-run and specify tags
```
ansible-playbook main.yml --check -t homebrew
```

## execute playbook

```
ansible-playbook main.yml 
```

# reference
- fork from https://github.com/kohbis/mac-ansible/tree/template

# Licence
MIT