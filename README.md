# ownCloud News app
[![irc](https://img.shields.io/badge/irc%20channel-%23owncloud--news%20on%20freenode-blue.svg)](https://webchat.freenode.net/?channels=owncloud-news)
[![Join the chat at https://gitter.im/owncloud/news](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/owncloud/news?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[![Build Status](https://travis-ci.org/owncloud/news.svg?branch=master)](https://travis-ci.org/owncloud/news)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/owncloud/news/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/owncloud/news/?branch=master)


The News app is an RSS/Atom feed aggregator. It offers a [RESTful API](https://github.com/owncloud/news/wiki/API-1.2) for app developers. The source code is [available on GitHub](https://github.com/owncloud/news)

![](https://apps.owncloud.com/CONTENT/content-pre1/168040-1.png)

For further developer and user documentation please visit [the wiki](https://github.com/owncloud/news/wiki)

## Maintainers
* [Bernhard Posselt](https://github.com/BernhardPosselt)
* [Alessandro Cosentino](https://github.com/cosenal)
* [Jan-Christoph Borchardt](https://github.com/jancborchardt) (Design)

## Sync Clients
are listed on the [ownCloud apps overview](https://github.com/owncloud/core/wiki/Apps)

## Dependencies
* 64bit operating system and PHP
* PHP >= 5.6
* ownCloud >= 9.0
* libxml >= 2.7.8 (2.9 recommended)
* php-curl
* iconv
* SimpleXML

## Build Dependencies
These Dependencies are only relevant if you want to build the source code:
* make
* which
* Node.js >= 6
* npm
* composer

## Supported Browsers
* Newest Firefox (Desktop, Android, Firefox OS)
* Newest Chrome/Chromium (Desktop, Android)

## Supported Databases
* PostgreSQL >= 9.4 (recommended)
* MariaDb >= 5.5
* SQLite (discouraged)

## Bugs
Please read the [appropriate section in the contributing notices](https://github.com/owncloud/news/blob/master/CONTRIBUTING.md#issues)

## Installation/Update

### Before you install/update the News app
Before you install the app do the following:
* Check that your **owncloud/data/** directory is owned by your webserver user and that it is write/readable
* Check that your installation fullfills the [requirements listed in the README section](https://github.com/owncloud/news#dependencies)
* [Set up ownCloud Background Jobs](https://doc.owncloud.org/server/8.0/admin_manual/configuration_server/background_jobs_configuration.html) to enable feed updates. A recommended timespan for feed updates is 15-30 Minutes.

Then proceed to install the app either from an archive (zip/tar.gz) or clone it from the repository using git

### Installing from the app store
This is the easiest solution: Simply go the the apps page and enable the News app

### Installing from archive
* Go to the [ownCloud News GitHub releases page](https://github.com/owncloud/news/releases) and download the latest release/archive to your server
* Starting with 8.0.0, there are two different releases: **news.tar.gz** and **Source code**. The first one requires no additional steps, the second one requires you to install the dependencies and compile the JavaScript. Choose the first one if you don't want to work on the code. If you want to install a version prior to 8.0.0, choose the **Source code** download.
* On your server, check if there is a folder called **owncloud/apps/news**. If there is one, delete it.
* Extract the downloaded archive to the **owncloud/apps/** folder.
* Remove the version from the extracted folder (e.g. rename **owncloud/apps/news-4.0.3/** to **owncloud/apps/news/**
* If you are a version greater than or equal to 8.0.0 and downloaded the **Source code** zip or tar.gz, you need to install the JavaScript and PHP dependencies and compile the JavaScript first. On your terminal, change into the **owncloud/apps/news/** directory and run the following command (requires node >5.6, npm, curl, make and which):

        sudo -u www-data make  # www-data might vary depending on your distribution

* Finally make sure that the **owncloud/apps/news** directory is owned by the web server user

        sudo chown -R www-data:www-data owncloud/apps/news  # www-data:www-data might vary depending on your distribution

* Activate the **News** app in the apps menu

### Installing from Git (development version)
* The master branch will always be stable in conjunction with the latest master branch from ownCloud
* JavaScript and PHP libraries are not included anymore since 8.0.0 and will require you to run **make** after updating/installing the app
* In your terminal go into the **owncloud/apps/** directory and then run the following command:

        git clone https://github.com/owncloud/news.git
        cd news
        make

* If you are using a stable ownCloud release, stay with the [latest git tag release which is running on your version](https://github.com/owncloud/news/releases). To get an overview over all existing tags run:

        git tag

 You can switch to a release which will be supported on your installation by running:

      git checkout tags/TAG
      make  # if News version >= 8.0.0

 For instance to use the 5.2.8 release, run:

      git checkout tags/5.2.8

* Activate the **News** app in the apps menu

To update the News app use change into the **owncloud/apps/news/** directory using your terminal and then run:

    git pull --rebase origin master
    make

## Performance Notices
* Use MySQL or PostgreSQL for better database performance
* Use the [updater script to thread and speed up the update](https://github.com/owncloud/news-updater)

## Updating Notices

To receive notifications when a new News app version was released, simply add the following Atom feed in your currently installed News app:

    https://github.com/owncloud/news/releases.atom

## FAQ

### My browser shows a mixed content warning (Connection is Not Secure)
If you are serving your ownCloud over HTTPS your browser will very likely warn you with a yellow warnings sign about your connection not being secure.

Chrome will show no green HTTPS lock sign, Firefox will show you the following image
![Mixed Passive Content](https://ffp4g1ylyit3jdyti1hqcvtb-wpengine.netdna-ssl.com/security/files/2015/10/mixed-passive-click1-600x221.png)

Note that this warning **is not red and won't block the page like the following images** which signal **a serious issue**:

![Untrusted Cert](http://www.inmotionhosting.com/support/images/stories/website/errors/ssl/chrome-self-signed-ssl-warning.png)
![Mixed Active Content](http://www.howtogeek.com/wp-content/uploads/2014/02/650x367xchrome-mixed-content-https-problem.png.pagespeed.gp+jp+jw+pj+js+rj+rp+rw+ri+cp+md.ic.r_lQiZiq38.png)

#### What is the cause of the (yellow) error message

This warning is caused by [mixed passive content](https://developer.mozilla.org/en/docs/Security/MixedContent) and means that your page loads passive resources from non HTTPS resources, such as:
* Images
* Video/Audio

This allows a possible attacker to perform a MITM (man-in-the-middle) attack by serving you different images or audio/video.

#### Why doesn't the News app fix it

The News app fully prevents mixed **active** content by only allowing HTTPS iframes from known locations; other possible mixed active content elements such as \<script> are stripped from the feed. Because images and audio/video are an integral part of a feed, we can not simply strip them.

Since an attacker can not execute code in contrast to mixed active content, but only replace images/audio/video in your feed reader, this is **not considered to be a security issue**. If, for whatever reason (e.g. feed which would allow fishing), this is a security problem for you, contact the specific feed provider and ask him to serve his feed content over HTTPS.

#### Why don't you simply use an HTTPS image/audio/video proxy

For the same reason that we can't fix non HTTPS websites: It does not fix the underlying issue but only silences it. If you are using an image HTTPS proxy, an attacker can simply attack your image proxy since the proxy fetches insecure content. **Even worse**: if your image proxy serves these images from the same domain as your ownCloud installation you [are vulnerable to XSS via SVG images](https://www.owasp.org/images/0/03/Mario_Heiderich_OWASP_Sweden_The_image_that_called_me.pdf). In addition people feel save when essentially they are not.

Since most people don't understand mixed content and don't have two domains and a standalone server for the image proxy, it is very likely they will choose to host it under the same domain.

Because we care about our users' security and don't want to hide security warnings, we won't fix (aka silence) this issue.

The only fix for this issue is that feed providers serve their content over HTTPS.

### I am getting: Doctrine DBAL Exception InvalidFieldNameException: Column not found: 1054 Unknown column some_column Or BadFunctionCallException: someColumn is not a valid attribute

The exception name itself will give you a hint about what is wrong:
* **BadFunctionCallException**: Is usually thrown when there are more columns in the database than in the code, e.g.:

      BadFunctionCallException, Message: basicAuthUser is not a valid attribute

    means that the attribute **basicAuthUser** was retrieved from the database but could not be found on the corresponding data object (item.php/feed.php/folder.php) in the **db/** folder

* **InvalidFieldNameException**: Is usually thrown when there are more columns in the code than the database

One reason for this error could be old files which were not overwritten properly when the app was upgraded. Make sure that all files match the files in the release archive!
Most of the time however this is caused by users trying to downgrade (**not supported!!!**) or by failed/timed out database migrations. To prevent future timeouts use

    php -f owncloud/occ upgrade

instead of clicking the upgrade button on the web interface.

If you have made sure that old files are not the cause of this issue, the solution is to either automatically or manually remove or add columns to your database. The automatic way to do this is to trigger a database migration. The manual way is to manually check which database columns have to be removed from or added to the News database tables.

#### Triggering a database migration
Databases are migrated when a newer version is found in **appinfo/info.xml** than in the database. To trigger a migration you can therefore simply increase that version number and refresh the web interface to run an update:

First, get the current version by executing the following Sql query:

```sql
SELECT configvalue FROM oc_appconfig WHERE appid = 'news' and configkey = 'installed_version';
```

This will output something like this:

    7.1.1

Then edit the **appinfo/info.xml** and increase the number on the farthest right in the version field by 1, e.g.:

```xml
<?xml version="1.0"?>
<info>
    <!-- etc -->
    <version>7.1.2</version>
    <!-- etc -->
</info>
```

Now run the update in the web interface by reloading the page.

Finally set back the old version number in the database, so the next News app update will be handled propery, e.g.:

```sql
UPDATE oc_appconfig SET configvalue = '7.1.1' WHERE appid = 'news' and configkey = 'installed_version';
```

#### Manually adding/removing the field
Instead of triggering an automatic migration, you can of course also add or remove the offending columns manually.

To find out what you need to add or remove, check the current **appinfo/database.xml** and compare it to your tables in the database and add/remove the appropriate fields.

Some hints:
* type text is usually an Sql VARCHAR
* type clob is usually an Sql TEXT
* length for integer fields means bytes, so an integer with length 8 means its 64bit

### I am getting: Exception: Some\\Class does not exist erros in my owncloud.log
This is very often caused by missing or old files, e.g. by failing to upload all of the News app' files or errors during installation. Before you report a bug, please recheck if all files from the archive are in place and accessible.

### How do I reset the News app
Delete the folder **owncloud/apps/news/** and **owncloud/data/news/**, then connect to your database and run the following commands where **oc\_** is your table prefix (defaults to oc\_)

```sql
DELETE FROM oc_appconfig WHERE appid = 'news';
DROP TABLE oc_news_items;
DROP TABLE oc_news_feeds;
DROP TABLE oc_news_folders;
```

### App is stuck in maintenance mode after failed update

Check the **owncloud/data/owncloud.log** for hints why it failed. After the issues are fixed, turn off the maintenance mode by editing your **owncloud/config/config.php** by setting the **maintenance** key to false:

    "maintenance" => false,

### Feeds are not updated
Feeds can be updated using ownCloud's system cron or any program that implements the [News app's updater API](https://github.com/owncloud/news/wiki/Updater-1.2), most notably [ownCloud News Updater](https://github.com/owncloud/news-updater). **The feed update is not run in Webcron and AJAX cron mode!**

System Cron:
* Check if the config.ini in **owncloud/data/news/config/config.ini** contains **useCronUpdates = true**
* Check if you are using the system cron (Cron) setting on the admin page. AJAX and Web cron will not update feeds
* Check if the cronjob exists with **crontab -u www-data -e** (replace www-data with your httpd user)
* Check the file permissions of the **cron.php** file and if **www-data** (or whatever your httpd user is called like) can read and execute that script
* Check if you can execute the cron with **sudo -u www-data php -f owncloud/cron.php** (replace www-data with your httpd user)
* Check your **data/owncloud.log** for errors
* Check if the cronjob is ever executed by placing an **error_log('updating');** in the [background job file](https://github.com/owncloud/news/blob/master/cron/updater.php#L28). If the cronjob runs, there should be an updating log statement in your httpd log.
* If there is no **updating** statement in your logs check if your cronjob is executed by executing a different script
* If your cron works fine but owncloud's cronjobs are never executed, file a bug in [core](https://github.com/owncloud/core/)

[ownCloud News Updater](https://github.com/owncloud/news-updater):
* Check if the config.ini in **owncloud/data/news/config/config.ini** contains **useCronUpdates = false**
* Start the updater in loglevel info mode and check if the feed update urls are polled, e.g.:

    owncloud_news_updater --loglevel info -c /path/to/config.ini

* Check your **data/owncloud.log** for errors

### Adding feeds that use self-signed certificates
If you want to add a feed that uses a self-signed certificate that is not signed by a trusted CA the request will fail with "SSL certficate is invalid". A common solution is to turn off the certificate verification **which is wrong** and **makes your installation vulnerable to MITM attacks**. Therefore **turning off certificate verification is not supported**.

If you have control over the feed in question, consider signing your certificate for free on one of the following providers:
* [letsencrypt.com](http://letsencrypt.com/)
* [StartSSL](https://www.startssl.com/)
* [WoSign](https://www.wosign.com/)

If you do not have control over the chosen feed, you should [download the certificate from the feed's website](http://superuser.com/questions/97201/how-to-save-a-remote-server-ssl-certificate-locally-as-a-file) and [add it to your server's trusted certificates](http://www.onlinesmartketer.com/2009/06/23/curl-adding-installing-trusting-new-self-signed-certificate/). The exact procedure however may vary depending on your distribution.


Configuration
-------------
All configuration values are set inside **owncloud/data/news/config/config.ini** and can be edited in the admin panel.

The configuration is in **INI** format and looks like this:

```ini
autoPurgeMinimumInterval = 60
autoPurgeCount = 200
maxRedirects = 10
maxSize = 104857600
feedFetcherTimeout = 60
useCronUpdates = true
exploreUrl =
```


* **autoPurgeMinimumInterval**: Minimum amount of seconds after deleted feeds and folders are removed from the database. Values below 60 seconds are ignored
* **autoPurgeCount**: Defines the maximum amount of articles that can be read per feed which won't be deleted by the cleanup job; if old articles reappear after being read, increase this value; negative values such as -1 will turn this feature off completely
* **maxRedirects**: How many redirects the updater should follow
* **maxSize**: Maximum feed size in bytes. If the RSS/Atom page is bigger than this value, the update will be aborted
* **feedFetcherTimeout**: Maximum number of seconds to wait for an RSS or Atom feed to load. If a feed takes longer than that number of seconds to update, the update will be aborted
* **useCronUpdates**: To use a custom update/cron script you need to disable the cronjob which is run by ownCloud by default by setting this to false
* **exploreUrl**: If given that url will be contacted for fetching content for the explore feed
