## 1. Setting up the OS
- Download the Raspberry Pi Imager
- Flash the SD card with Raspberry Pi Os lite (64-bit)
- Plug in all peripherals and power

## 2. Initial configuration
#### Keyboard
rpi has default UK keyboard, so change it by running the following commands and options:
`sudo dpkg-reconfigure locales`
- Select en-US blah blah, then default, then reboot.
`sudo dpkg-reconfigure keyboard-configuration`
- Select `Generic 105-key PC`
- Select `Other`
- Select `English (US)`
- Select `English (US)`
- Reboot

#### Wifi
`sudo raspi-config`
- Select `System Options>Wireless LAN`
- SSID = network name

#### Packages
```
sudo apt install vim fail2ban rsyslog iptables
sudo apt update
sudo apt upgrade

sudo systemctl enable fail2ban
sudo systemctl enable rsyslog
```
 
#### SSH
```
sudo useradd -m <userid>
sudo usermod -a -G sudo <userid>
sudo passwd <userid>
sudo mkdir /home/<userid>/.ssh
sudo chown <userid>:<userid> /home/<userid>/.ssh
sudo systemctl restart ssh
sudo systemctl enable ssh
```
`ifconfig`
- Note what the ip address is, and try to ssh into the pi using <userid> and the password.

```
ssh-keygen -f ~/.ssh/id_rsa -t rsa -b 4096
scp -P <port> ~/.ssh/id_rsa.pub <userid>@<ipaddr>:~/.ssh/authorized_keys
printf "Host <servername>\n\tHostname <sipaddr>\n\tUser <userid>\n\tPort <x>\n\tIdentityFile ~/.ssh/id_rsa\n" >> ~/.ssh/config
```
#### Visual/Text
- Set default text editor to vim:
```
printf "export EDITOR='vim'\nexport VISUAL='vim'\nsource ~/.bashrc\n" >> ~/.bash_profile
source ~/.bash_profile
sudo update-alternatives --config editor
4
```

#### Security
- Setting up fail2ban:
```
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo vim /etc/fail2ban/jail.local 
    see my super secret file that is not here... ;) 
sudo systemctl start fail2ban
sudo fail2ban-client status
sudo fail2ban-client status sshd
```


## Reference
`sudo netstat -tupan` 		Shows active ports  
`[CTRL]-V`                  Tells the > shell to take all inputs literally (can use tabs)  
