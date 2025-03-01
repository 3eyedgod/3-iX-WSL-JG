# 3-iX-WSL-CC

[![IXSYSTEMS INC.](https://raw.githubusercontent.com/3eyedgod/3-iX-WSL-CC/main/IMAGES/iX_Logo.png)](https://www.ixsystems.com/)

## _Automation Scripts for TrueNAS Systems & Custom Servers_

These scripts are used for Client Configuration (CC) and Sofware Quality Control (SWQC) to configure and validate system configuration based on iX Redbooks & customer needs

- Automating Redbook Qualified Configuration
- Allowed for the increase in capacity without additional personel
- Log And Archive Configuration Results
- Gather System Information & Debug Files To Automate The SWQC Process

## Features

- Multi Script Menu
- WSL Based & Can Be Used With Any Windows System Running ([Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/about))
- Importing Multiple Hosts Using _KEY.txt_ File For Batch Configuration
- Supermicro Update Manager ([SUM](https://www.supermicro.com/en/solutions/management-software/supermicro-update-manager)) Intergration For Batch BIOS Configuration & [OOB/DCMS](https://store.supermicro.com/us_en/software/software-license-key-activation-usage) License Activation
- Added Logic For Error Checking And Accurate Results

## Dependencies

In order to run some scripts, Certain dependancies must be installed on the WSL Ubuntu VM:

- [[IPMITOOL]](https://linux.die.net/man/1/ipmitool) - Utility for controlling IPMI-enabled devices
- [[SSHPASS]](https://linux.die.net/man/1/sshpass) - Noninteractive ssh password provider
- [[PV]](https://linux.die.net/man/1/pv) - Monitor the progress of data through a pipe
- [[POSTGRESQL-CLIENT]](https://ubuntu.com/server/docs/databases-postgresql) - PostgreSQL (also known as Postgres) is an object-relational database system that has the features of traditional commercial database systems with enhancements to be found in next-generation database management systems (DBMS)
- [[SQLITE3]](https://linux.die.net/man/1/sqlite3) - A command line interface for SQLite version 3
- [[PYTHON]](https://www.python.org/downloads/) - Python is a programming language that lets you work more quickly and integrate your systems more effectively
- [[PDFGREP]](https://pdfgrep.org/) - A commandline utility to search text in PDF files
- [[LYNX]](https://linux.die.net/man/1/lynx) - A general purpose distributed information browser for the World Wide Web
- [[CURL]](https://linux.die.net/man/1/curl) - Transfer a URL
- [[GIT]](https://linux.die.net/man/1/git) - Git is a fast, scalable, distributed revision control system with an unusually rich command set that provides both high-level operations and full access to internals
- [[ZSH]](https://linux.die.net/man/1/zsh) - The Z shell

## Setup

[WSL](https://learn.microsoft.com/en-us/windows/wsl/install) must be installed on any Windows PC

Open up a PowerShell command prompt (Run as Administrator) & type the following:
```powershell
wsl --install
```

Once your Ubuntu user is setup update the repositories by typing the following:
```bash
sudo apt-get update && sudo apt-get full-upgrade -y
```

Install required dependancies with:
```bash
sudo apt install ipmitool sshpass pv postgresql-client sqlite3 python3 dialog pdfgrep lynx curl git zsh -y
```

Run the following command to install [oh-my-zsh](https://ohmyz.sh/)
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" -y
```

Copy theme over to [oh-my-zsh](https://ohmyz.sh/)
```bash
cp ~/3-iX-WSL-CC/SETUP/3eyedgod.zsh-theme ~/.oh-my-zsh/themes/
```

Changing theme on .zshrc file
```bash
sed -i 's/ZSH_THEME="robbyrussell"/ZSH_THEME="3eyedgod"/g' ~/.zshrc
```

Add the following aliases to .zshrc file
```zsh
alias ixcc="cd ~/3-iX-WSL-CC;./3-iX-CC.sh"
alias 1up="sudo hwclock -s && sudo apt-get update && sudo apt-get full-upgrade -y && sudo apt-get autoremove -y"
alias sums="cd ~/3-iX-WSL-CC/SUMS/"
alias oob="./sum -l OOB-LIC.txt -c ActivateProductKey"
alias dcms="./sum -l DCMS-LIC.txt -c ActivateProductKey"
```

Making alias using sed
```
sed -i '/alias ohmyzsh="mate ~\/.oh-my-zsh"/a alias 1up="sudo apt update && sudo apt full-upgrade -y && sudo apt autoremove -y"' ~/.zshrc
```

