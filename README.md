# How-To-Build-Zitadel-from-Source

Zitadel Build
The following Documentation is how to build Zitadel from source.

Building and upgrades,

Prerequisite:
```
Ubuntu 22.0.4   4 CPU and 16 GB RAM
CockroachDB Version 23.x.x completed
Nginx setup and working.
apt update && apt upgrade
timedatectl set-timezone America/Chicago
apt install net-tools
apt install mlocate
apt install make
network configurations (static IP Address & DNS)
```
Login as root, go to home directory.

Navigate to home directory. 
```
cd /home
```
Dependencies:
```
### Installing NodeJS-18.x first before npm. If not, it will install an incompatible version of Node ###
```
Install NodeJS Version-18 package.
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
Installing npm this is a package manager for the JavaScript programming language maintained by npm.
```
apt install npm
```
Ensure npm version-10.3.0 is installed.
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
Install Angular.
```
npm install @angular/animations@16.2.5
```
Install Sass.
```
npm install -g sass
```
Find where Sass is located.
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
Install Zitadel 
Get Zitadel Release Open Source Code
```
wget  https://github.com/zitadel/zitadel/archive/refs/tags/v2.42.10.tar.gz
```
Unzip package
```
sudo tar -xvf  v2.42.10.tar.gz
```
Change Directory 
```
cd /home/zitadel-2.42.10/
```
Install GO
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
Create file.
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
Zitadel Modification 

These files favicon.ico and favicon.png to replace browser tab icon.  There located in directory  /home/zitadel-2.42.10/.

Files that need to be modified. Each one of these files has URL called https://zitadel.com/something/something/. This can be replace by any URL/URI/URN. 
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
```
NOTE: Logo Size Increase. For some reason  when running MAKE it writes over this file.
```
/home/zitadel-2.42.10/internal/api/ui/login/static/resources/themes/zitadel/css/zitadel.css ( size  logo increase)
```
Removing Console Buttons 

Documentation button navigate to this file.
```
vi /home/zitadel-2.42.10/console/src/app/modules/header/header.component.html
```
Removal lines 171 thru 173 as shown below, remove and save.
```
169    <span class="fill-space"></span>
170
171    <a class="doc-link" href="https://zitadel.com/docs" mat-stroked-button target="_blank">
172      {{ 'MENU.DOCUMENTATION' | translate }}
173    </a>
```
Remove Social Links

Remove the social link  modify this file
```
vi /home/zitadel-2.42.10/console/src/app/modules/footer/footer.component.html
```
Remove these lines. They are from 16  thru 30.
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
Rest of the files need the URL replaced from zitadel.com to any URL/URI/URN or none.

Adjust the Makefile
The Makefile should be located in Zitadel's home directory for the build /home/zitadel-2.42.10/
```
vi /home/zitadel-2.42.10/Makefile
```
Edit the following lines to match the package version download. This will be shown in the console.
```
now := $(shell date --rfc-3339=seconds | sed 's/ /T/')
VERSION ?= v2.42.10                                  <---------- HERE
```
Compile Zitadel 

Execute the Makefile.
```
root# make
```
Once completed move executable.
```
mv zitadel  /usr/local/bin
```
Change Directory.
```
cd /usr/local/bin
```
Acquire the configurations files needed.

Copy and paste from Zitadel Doc’s  "defaults.yaml && steps.yaml" . You can find these files here. 

 (https://zitadel.com/docs/self-hosting/manage/configure) 

Create runtime configuration file and then add the configuration.
```
vi /home/zitadel-2.42.10/defaults.yaml
```
Create database initialization file and then add the configuration.
```
vi /home/zitadel-2.42.10/steps.yaml
```
Ensure these files are in this directory.  
```
 /usr/local/bin
