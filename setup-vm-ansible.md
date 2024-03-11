# Ansible VM setup

## Proxmox Host

Clone Ubuntu Cloud Image template via web GUI

### Run as `root`

ssh into the VM from Proxmox shell

    ssh <USER>@<VM_HOSTNAME>

## VM

Add user `<USER>` to the groups `sudo`

    usermod -aG sudo <USER>

Become `<USER>`
    
    sudo su - <USER>

### Run as `<USER>`

Customize permissions to ~/.ssh

    chmod 700 ~/.ssh

Customize permissions to ~/.ssh/authorized_keys
    
    chmod 600 ~/.ssh/authorized_keys

Become root again

    exit

Edit SSH config

    nano /etc/ssh/sshd_config

Uncomment these lines and change them accordingly:

- Set `PubkeyAuthentication` to `yes` to enable login with public keys
- Set `PasswordAuthentication` to `no` to disable login with password

Restart SSH service

    systemctl restart ssh

Let all sudoers execute commands without needing a password

    sudo visudo

- Replace `%sudo   ALL=(ALL:ALL) ALL` with `%sudo   ALL=(ALL:ALL) NOPASSWD:ALL`

Save and exit with `Ctrl+X` and `y`

## Login via SSH as `<USER>`

    ssh <USER>@<IP_ADDRESS>

Install Starhip (https://starship.rs)

    curl -sS https://starship.rs/install.sh | sh

Install some tools

    apt install git stow neofetch

Remove default dotfiles

    rm -rf .bashrc .bash_aliases .hushlogin .gitconfig

Clone repositories from Github

    git clone https://github.com/funker/dotfiles.git ~/dotfiles
    git clone https://github.com/funker/docs.git ~/docs

Stow the dotfiles

    cd ~/dotfiles
    stow .

Restart the terminal




