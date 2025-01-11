# LXbash
My best bash's ordinated in list and categories 

## Linux General
### Mounting & Unmounting

- Mounting `sudo mount /dev/sda1 /mnt/usb`
    
- UnMounting `sudo umount /media/usb`
    
* * *
- Deleting everything in a folder `sudo rm -rf /mnt/usb/*`

* * *

### Flashing

- Flash ISO  
    `sudo dd if=</pathISO> of="/pathUSB" bs=4M status=progress oflag=sync`

* * *

### SSH

- Connecting SSH
    `ssh username@local/publicIP`

    #### Hosting SSH

    -  Creating a key
    `ssh-keygen -t rsa -b 4096 -C "commentExample"`

    - Copying the content of the `id_rsa.pub` generated before and adding it to the `~/.ssh/authorized_keys` file on the server

    #### Disable Password Authentication on the Remote Server (Optional but recommended)

    - SSH into the server:
        ```linux
        ssh user@remote_host
        ```
    - Open the SSH configuration file in an editor (e.g., nano):

        ```linux
        sudo nano /etc/ssh/sshd_config
        ```
    - Ensure the following lines are set (you might need to uncomment them by removing the #):
        ```linux
        PasswordAuthentication no
        UsePAM no
        ```
        Save and exit the editor (in nano, press `Ctrl + X`, then `Y` to confirm, and `Enter` to save).

    - Restart SSH service to apply the changes:

        ```
        sudo systemctl restart sshd
        ```
    This will prevent users from logging in via passwords, forcing them to use SSH keys instead.
        
    
* * *

- Restart  
    `sudo reboot`

* * *

### Apache2

- Basic Commands  
    `sudo systemctl start apache2`  
    `sudo systemctl stop apache2`  
    `sudo systemctl reload apache2`

* * *

### SFTP

- Connection
    `sftp username@local/publicIP`

- Stopping Connection
    `exit`

#### SFTP file transfer

- Put (Transfer files Local -> Target)
    `put path/example`

- Get (Transfer files Target -> Local)
    `get path/example`

* * *

### Firewalls Commands

- Firewalld  
    `sudo systemctl stop firewalld`  
    `sudo systemctl start firewalld`  
    `sudo firewall-cmd --zone=public --add-port=NUMBERS/udp --permanent`
	`sudo firewall-cmd --list-ports`
	`sudo firewall-cmd --reload`

* * *

- WifiInfo  
    `ip addr`  
    `hostname -I`  
    `ifconfig`

* * *

### Wifi & Ip

- PublicWifiInfo  
    `curl -s http://tnx.nl/ip`  
    `dig ANY +short @resolver2.opendns.com myip.opendns.com`
    
- Startup Service
    
    1.  Enable and start the service for your user. This ensures that the service starts automatically.  
        `systemctl --user enable example.service`  
        `systemctl --user start example.service`
        
    2.  Check the Service:  
        Verify that the Syncthing service is running:  
        `systemctl --user status syncthing.service`
        

* * *

### Bluethoot

Install Bluetooth drivers `sudo pacman -S --needed bluez bluez-utils`  
Start till next reboot/power off system `sudo systemctl start bluetooth`  
Enable to start on booting the machine (permanent) `sudo systemctl enable bluetooth`

* * *

### KDE Connect

### UFW

```
sudo ufw allow 1714:1764/udp
sudo ufw allow 1714:1764/tcp
sudo ufw reload
```
### Firewalld

```
sudo firewall-cmd --permanent --zone=public --add-service=kdeconnect
sudo firewall-cmd --reload
```

* * *

### File Convertion

- Install ffmpeg `sudo pacman -S ffmpeg`
- Convert Example
    
    ```
    ffmpeg -i input.mp4 -vn -acodec copy output.m4a
    ```
    
    **Breakdown of the command**  
    `-i input.mp4` Specifies the input file.  
    `-vn` Ignores the video stream.  
    `-acodec copy` Copies the audio stream without re-encoding it.  
    `output.m4a` Specifies the output file.
    - Check for supported formats and codecs  
        `ffmpeg -formats`  
        `ffmpeg -codecs`

* * *

### File Encrypyion (OpenSSL)
- Crypting a file `openssl enc -aes-256-cbc -salt -pbkdf2 -in "/path/where/is/file/to/encrypt.extension" -out "path/to/export/file.enc" -pass pass:Password123`
- Decrypting a file `openssl enc -d -aes-256-cbc -pbkdf2 -in "/path/where/is/file/to/decrypt.enc" -out "path/to/export/file.extension" -pass pass:Password123`

* * *

### Installing nvidia GUI controls

- Installing `sudo pacman -S nvidia-settings`

* * *

### Kill Command

- SIGHUP (Signal 1):
    
    - Description: Hang up detected on controlling terminal or death of controlling process.
    - Usage: Often used to reload configuration files without restarting the process.
    - Esample `sudo kill 1 PID`
- SIGINT (Signal 2):
    
    - Description: Interrupt from the keyboard (like pressing Ctrl + C).
    - Usage: Used to interrupt and terminate a process.
    - Esample `sudo kill 2 PID`
- SIGQUIT (Signal 3):
    
    - Description: Quit from keyboard (like pressing Ctrl + ).
    - Usage: Generates a core dump and terminates the process.
    - Esample \`\`
- SIGILL (Signal 4):
    
    - Description: Illegal Instruction.
    - Usage: Sent when a process attempts to execute an invalid or illegal machine instruction.  
        Esample `sudo kill 4 PID`
- SIGABRT (Signal 6):
    
    - Description: Abort signal from abort(3).
    - Usage: Usually sent by the process itself when it calls the abort function, often used for debugging.
    - Esample `sudo kill 6 PID`
- SIGFPE (Signal 8):
    
    - Description: Floating-point exception.
    - Usage: Sent when a process performs an illegal mathematical operation, like division by zero.
    - Esample `sudo kill 8 PID`
- SIGKILL (Signal 9):
    
    - Description: Kill signal.
    - Usage: Forces the immediate termination of the process. Cannot be caught, blocked, or ignored.
    - Esample `sudo kill 9 PID`
- SIGSEGV (Signal 11):
    
    - Description: Invalid memory reference (segmentation fault).
    - Usage: Sent when a process tries to access memory that it's not allowed to.
    - Esample `sudo kill 11 PID`
- SIGPIPE (Signal 13):
    
    - Description: Broken pipe.
    - Usage: Sent when a process writes to a pipe that has no readers.
    - Esample `sudo kill 13 PID`
- SIGALRM (Signal 14):
    
    - Description: Timer signal from alarm(2).
    - Usage: Used to signal the expiration of a timer set by the alarm function.
    - Esample `sudo kill 14 PID`
- SIGTERM (Signal 15):
    
    - Description: Termination signal.
    - Usage: Requests the process to terminate. Can be caught and handled by the process for graceful shutdown.
    - Esample `sudo kill 15 PID`
- SIGUSR1 (Signal 10) and SIGUSR2 (Signal 12):
    
    - Description: User-defined signals 1 and 2.
    - Usage: Used for application-specific purposes.
    - Esample `sudo kill 12 PID`
- SIGCHLD (Signal 17):
    
    - Description: Child stopped or terminated.
    - Usage: Sent to a parent process when one of its child processes terminates or stops.
    - Esample `sudo kill 17 PID`
- SIGCONT (Signal 18):
    
    - Description: Continue executing, if stopped.
    - Usage: Resumes a process that was stopped (e.g., by SIGSTOP or SIGTSTP).
    - Esample `sudo kill 18 PID`
- SIGSTOP (Signal 19):
    
    - Description: Stop process.
    - Usage: Stops (pauses) a process. Cannot be caught or ignored.
    - Esample `sudo kill 19 PID`
- SIGTSTP (Signal 20):
    
    - Description: Stop typed at terminal (like pressing Ctrl + Z).
    - Usage: Stops (pauses) a process but can be caught and handled by the process.
    - Esample `sudo kill 20 PID`
- SIGTTIN (Signal 21):
    
    - Description: Background process attempting read.
    - Usage: Sent when a background process tries to read from the terminal.
    - Esample `sudo kill 21 PID`
- SIGTTOU (Signal 22):
    
    - Description: Background process attempting write.
    - Usage: Sent when a background process tries to write to the terminal.
    - Esample `sudo kill 22 PID`
- SIGPOLL (Signal 29):
    
    - Description: Pollable event (Sys V).
    - Usage: Used for asynchronous I/O events.
    - Esample `sudo kill 29 PID`
- SIGXFSZ (Signal 25):
    
    - Description: File size limit exceeded.
    - Usage: Sent when a process exceeds the maximum allowed file size.
    - Esample `sudo kill 25 PID`

* * *

### CLI system monitor + PID

- Command `sudo top` to exit use CTRL + C

* * *
### WGet
- Fetch Online Files `wget https://.....extension -O name.exetension`
***
### Btop
CLI command to the system monitor `btop`
***
### Nmap
Show you all the open ports on your device `nmap localhost`
Show you all the open ports on the ip device `nmap 'ip'`
***
### Docker
The command need to be done when in the same folder as the docker.yml
- Open a docker in detached mode `sudo docker-compose up -d`
  - It means detached `-d`
- Close a docker in detached mode `sudo docker-compose down`

Install [Docker](https://linuxiac.com/how-to-install-docker-on-raspberry-pi/)
***
### RClone

Start nextcloud RClone `rclone mount NextcloudPI: ~/mnt/nextcloud --vfs-cache-mode full --no-check-certificate &`



## Arch

### Pacman

- App list `pacman -Qe`
- Uninstall `pacman -Rsn example`

## Nextcloud
### Trusted Domains
Usually `/var/www/html/nextcloud/config/config.php`
Or where you put the nextcloud installation

### HTTPS connection (Certbot Plugin Apache)
[Website Certbot](https://certbot.eff.org/)

1. Install Certbot
`sudo apt install certbot`

2. Install the plugin for apache
`sudo apt install python3-certbot-apache`

3. Obtain the certificate
`sudo certbot --apache`

## Git

- Cloning repos `git clone -b BranchName --single-branch https://github.com/username/mainProjectName.git`
- Stage changes `git add .`
- Commit `git commit -m "Your commit message here"`
- Push `git push origin BranchName`
- Initialiaze a new repo `git init` 


## DiscordTokenGrabber (by [ITZNEXUS](https://github.com/NotNexuss/Get-Discord-Token))

```javascript
// CODE BY ITZNEXUS
(webpackChunkdiscord_app.push([[''],{},e=>{m=[];for(let c in e.c)m.push(e.c[c])}]),m).find(m=>m?.exports?.default?.getToken!==void 0).exports.default.getToken()
// HOW TO
// If copied, go to discord (browser version) and press "CTRL+SHIFT+I" on your keyboard, if that doesn't work, click on the three dots on upright corner. Then hover on more tools and hover your cursor over "Developer Tools". then open console tab. While it's open, paste the code that we copied. 
```
## Linux Spotify Patcher (by [SpotX-Bash](https://github.com/SpotX-Official/SpotX-Bash))
```
bash <(curl -sSL https://spotx-official.github.io/run.sh)
```
- By default...
  - all supported experimental features are enabled
  - free-tier user patches are applied, paid-premium users should use  `-p` / `--premium` flag
  - macOS client auto-updates are NOT disabled, block auto-updates with `-B` / `--blockupdates` flag
- View additional flags/options and examples in the `Options` section below
- For more information, see the [FAQ](https://github.com/SpotX-Official/SpotX-Bash/wiki/SpotX%E2%80%90Bash-FAQ)

### Options:
<details>
  <summary>Click to expand!</summary>

| Option | Description |  
| --- | --- |  
| `-B` | block client auto-updates [macOS] |  
| `-c` | clear client app cache |  
| `-d` | enable [developer mode](https://github.com/SpotX-Official/SpotX-Bash/wiki/SpotX%E2%80%90Bash-FAQ#what-is-developer-mode) |  
| `-e` | exclude all experimental features |  
| `-f` | force SpotX-Bash to run |  
| `-h` | hide non-music on home screen |  
| `--help` | print options |  
| `-i` | enable interactive mode | 
| `--installdeb` | install latest client deb pkg on APT-based distros [Linux] |   
| `--installmac` | install latest supported client [macOS] |  
| `-l` | [set lyrics background color to black](https://github.com/SpotX-Official/SpotX-Bash/issues/20#issuecomment-1762040019) |  
| `--nocolor` | remove colors from SpotX-Bash output |  
| `-o` | use [old home screen UI](https://github.com/SpotX-Official/SpotX-Bash/wiki/SpotX%E2%80%90Bash-FAQ#what-is-the-old-and-new-ui) |  
| `-p` | [paid premium-tier subscriber](https://github.com/SpotX-Official/SpotX-Bash/wiki/SpotX%E2%80%90Bash-FAQ#can-spotx-bash-be-used-with-a-paid-premium-account) |  
| `-P <path>` | set path to client |  
| `-S` | skip [codesigning](https://github.com/SpotX-Official/SpotX-Bash/discussions/3) [macOS] | 
| `--stable` | use with '--installdeb' for stable branch [Linux] |   
| `--uninstall` | uninstall SpotX-Bash |  
| `-v` | print SpotX-Bash version |  
| `-V <version>` | install client version [macOS] |  

**Examples:**

**Run SpotX-Bash, clear app cache, enable dev mode, hide non-music categories** 
```
bash <(curl -sSL https://spotx-official.github.io/run.sh) -cdh
```
**Run SpotX-Bash, enable interactive mode, set custom path to client** 
```
bash <(curl -sSL https://spotx-official.github.io/run.sh) -i -P $HOME/Downloads/
```
**Run SpotX-Bash, set paid premium-tier subscriber** 
```
bash <(curl -sSL https://spotx-official.github.io/run.sh) -p
```
**Run SpotX-Bash, install latest testing branch client version (Linux)** 
```
bash <(curl -sSL https://spotx-official.github.io/run.sh) --installdeb
```
**Run SpotX-Bash, block auto-updates, install latest supported client version (macOS)** 
```
bash <(curl -sSL https://spotx-official.github.io/run.sh) -B --installmac
```
</details>

### Thanks:

- [amd64fox](https://github.com/amd64fox/) of [SpotX](https://github.com/SpotX-Official/SpotX)

## Termux
### Termux Settings
#### Change terminal font
Just copy your TTF/OTF font file in the `~/.termux/font.ttf` directory and reload
	```
 	cp path/to/font/ttf/otf ~/.termux/font.ttf
  	termux-reload-settings
	```
# Neovim
## Neovim for devs
### Installing plugin manager
1. Use this `curl` command to get the plugin on your device
2. Create the `.config/nvim` folder and the config file using `nano`
```
mkdir -p ~/.config/nvim
sudo nano ~/.config/nvim/init.vim
```
3. When inside the `init.vim` write this
   ```
   " Initialize vim-plug
     call plug#begin('~/.local/share/nvim/plugged')

     " Add your plugins here, for example:
     Plug 'tpope/vim-sensible'

     call plug#end()
   ```
4. Now open neovim with `nvim` and use `:PlugInstall` to install plugin added with `call plug#begin()` or `call plug#end()`
  
