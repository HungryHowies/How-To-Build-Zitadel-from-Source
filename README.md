# How-To-Build-Zitadel-from-Source

Zitadel Build

The following Documentation is how to build Zitadel from source and customize it. 

Prerequisite:
```
Ubuntu 22.0.4   4 CPU and 4 GB RAM
CockroachDB Version 23.x.x completed
Nginx setup and working.
apt update && apt upgrade
timedatectl set-timezone America/Chicago
apt install net-tools
apt install mlocate
apt install make
network configurations (static IP Address & DNS)
Certificates are completed.
```
Login as root.

Navigate to home directory. 
```
cd /home
```
# Dependencies:

Install NodeJS Version-18 package and Dependency
```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
Install NodeJS.
```
apt install nodejs -y
```
Check Version
```
node –version
```
Install npm version-10.3.0 .
```
npm install -g npm@10.3.0
```
Check version.
```
npm --version
```
Install Yarn.
```
npm install --global yarn
```

Install Sass.
```
npm install -g sass
```
Find Sass.
```
which sass
```
Set Sass.
```
export PATH=$PATH:/usr/bin/sass
```
Install Buf.
```
npm install @bufbuild/buf
```
# Install GO

Get Go Package.
```
wget https://go.dev/dl/go1.21.6.linux-amd64.tar.gz
```
Unzip.
```
tar -xvf go1.21.6.linux-amd64.tar.gz
```
Move Go directory.
```
mv go /usr/local
```
Create file for GO env.
```
vi ~/.bash_profile
```
Set environment variables to the file.
```
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```
Apply changes.
```
source ~/.bash_profile
```
Check Version.
```
go version
```
#  Zitadel Source

Get Zitadel Release.

Depending what version is required, you can find them all here https://github.com/zitadel/zitadel/releases 
```
wget  https://github.com/zitadel/zitadel/archive/refs/tags/v2.42.10.tar.gz
```
Unzip package.
```
sudo tar -xvf  v2.42.10.tar.gz
```
Change Directory. 
```
cd /home/zitadel-2.42.10/
```

# Zitadel Modification 

Most of these files has a URL in them called https://zitadel.com/something/something/. This can be replace by any URL/URI/URN. 
I modified the following files with the discription shown in  "( )" states what was modified.
```
/home/zitadel-2.42.10/console/src/index.html (Browser Button && icon on tab)
/home/zitadel-2.42.10/console/src/assets/i18n/en.json (Most of all the text for the front end)
/home/zitadel-2.42.10/console/src/app/modules/header/header.component.html (documentation button)
/home/zitadel-2.42.10/console/src/app/modules/footer/footer.component.html (removed social link at the bottom of the page)
/home/zitadel-2.42.10/console/src/app/pages/home/home.component.html (UI Console called MORE SHORTCUTS section “ Get Started”)
/home/zitadel-2.42.10/console/src/app/utils/onboarding.ts ( YOUR ONBOARDING PROCESS) section
/home/zitadel-2.42.10/console/src/app/modules/header/header.component.html (icon on header)
/home/zitadel-2.42.10/console/src/app/pages/signedout/signedout.component.html  (logo above user login)
/home/zitadel-2.42.10/console/src/app/pages/users/user-list/user-list.component.html ( (i)  header redirect  in users page)
/home/zitadel-2.42.10/console/src/app/pages/projects/projects.component.html ( (i) external link correction)
/home/zitadel-2.42.10/console/src/app/pages/signedout/signedout.component.scss (logout size of image)
/home/zitadel-2.42.10/console/src/app/pages/orgs/org-members/org-members.component.html ( (i) external link correction)
/home/zitadel-2.42.10/console/src/app/pages/instance/instance-members/instance-members.component.html ( (i) external link correction)
/home/zitadel-2.42.10/console/src/app/modules/domains/domains.component.html ( (i) external link correction)
/home/zitadel-2.42.10/console/src/app/pages/users/user-detail/user-detail/user-detail.component.html ( (i) external link correction)
/home/zitadel-2.42.10/console/src/app/pages/projects/owned-projects/owned-project-detail/application-grid/application-grid.component.html ( (i) external link correction)
/home/zitadel-2.42.10/console/src/app/pages/projects/apps/app-detail/app-detail.component.html  ( (i) external link correction)
```

# Removing Console Buttons 

To modify or delete the Documentation button in the console. Navigate to this file.

```
vi /home/zitadel-2.42.10/console/src/app/modules/header/header.component.html
```
Remove/Edit the following lines 171 thru 173 as shown below, and save.
```
169    <span class="fill-space"></span>
170
171    <a class="doc-link" href="https://zitadel.com/docs" mat-stroked-button target="_blank">
172      {{ 'MENU.DOCUMENTATION' | translate }}
173    </a>
```
# Remove Social Links

To modify or delete the Social Links button in the console. Navigate to this file.

```
vi /home/zitadel-2.42.10/console/src/app/modules/footer/footer.component.html
```
Remove/Edit following lines are from 16 thru 30, and save.
```
16         <a target="_blank" rel="noreferrer" href="https://github.com/zitadel">
17          <i class="text-3xl lab la-github"></i>
18        </a>
19        <a target="_blank" rel="noreferrer" href="https://twitter.com/zitadel">
20          <fa-icon [icon]="faXTwitter" size="xl"></fa-icon>
21        </a>
22        <a target="_blank" rel="noreferrer" href="https://www.linkedin.com/company/zitadel/">
23          <i class="text-3xl lab la-linkedin"></i>
24        </a>
25        <a target="_blank" rel="noreferrer" href="https://zitadel.com/chat">
26          <i class="text-3xl lab la-discord"></i>
27        </a>
28        <a target="_blank" rel="noreferrer" href="https://www.youtube.com/channel/UCUAWJUNYaRn1yIVrZxEfsuA">
29          <i class="text-3xl lab la-youtube"></i>
30        </a>
```

Adjust the Makefile.

The Makefile should be located in Zitadel's home directory for the build. Example: /home/zitadel-2.42.10/
```
vi /home/zitadel-2.42.10/Makefile
```
Edit the following lines to match the package version download. This will be shown in the console after the build.
```
now := $(shell date --rfc-3339=seconds | sed 's/ /T/')
VERSION ?= v2.42.10                                  <---------- HERE
```
# Compile Zitadel 

Execute the Makefile.
```
root# make
```
Once completed then move the executable as shown.
```
mv zitadel  /usr/local/bin
```
Change Directory.
```
cd /usr/local/bin
```
Acquire the configurations files needed.

Get Zitadel's runtime configuration files (i.e.,"defaults.yaml && steps.yaml"). 

Those files are located here. (https://zitadel.com/docs/self-hosting/manage/configure)  

Edit the runtime configuration file/s as needed.
```
vi /usr/local/bin/defaults.yaml
```
Edit the database initialization file as needed.
```
vi /usr/local/bin/steps.yaml
```
The runtime configuration file/s can be in the same directory as zitadel's executable, if not make sure you adjust permissions and add the Full Path when starting Zitadel for the first time.
In this example I placed the runtime configuration file/s && Zitadel executable in the same directory this is shown below.
```
 /usr/local/bin
