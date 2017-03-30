Clone psfmember.org and Downgrade php
=====================================

.. 28 March 2017: 

Starting with a Rackspace clone of psfmember.org named psfmember-dev
192.237.176.114

Stop postfix and disable::

  # /etc/init.d/postfix stop
  # update-rc.d postfix disable

Add to ``/etc/apt/sources``::

  # Needed for php 5.3 and drupal6:
  deb http://archive.debian.org/debian/ squeeze main

To force the install of php 5.3, add to ``/etc/apt/preferences``::

  Package: php5*
  Pin: version 5.3.3*
  Pin-priority: 1010

  Package: php-pear
  Pin: version 5.3.3*
  Pin-priority: 1010

  Package: libapache2-mod-php5
  Pin: version 5.3.3*
  Pin-priority: 1010

  Package: drush
  Pin: version 3.3.1*
  Pin-priority: 101
  

Do an update, then force a down-grade on php5 to 5.3 to avoid massive error
messages in the logs and a bug with php5.4 on Civi 4.2.1 / Drupal 7.16
https://forum.civicrm.org/index.php?topic=26601.0::

  # apt-get update
  # apt-get install php5-cli php-pear

.. 
 psfmember-dev:/home/kbk# apt-get install php5-common php-pear
 Reading package lists... Done
 Building dependency tree       
 Reading state information... Done
 The following package was automatically installed and is no longer required:
   lsof
 Use 'apt-get autoremove' to remove it.
 The following extra packages will be installed:
   libapache2-mod-php5 libdb4.8 php5-cli php5-mcrypt php5-mysql php5-suhosin
 Suggested packages:
   php5-dev
 The following packages will be REMOVED:
   drupal6 php5-gd
 The following NEW packages will be installed:
   libdb4.8 php-pear php5-suhosin
 The following packages will be DOWNGRADED:
   libapache2-mod-php5 php5-cli php5-common php5-mcrypt php5-mysql
 0 upgraded, 3 newly installed, 5 downgraded, 2 to remove and 0 not upgraded.
 Need to get 7,778 kB of archives.
 After this operation, 1,792 kB disk space will be freed.
 Do you want to continue [Y/n]? 
 Get:1 http://archive.debian.org/debian/ squeeze/main libdb4.8 amd64 4.8.30-2 [696 kB]
 Get:2 http://archive.debian.org/debian/ squeeze/main php5-mcrypt amd64 5.3.3-7+squeeze19 [15.2 kB]
 Get:3 http://archive.debian.org/debian/ squeeze/main php5-cli amd64 5.3.3-7+squeeze19 [2,944 kB]
 Get:4 http://archive.debian.org/debian/ squeeze/main php5-mysql amd64 5.3.3-7+squeeze19 [76.7 kB]
 Get:5 http://archive.debian.org/debian/ squeeze/main libapache2-mod-php5 amd64 5.3.3-7+squeeze19 [3,039 kB]
 Get:6 http://archive.debian.org/debian/ squeeze/main php5-common amd64 5.3.3-7+squeeze19 [556 kB]
 Get:7 http://archive.debian.org/debian/ squeeze/main php-pear all 5.3.3-7+squeeze19 [363 kB]
 Get:8 http://archive.debian.org/debian/ squeeze/main php5-suhosin amd64 0.9.32.1-1 [88.4 kB]
 Fetched 7,778 kB in 3s (2,563 kB/s)
 (Reading database ... 42705 files and directories currently installed.)
 Removing drupal6 ...
 Removing php5-gd ...
 Processing triggers for libapache2-mod-php5 ...
 Action 'configtest' failed.
 The Apache error log may have more information.
 Your apache2 configuration is broken, so we're not restarting it for you.
 Selecting previously unselected package libdb4.8.
 (Reading database ... 42174 files and directories currently installed.)
 Unpacking libdb4.8 (from .../libdb4.8_4.8.30-2_amd64.deb) ...
 dpkg: warning: downgrading php5-mcrypt from 5.4.45-0+deb7u8 to 5.3.3-7+squeeze19
 Preparing to replace php5-mcrypt 5.4.45-0+deb7u8 (using .../php5-mcrypt_5.3.3-7+squeeze19_amd64.deb) ...
 Unpacking replacement php5-mcrypt ...
 dpkg: warning: downgrading php5-cli from 5.4.45-0+deb7u8 to 5.3.3-7+squeeze19
 Preparing to replace php5-cli 5.4.45-0+deb7u8 (using .../php5-cli_5.3.3-7+squeeze19_amd64.deb) ...
 Unpacking replacement php5-cli ...
 dpkg: warning: downgrading php5-mysql from 5.4.45-0+deb7u8 to 5.3.3-7+squeeze19
 Preparing to replace php5-mysql 5.4.45-0+deb7u8 (using .../php5-mysql_5.3.3-7+squeeze19_amd64.deb) ...
 Unpacking replacement php5-mysql ...
 dpkg: warning: downgrading libapache2-mod-php5 from 5.4.45-0+deb7u8 to 5.3.3-7+squeeze19
 Preparing to replace libapache2-mod-php5 5.4.45-0+deb7u8 (using .../libapache2-mod-php5_5.3.3-7+squeeze19_amd64.deb) ...
 Unpacking replacement libapache2-mod-php5 ...
 dpkg: warning: downgrading php5-common from 5.4.45-0+deb7u8 to 5.3.3-7+squeeze19
 Preparing to replace php5-common 5.4.45-0+deb7u8 (using .../php5-common_5.3.3-7+squeeze19_amd64.deb) ...
 Unpacking replacement php5-common ...
 dpkg: warning: unable to delete old directory '/etc/php5/mods-available': Directory not empty
 Selecting previously unselected package php-pear.
 Unpacking php-pear (from .../php-pear_5.3.3-7+squeeze19_all.deb) ...
 Selecting previously unselected package php5-suhosin.
 Unpacking php5-suhosin (from .../php5-suhosin_0.9.32.1-1_amd64.deb) ...
 Processing triggers for man-db ...
 Setting up libdb4.8 (4.8.30-2) ...
 Setting up php5-common (5.3.3-7+squeeze19) ...
 Installing new version of config file /etc/cron.d/php5 ...
 Setting up php5-cli (5.3.3-7+squeeze19) ...
 Replacing config file /etc/php5/cli/php.ini with new version
 Setting up libapache2-mod-php5 (5.3.3-7+squeeze19) ...
 Installing new version of config file /etc/apache2/mods-available/php5.conf ...
 Replacing config file /etc/php5/apache2/php.ini with new version
 Action 'configtest' failed.
 The Apache error log may have more information.
 Your apache2 configuration is broken, so we're not restarting it for you.
 Setting up php5-mcrypt (5.3.3-7+squeeze19) ...
 Setting up php5-mysql (5.3.3-7+squeeze19) ...
 Setting up php-pear (5.3.3-7+squeeze19) ...
 Setting up php5-suhosin (0.9.32.1-1) ...
 Processing triggers for libapache2-mod-php5 ...
 Action 'configtest' failed.
 The Apache error log may have more information.
 Your apache2 configuration is broken, so we're not restarting it for you.
 [master 8c7aabe] committing changes in /etc after apt run
  Author: kbk <kbk@psfmember-dev>
  15 files changed, 594 insertions(+), 342 deletions(-)
  delete mode 120000 apache2/conf.d/drupal6.conf
  rewrite apache2/mods-available/php5.conf (98%)
  delete mode 120000 drupal/6/sites/default/files
  create mode 100644 pear/pear.conf
  delete mode 120000 php5/conf.d/20-gd.ini
  create mode 100644 php5/conf.d/mcrypt.ini
  create mode 100644 php5/conf.d/mysql.ini
  create mode 100644 php5/conf.d/mysqli.ini
  create mode 100644 php5/conf.d/pdo.ini
  create mode 100644 php5/conf.d/pdo_mysql.ini
  create mode 100644 php5/conf.d/suhosin.ini


