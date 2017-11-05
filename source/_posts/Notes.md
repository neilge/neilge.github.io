---
title: Note
date: 2017-08-22 07:15:07
visible: hide
tags: Note
password: tswc941=
---

[toc]

# Notes

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

#### DNS Name: 

neilge-arya.iad.amazon.com

#### Proxy

neilge-arya-iad.iad.proxy.amazon.com

[VIP home site](https://vip-management.amazon.com/vipmgmt/ManageVips.mhtml)

### CName:

* neilge-platform-preprod.audible.com -> neilge-arya-iad.iad.proxy.amazon.com 
* neilge-platform-preprod.audible.ca -> neilge-arya-iad.iad.proxy.amazon.com 

## AmazonUIDevServer

### VIP

DNS name:
neilge-auiserver-gamma.iad.amazon.com

Proxy vip:
neilge-auiserver-gamma-iad.iad.proxy.amazon.com

[VIP home site](https://vip-management.amazon.com/vipmgmt/ManageVips.mhtml)


ssh into your gamma and go to folder '/apollo/env/HorizontePlatform/brazil-config/global'

edit AmazonUIAssetInjector.cfg

/apollo/env/HorizontePlatform/brazil-config/global/AmazonUIAssetInjector.cfg

For 

`*.*.BSFSRHttpConnectionInfo.AUIDevServerBase`

and
 
`*.*.BSFSRHttpConnectionInfo.AUIDevServer` 

make sure the 

`servers = neilge-auiserver-gamma.iad.amazon.com`

### To rsync the built assets to another host's DevServer environment

`AUIDS_HOST=neilge-gamma-1a-f7e07770.us-east-1.amazon.com brazil-build dev`

If you want to keep update the change in code, use `--guard`

`AUIDS_HOST=neilge-gamma-1a-f7e07770.us-east-1.amazon.com brazil-build dev --guard`


## Working on new workspace and package

1. ***Add a new workspace and pacakge***: 

	```
	brazil workspace create --name <WorkspaceName> --versionSet <VersionSetName>
	cd <WorkspaceName> 
	kinit -f 
	brazil workspace use --package <PackageName>
	```
	```
	brazil ws use -vs ...
	brazil ws use -p ...
	brazil ws remove -p ...
	```


2. ***Delete a package***
`brazil ws --remove --package <Package Name> --branch <branch name>`
1. ***Override package***: Go the gamma environment, click edit next to Local override. In the Edit Local Overrides, add the new package as a new local override. Reactivate environment after that (In apollo, click the activate link or run `sudo /apollo/bin/runCommand -e HorizontePlatform -a Activate` in terminal of gamma stage).

2. ***Symlink to override tomcat jsps (views and tags)***:

	```bash
	sudo rm -rf /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/views/accountdetails && sudo ln -s /home/neilge/workspace/arya/src/AudibleWebAccountDetailsApplication/src/main/resources/WEB-INF/views/accountdetails /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/views/accountdetails && sudo rm -rf /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/tags/accountdetails && sudo ln -s /home/neilge/workspace/arya/src/AudibleWebAccountDetailsApplication/src/main/resources/WEB-INF/tags/accountdetails /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/tags/accountdetails
	```

	```bash
	sudo rm -rf /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/views/navigation && sudo ln -s /home/neilge/workspace/arya/src/AudibleWebNavigationApplication/src/main/resources/WEB-INF/views/navigation /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/views/navigation && sudo rm -rf /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/tags/navigation && sudo ln -s /home/neilge/workspace/arya/src/AudibleWebNavigationApplication/src/main/resources/WEB-INF/tags/navigation /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/tags/navigation
	```
	
	```bash
	sudo rm -rf /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/views/paymentswidget && sudo ln -s /home/neilge/workspace/arya/src/AudiblePaymentsWidgetApplication/src/main/resources/WEB-INF/views/paymentswidget /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/views/paymentswidget && sudo rm -rf /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/tags/paymentswidget && sudo ln -s /home/neilge/workspace/arya/src/AudiblePaymentsWidgetApplication/src/main/resources/WEB-INF/tags/paymentswidget /apollo/env/HorizontePlatform/var/tomcat/webapps/HorizonteWebApp/WEB-INF/tags/paymentswidget
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


## Using Symphony to copy a new placement

1. Select a placement you want to copy and click into it.
2. Click option and select **Copy to Clipboard**
3. Go back to campaign page where you want to add this placement
4. Click Add Placementn and select **Paste From Clipboard**
5. The page will be redirect to adding new placement page
6. Select the site you want to choose, CA or US
7. Click **Override** in Type and make sure type is guaranteed and 100%
8. In the page targeting section, make sure the Browse Node value is the page Id we set in the code.

## About the country

1. In symphony we can select country when we create a placement
2. We can also change the content shows in different country by using LMS


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

### View in mobile mode

Add `?referrerPlatform=wasabi` after the url

### Turn on debug mode

Add `?debug=1` after the url



## Memo

When Bing vip to certificate

Choose Amazon CAM as team


AudibleMembershipSubscriptionApplication

AudibleAddressAndPaymentsLib
AudibleAddressAndPaymentsInterface

## Log
/apollo/env/HorizontePlatform/var/output/logs/


### Timber. Run on desktop** 

* /apollo/env/envImprovement/bin/sshenv -e TimberFS/IAD/Audible

### Find files contains the log 
find -name \*.gz -print0 | xargs -0 zgrep "No configuration found for service: AudibleCustomerOnboardingService, realm: CAAMAZON

## String tools

There is a old string manager: audible-strings.amazon.com. If the translator cannot find the associated value for a specific key in current market, it will go to audible-strings.amazon.com to fetch data.

## Weblab

A tool can help us to gradually dialed up the percentage of a page. And it also can be used as a tool to do A/B testing. It can help us to switch from simple stack to arya.

### How to create a weblab

1. Go to weblab.amazon.com and click Create a New Weblab
2. Fill all the necessary content. 
	* **PREFIX** would be the prefix of your weblab Id, the real Id is the PREFIX follow by a serious digits. 
	* **WEBLAB TITLE** is the name of this weblab. 
	* **BUSINESS GROUP** is Audible CAM. 
	* **REMEDY CTI**  C: Audible, T: Website, I: Account Details and Settings. 
	* **PRIMARY OWNER**: yourself
	* **SECONDARY OWNER**: Team member
	* **OBSERVERS**: Your product manager
3. In the **Treatments** add two treatments and screenshots for each treatment
	* C is controller. The associated page will show when weblab is off.
	* T1 is first treatment. The associated page will show when weblab is on.
4. Activate the webpage on CAAudible and USAudible normally.

### How to use weblab

1. We can add weblab to a placement. When editing a placement we can add a weblab rule and add the weblab Id and associated treament Id into it.
2. We can also exclude a weblab from a placement. Similar to adding weblab, we add a weblab rule in exclude and add the weblab Id and its associated treatment Id.

### How to turn on and off of weblab

1. We cannot launch a treatment (that is the job of QA and PM). But we can also test the weblab by using weblab bookmarklet.
2. We can use bookmarklet builder to build bookmark to enter c or t1.
3. Or we can just use bookmarklet to go into page with a weblab.

### What is the relation between weblab and symphony content

Each campaign contains one or more symphony contents in the form of key value pair. These symphony contents are only belong to this campaign, while this campaign can be applied to many different placements. Each placement is actually a slot (working as widget in code) in a page. We can set rules and excludes to specify the logic of the placement.

### How to debug in web page

1. In arya, we can turn on debug mode by add paremeter `debug=1` into URL
2. In santana, we use `inspect=true`
3. If we want to get the LMS key for strings in this page, using `stringDebug=1` 
### 4. When you want to find the log correspond to the page. Turn debug on and inspect the page, then search 'debugInfo' in Elements, the host name would be the host you may want to ssh.