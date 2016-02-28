# OpenShift - MediaWiki

This repository is designed to be used with https://www.openshift.com
applications. To use, just follow the quickstart below. This script is based on [this repo](https://github.com/openshift-quickstart/mediawiki-example "OpenShift Quickstart").


# Quickstart

1. Create an account at https://www.openshift.com
2. Create a php application with mysql:
	```
    $ rhc app create mediawiki php-5.4 mysql-5.5
	```
3. Add this upstream mediawiki repo
    ```
    $ cd mediawiki
    $ git remote add upstream -m master https://github.com/Lux-Vacuos/mediawiki.git
    $ git pull -s recursive -X theirs upstream master
	```
4. Then push the repo upstream
    ```
    $ git push
	```
5. That's it, you can now checkout your application at:
    http://mediawiki-$yourlogin.rhcloud.com/wiki

# Updates

In order to update or upgrade to the latest mediawiki, you'll need to re-pull
and re-push.

1. Pull from upstream:
	```
    $ cd mediawiki/
    $ git pull -s recursive -X theirs upstream master
	```
2. Push the new changes upstream
	```
    $ git push
	```


# Repo layout
../data - For persistent data
.openshift/pear.txt - list of pears to install
.openshift/action_hooks/build - Script that gets run every push, just prior to starting your app.


# Notes about layout
Please leave  data directory but feel free to create additional directories if needed.

Note: Every time you push, everything in your remote repo dir gets recreated
please store long term items (like an sqlite database) in ../data which will
persist between pushes of your repo.


# pear.txt

A list of pears to install, line by line on the server.  This will happen when the user git pushes.