This action removed drupal6 and php5-gd, re-install.  Also add drush.

**N.B. Reject the option to remove the drupal6 database** ::

  
  # apt-get install drupal6 php5-gd
  # apt-get install drush
.. 
  psfmember-dev:/home/kbk# apt-get install drupal6
  Reading package lists... Done
  Building dependency tree       
  Reading state information... Done
  The following package was automatically installed and is no longer required:
    lsof
  Use 'apt-get autoremove' to remove it.
  The following extra packages will be installed:
    libjpeg62 libt1-5 php5-gd
  The following NEW packages will be installed:
    drupal6 libjpeg62 libt1-5 php5-gd
  0 upgraded, 4 newly installed, 0 to remove and 0 not upgraded.
  Need to get 1,442 kB of archives.
  After this operation, 5,835 kB of additional disk space will be used.
  Do you want to continue [Y/n]? 
  Get:1 http://archive.debian.org/debian/ squeeze/main php5-gd amd64 5.3.3-7+squeeze19 [39.2 kB]
  Get:2 http://httpredir.debian.org/debian/ wheezy/main libjpeg62 amd64 6b1-3+deb7u1 [96.9 kB]
  Get:3 http://httpredir.debian.org/debian/ wheezy/main libt1-5 amd64 5.1.2-3.6 [174 kB]
  Get:4 http://archive.debian.org/debian/ squeeze/main drupal6 all 6.31-1 [1,132 kB]
  Fetched 1,442 kB in 1s (1,057 kB/s)
  Selecting previously unselected package libjpeg62:amd64.
  (Reading database ... 42381 files and directories currently installed.)
  Unpacking libjpeg62:amd64 (from .../libjpeg62_6b1-3+deb7u1_amd64.deb) ...
  Selecting previously unselected package libt1-5.
  Unpacking libt1-5 (from .../libt1-5_5.1.2-3.6_amd64.deb) ...
  Selecting previously unselected package php5-gd.
  Unpacking php5-gd (from .../php5-gd_5.3.3-7+squeeze19_amd64.deb) ...
  Selecting previously unselected package drupal6.
  Unpacking drupal6 (from .../drupal6_6.31-1_all.deb) ...
  Processing triggers for libapache2-mod-php5 ...
  [ ok ] Reloading web server config: apache2.
  Setting up libjpeg62:amd64 (6b1-3+deb7u1) ...
  Setting up libt1-5 (5.1.2-3.6) ...
  Setting up php5-gd (5.3.3-7+squeeze19) ...
  Processing triggers for libapache2-mod-php5 ...
  [ ok ] Reloading web server config: apache2.
  Setting up drupal6 (6.31-1) ...
  dbconfig-common: writing config to /etc/dbconfig-common/drupal6.conf
  Replacing config file /etc/drupal/6/sites/default/dbconfig.php with new version
  dbconfig-common: flushing administrative password
  www-data www-data 750 /var/lib/drupal6/files
  [master 69bc576] committing changes in /etc after apt run
   Author: kbk <kbk@psfmember-dev>
   4 files changed, 5 insertions(+), 1 deletion(-)
   create mode 120000 drupal/6/sites/default/files
   create mode 100644 php5/conf.d/gd.ini

