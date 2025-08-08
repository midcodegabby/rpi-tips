### 1. Setting up the OS
- Download the Raspberry Pi Imager
- Flash the SD card with Raspberry Pi Os lite (64-bit)
- Plug in all peripherals and power

### 2. Initial configuration
#### Keyboard
rpi has default UK keyboard, so change it by running the following commands and options:
`sudo dpkg-reconfigure locales`
-> select en-US blah blah, then default, then reboot.
`sudo dpkg-reconfigure keyboard-configuration`
-> select `Generic 105-key PC`
-> select `Other`
-> select `English (US)`
-> select `English (US)`
-> reboot

#### Wifi
`sudo raspi-config`
-> `System Options>Wireless LAN`
- SSID = network name

#### Packages
```
sudo apt install vim fail2ban
sudo apt update
sudo apt upgrade
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
-> note what the ip address is, and try to ssh into the pi using <userid> and the password.

```
ssh-keygen -f ~/.ssh/id_rsa -t rsa -b 4096
scp -P <port> ~/.ssh/id_rsa.pub <userid>@<ipaddr>:~/.ssh/authorized_keys
cat > ~/.ssh/config << EOF
Host <servername>
	Hostname <sipaddr>
	User <userid>
	Port <x>
	IdentityFile ~/.ssh/id_rsa
EOF
```



#### Reference
`sudo netstat -tupan` 		shows active ports
`[CTRL]-V`                  tells the > shell to take all inputs literally (can use tabs)