```
All configurations must to be made prior to starting Zitadel.

When files “defaults.yaml && steps.yaml“ are completed then execute the following command.
```
Root# zitadel start-from-init --config defaults.yaml --steps steps.yaml --masterkey "MasterkeyNeedsToHave32Characters" --tlsMode external
```
Depending on the version you may see some WARN signs.  The error below shown means  it can not find SMTP config, because I didn't create one.
```
Level=warning msg="process events failed" caller="/home/zitadel-2.42.11/internal/eventstore/
Level=warning msg="missing translation" args="map
ID=QUERY-fwofw Message=Errors.SMTPConfig.NotFound Parent=(sql: no rows in result set)" projection=projections.notifications
```
Login and check configuration in the console that were made. If there are no issues, then CTRL -C and create a service for Zitadel.

Zitadel Service

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
TimeoutStopSec=infinity

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

Upgrade Zitadel
Overview: 

Follow the above steps to build new version of Zitadel. Download the new version, copy any configuration files that were modify in the previous Zitadel version to the new Zitadel version, build/configure using the Makefile, stop Zitadel service, remove old executable OR copy new Zitadel executable over the old executable in this working directory.( /usr/local/bin/). 

The only difference is copying the modified configuration files previously before the build and the executable file "Zitadel" will replace the old one in directory ( /usr/local/bin).

Files that should be copied over are shown below. Navigate to Zitadel current version.
```
cd /home/zitadel-2.42.10/
```
Copy files over to new version.
```
cp console/src/index.html  /home/ zitadel-2.42.11/console/src/index.html 
cp console/src/assets/i18n/en.json  /home/ zitadel-2.42.11/console/src/assets/i18n/en.json 
cp console/src/app/modules/header/header.component.html  /home/ zitadel-2.42.11/console/src/app/modules/header/header.component.html
cp console/src/app/modules/footer/footer.component.html  /home/ zitadel-2.42.11/console/src/app/modules/footer/footer.component.html 
cp console/src/app/pages/home/home.component.html  /home/ zitadel-2.42.11/console/src/app/pages/home/home.component.html 
cp console/src/app/utils/onboarding.ts  /home/ zitadel-2.42.11/console/src/app/utils/onboarding.ts  
cp console/src/app/pages/users/user-list/user-list.component.html /home/ zitadel-2.42.11/console/src/app/pages/users/user-list/user-list.component.html
cp console/src/app/pages/signedout/signedout.component.html /home/zitadel-2.42.11/console/src/app/pages/signedout/signedout.component.html 
cp console/src/app/pages/users/user-list/user-list.component.html /home/zitadel-2.42.11/console/src/app/pages/users/user-list/user-list.component.html
cp console/src/app/pages/projects/projects.component.html /home/zitadel-2.42.11/console/src/app/pages/projects/projects.component.html
cp console/src/app/pages/orgs/org-members/org-members.component.html /home/zitadel-2.42.11/console/src/app/pages/orgs/org-members/org-members.component.html
cp console/src/app/pages/instance/instance-members/instance-members.component.html /home/zitadel-2.42.11/console/src/app/pages/instance/instance-members/instance-members.component.html 
cp console/src/app/modules/domains/domains.component.html /home/zitadel-2.42.11/console/src/app/modules/domains/domains.component.html
cp console/src/app/modules/domains/domains.component.html /home/zitadel-2.42.11/console/src/app/pages/users/user-detail/user-detail/user-detail.component.html 
```
The Makefile should be located in Zitadel's home directory for the new build (/home/zitadel-2.42.11).
```
vi /home/zitadel-2.42.11/Makefile
```
Edit the following lines to match the package version download. This will be shown in the console when finished.
```
now := $(shell date --rfc-3339=seconds | sed 's/ /T/')
VERSION ?= v2.42.11                                  <---------- HERE
```
Stop Zitadel service
```
systemctl stop zitadel
```
Copy new Zitadel version executable made to the working directory. You can either remove the old Zitadel executable or copy over the old one.
```
cp  /home/zitadel-2.42.11/zitadel /usr/local/bin/zitadel
```
Update tables.
```
Root # zitadel setup   --config defaults.yaml --steps steps.yaml --masterkey "MasterkeyNeedsToHave32Characters"  --tlsMode external
```
Start  Zitadel service 
```
systemctl start zitadel
```
Organizing Home directory for future Upgrades.
Using the Home directory, I have different version downloaded. Each one has an executable file for that version. 

![image](https://github.com/HungryHowies/How-To-Build-Zitadel-from-Source/assets/22652276/04ffd46a-e22f-4afe-8d54-8f643981205d)





Revision #4
Created 27 January 2024 00:10:08 by Admin
Updated 27 January 2024 04:52:02 by Admin