Create ``/etc/apache2/sites-available/dev-rs.psfmember.org`` from ``psfmember.org``::

  <VirtualHost *:80>
	  ServerName dev-rs.psfmember.org
	  ##ServerAlias www.psfmember.org psfmember.net www.psfmember.net psfmembe\
  r.com www.psfmember.com
	  ##RedirectPermanent / https://psfmember.org/
	  DocumentRoot /usr/share/drupal6/
	  ServerAdmin webmaster@localhost
  </VirtualHost>

  ## <VirtualHost *:443>
  ##         ServerName psfmember.org
  ##         ServerAlias www.psfmember.org
  ##      DocumentRoot /usr/share/drupal6/
  ##         ServerAdmin webmaster@localhost
  ##         SSLEngine on
  ##         SSLCertificateKeyFile /etc/apache2/ssl/psfmember.key
  ##         SSLCertificateFile /etc/apache2/ssl/psfmember.crt
  ##         SSLCertificateChainFile /etc/apache2/ssl/sub.class1.server.ca.pem
  ##         SSLCACertificateFile /etc/apache2/ssl/ca.pem
  ##</VirtualHost>

  <Directory /usr/share/drupal6/>
	     Options +FollowSymLinks
	     AllowOverride None
	     order allow,deny
	     allow from all
	     <IfModule mod_rewrite.c>
	      RewriteBase /
	      </IfModule>
	      Include /usr/share/drupal6/.htaccess
  </Directory>

