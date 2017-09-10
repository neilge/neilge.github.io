---
title: note
date: 2017-08-22 07:15:07
visible: hide
tags: Note
---

# Notes

[toc]

## Desktop

### Log into desktop


```bash
ssh neilge.aka.corp.amazon.com
```


## GAMMA host

### Log into gamma server

```bash
ssh -L 8000:localhost:8000 neilge@neilge-gamma-1a-f7e07770.us-east-1.amazon.com
```

### Hostclass
NEILGE-GAMMA-1A

### Host name
neilge-gamma-1a-f7e07770.us-east-1.amazon.com

### Alias
neilge-platform-preprod.audible.com

### VIP
neilge-arya.iad.amazon.com

[VIP home site](https://vip-management.amazon.com/vipmgmt/ManageVips.mhtml)

### CName:

neilge-platform-preprod.audible.com -> neilge-arya-iad.iad.proxy.amazon.com 
neilge-platform-preprod.audible.ca -> neilge-arya-iad.iad.proxy.amazon.com 

## AmazonUIDevServer

### VIP

DNS name:
neilge-auiserver-gamma.iad.amazon.com

Proxy vip:
neilge-auiserver-gamma-iad.iad.proxy.amazon.com

[VIP home site](https://vip-management.amazon.com/vipmgmt/ManageVips.mhtml)

## Working on new package

1. ***Add a new pacakge***: `brazil ws --remove --package <Package Name> --branch <branch name>`
1. ***Override package***: Go the gamma environment, click edit next to Local override. In the Edit Local Overrides, add the new package as a new local override. Reactivate environment after that (In apollo, click the activate link or run `sudo /apollo/bin/runCommand -e HorizontePlatform -a Activate` in terminal of gamma stage).

2. ***Symlink to override tomcat jsps (views and tags)***:

	```bash
	sudo rm -rf /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/views/accountdetails && sudo ln -s /home/neilge/workspace/arya/src/AudibleWebAccountDetailsApplication/src/main/resources/WEB-INF/views/accountdetails /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/views/accountdetails && sudo rm -rf /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/tags/accountdetails && sudo ln -s /home/neilge/workspace/arya/src/AudibleWebAccountDetailsApplication/src/main/resources/WEB-INF/tags/accountdetails /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/tags/accountdetails
	```

	```bash
	sudo rm -rf /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/views/navigation && sudo ln -s /home/neilge/workspace/arya/src/AudibleWebNavigationApplication/src/main/resources/WEB-INF/views/navigation /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/views/navigation && sudo rm -rf /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/tags/navigation && sudo ln -s /home/neilge/workspace/arya/src/AudibleWebNavigationApplication/src/main/resources/WEB-INF/tags/navigation /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/tags/navigation
	```

3. ***Set jsp hotloading***: open `/local/apollo/var/env/HorizontePlatform/tomcat/conf/web.xml` in gamma and set `development=true`

4. ***Restart tomcat***:

	```bash
	sudo sudo -u nobody /apollo/bin/env /apollo/env/HorizontePlatform/bin/forceTomcatRestart
	```


## Changing backend code

1. ***Build the package in work space***: `brazil-build` the package, `brazil-build apollo-pkg` the package.
2. ***Sync the code from Desktop to Gamma***:

	```bash
	rsync -avz --delete /home/neilge/workspace/ neilge-gamma-1a-f7e07770.us-east-1.amazon.com:/home/neilge/workspace/
	```
3. ***Restart tomcat***:

	```bash
	sudo sudo -u nobody /apollo/bin/env /apollo/env/HorizontePlatform/bin/forceTomcatRestart
	```

## Changing the frontend code

Only need to do the 2, 3 steps of ***Changing backend code***


## Build a package into Gamma environment and sync to my gamma environment

Sometimes we need a updated package that has not been in Gamma yet, then we need mannually build this package into Our Gamma Environment (AudibleWebSite/ace) and sync to my gamma environment.

### Build package

* Go to [Package Builder](build.amazon.com), select the Version Set the package will be built in (in most of the cases is `AudibleWebsite/ace`).
* Select the package and proper branch and change in the package we want to add.
* Select Audo-merge Dependencies
* Submit Build Request

### Do a minimal deploy to my gamma

* Select mimimal deployment
* Select AudibleWebsite and choose the version you want to deploy
* Skip to review
* Create delpoyment

## Account info

### Audible account

* **Account**: youdavi+GoldAnnual1@amazon.com
* **Password**: test123

### Credit card info

* AMEX 372711340751041
* expires 10/19


## Useful Cli

### sync from version set

```bash
brazil ws --sync -md
```

### sync all the source in a workspace.

Sync all packages in workspace??

```bash
brazil ws --sync -src
```

### checkout a package

```bash
brazil ws use -p FirstCodeChangeListGit -b mainline
```

### remove a package

```bash
brazil ws --remove -p AudibleCombinedPurchaseHistoryLib
```

## Other info

### View in mobile model

Add `?referrerPlatform=wasabi` after the url


## Memo

When Bing vip to certificate

Choose Amazon CAM as team

AUIDS_HOST=neilge-gamma-1a-f7e07770.us-east-1.amazon.com brazil-build

AudibleMembershipSubscriptionApplication

AudibleAddressAndPaymentsLib
AudibleAddressAndPaymentsInterface

## Log
/apollo/env/HorizontePlatform/var/output/logs/