```
![image](https://github.com/HungryHowies/How-To-Build-Zitadel-from-Source/assets/22652276/0bdd3fcd-017c-4e9f-bcb4-4047a7e14011)



All configurations must to be made prior to starting Zitadel.

zitadel binary will read configuration from environment variables as shown below. 
```
zitadel start-from-init --config defaults.yaml --steps steps.yaml --masterkey "MasterkeyNeedsToHave32Characters" --tlsMode external
```
NOTE: This setup is configured with TCP/TLS && FQDN. 
Login and check configuration in the console that were made. If there are no issues, then CTRL -C.

# Zitadel Service

Create a service for Zitadel.

Make Zitadel service file.
```
vi /etc/systemd/system/zitadel.service
```
Add the following to zitadel.service file.  
```
[Unit]
Description=zitadel

[Service]
Type=simple
User=root
Group=root
EnvironmentFile=-/usr/local/bin/zitadel
ExecStart=/usr/local/bin/zitadel  start  --masterkey "MasterkeyNeedsToHave32Characters"  --tlsMode external
WorkingDirectory=/usr/local/bin/
Restart=always
Nice=19
LimitNOFILE=16384
# When stopping, how long to wait before giving up and sending SIGKILL?
# Keep in mind that SIGKILL on a process can cause data loss.
TimeoutStopSec=60

[Install]
WantedBy=multi-user.target
```
Reload services
```
systemctl daemon-reload
```
Start Zitadel with systemd
```
systemctl start zitadel
```

Revision #4
Created 27 January 2024 00:10:08 by Admin
Updated 27 January 2024 04:52:02 by Admin