Enable the site and restart apache::

  # a2ensite dev-rs.psfmember.org
  # apachectl graceful

(Set the Rackspace Cloud DNS to get an A record for dev-rs.psfmember.org)

Navigate to dev-rs.psfmember.org, log in, and check the site.  Review the
Drupal status report and confirm we have php 5.3.

.. * 29 March 2017:

Download  the CiviCRM Files Needed for Upgrade
=============================================

These files are available from
https://sourceforge.net/projects/civicrm/files/civicrm-stable/ ::

  3.4.8-drupal
  4.1.6-drupal6
  4.1.6-drupal
  4.2.20-drupal
  4.3.11-drupal
  4.4.6-drupal
  4.5.8-drupal
  4.6.27-drupal

Prepare Drupal / CiviCRM for Upgrade
====================================

Take the Drupal site offline

Disable the Drupal devel and frontpage modules, then uninstall them.  Delete
their files.

Disable LogToboggan and LoginToboggan Rules Integration

Turn off caching at ``http://dev-rs.psfmember.org/admin/settings/performance``

Take screenshots of the Drupal module configuration and the Garland theme
configuration.

Shutdown and take a Rackspace image of the server at this point.

Upgrade to CiviCRM 3.3.8
==========================

Restart the server.

Disable all the CiviCRM modules except CiviCRM itself.

Clear the cache and templates_c::

  # pushd /var/lib/drupal6/files/civicrm/templates_c/
  # rm -rf en_US
  # popd
  # drush -v -r /usr/share/drupal6 -l dev-rs.psfmember.org -s cc all

Remove the CiviCRM files and install 3.4.8::

  # cd /etc/drupal/6/sites/all/modules
  # rm -rf civicrm
  # tar xzvf 

Run the CiviCRM upgrade, followed by a Drupal update::

  http://dev-rs.psfmember.org/civicrm/upgrade?reset=1
  http://dev-rs.psfmember.org/update.php

Upgrade to CiviCRM 4.1.6
========================

Follow the previous pattern, clear the caches and install the Drupal 6 version
of CiviCRM 4.1.6 (note the drupal6 in the file specification)::

  # tar xzvf civicrm-4.1.6-drupal6.tar.gz 

Change the configuration of ``../sites/psfmember.org/civicrm.settings.php`` and
``../sites/default/civicrm.settings.php``::

  define( 'CIVICRM_UF'               , 'Drupal'        );

  to

  define( 'CIVICRM_UF'               , 'Drupal6'        );

Run the CiviCRM upgrade, followed by a Drupal update::

  http://dev-rs.psfmember.org/civicrm/upgrade?reset=1
  http://dev-rs.psfmember.org/update.php

Switch to Drupal 7
==================

Install Drupal 7::

  # apt-get install drupal7

Select "Yes" to configure a drupal7 mysql database. There are two passwords
requests.  The first is for the root user to access mysql. The second password
is to be the same as the drupal6 mysql user.

.. 
  If db access issues, verify this 
  mysql> grant usage on *.* to drupal7@localhost identified by <pw>
  mysql> grant all on drupal7.* to drupal7@localhost

.. https://wiki.civicrm.org/confluence/display/CRMDOC/CiviCRM+MySQL+Permission+Requirements

Clean up the msql access rights for user civicrm::

  mysql> drop user civicrm;

  mysql> drop user civicrm@localhost;

  mysql> create user civicrm@localhost identified by <pw>

  mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, DROP, INDEX, ALTER,
  	 CREATE TEMPORARY TABLES, LOCK TABLES, TRIGGER, CREATE ROUTINE, ALTER
  	 ROUTINE, CREATE VIEW ON civicrm.* TO 'civicrm'@'localhost'

Copy the drupal6 db to drupal7.  This works only because the db is ISAM::

  # cd /var/lib/mysql
  # rm -rf drupal7
  # cp -ar drupal6 drupal7



