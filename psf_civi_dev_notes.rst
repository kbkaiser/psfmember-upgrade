Clone psfmember.org and Downgrade php
=====================================

.. 28 March 2017: 

Starting with a Rackspace clone of psfmember.org named psfmember-dev
192.237.176.114

This site is running Debian's drupal6 package, which is 6.31 patched for
security issues and downloaded CiviCRM 3.3.6.  The server is running Debian
Squeeze LTS.

Stop postfix and disable::

  # service postfix stop
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

Create ``/etc/apache2/sites-available/dev-rs6.psfmember.org`` from ``psfmember.org``::

  <VirtualHost *:80>
	  ServerName dev-rs6.psfmember.org
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

  # a2ensite dev-rs6.psfmember.org
  # apachectl graceful

(Set the Rackspace Cloud DNS to get an A record for dev-rs6.psfmember.org)

Navigate to dev-rs6.psfmember.org, log in, and check the site.  Review the
Drupal status report and confirm we have php 5.3.

.. * 29 March 2017:

Download  the CiviCRM Files Needed for Upgrade
================================================

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

Disable all the CiviCRM modules except the base module. Leave that enabled.

Disable the Drupal devel and frontpage modules, then uninstall them.  Delete
their files. Do the same for the CiviCRM theme module. Remove the SimplyCivi
files from ``.../sites/all/themes/``

Disable LogToboggan and LoginToboggan Rules Integration

Turn off caching at ``http://dev-rs6.psfmember.org/admin/settings/performance``

Take screenshots of the Drupal module configuration and the Garland theme
configuration.

Shutdown and take a Rackspace image of the server at this point.

Upgrade to CiviCRM 3.4.8
==========================

Restart the server.

Disable all the CiviCRM modules except CiviCRM itself.

Clear the cache and templates_c::

  # pushd /var/lib/drupal6/files/civicrm/templates_c/
  # rm -rf en_US/*
  # popd
  # drush -v -r /usr/share/drupal6 -l dev-rs6.psfmember.org -s cc all

Remove the CiviCRM files and install 3.4.8::

  # cd /etc/drupal/6/sites/all/modules
  # rm -rf civicrm
  # tar xzvf civicrm-3.4.8-drupal.tar.gz

Run the CiviCRM upgrade, followed by a Drupal update::

  http://dev-rs6.psfmember.org/civicrm/upgrade?reset=1
  http://dev-rs6.psfmember.org/update.php

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

  http://dev-rs6.psfmember.org/civicrm/upgrade?reset=1
  http://dev-rs6.psfmember.org/update.php

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

Clean up the mysql access rights for user civicrm::

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

Copy the CiviCRM files from the D6 to the D7 tree::

  # cd /var/lib/drupal7
  # rm -rf files
  # cd /var/lib/drupal6
  # cp -ar files /var/lib/drupal7

Copy the D7 .htaccess file into the files directory::

  # cd /var/lib/drupal7/files
  # cp -a /usr/share/doc/drupal7/file.htaccess .htaccess
  # chown www-data:www-data .htaccess
  # chmod 644 .htaccess

Copy the virtual host files into the D7 tree::

  # cd /etc/drupal/7/sites
  # cp -ar default psfmember.org
  # cp -a /etc/drupal/6/sites/psfmember.org/civicrm.settings.php psfmember.org

Configure the copied civicrm.settings.php for Drupal 7::

  Edit /etc/drupal/7/sites/psfmember.org

  Was:
  define( 'CIVICRM_UF'               , 'Drupal6'        );
  Is:
  define( 'CIVICRM_UF'               , 'Drupal'        );

  Was:
  define( 'CIVICRM_UF_DSN' , 'mysql://drupal6:0MhAQL0wh87s@localhost/drupal6?new_link=true' );
  Is:
  define( 'CIVICRM_UF_DSN' , 'mysql://drupal7:0MhAQL0wh87s@localhost/drupal7?new_link=true' );

  Was:
  $civicrm_root = '/usr/share/drupal6/sites/all/modules/civicrm';
  Is:
  $civicrm_root = '/usr/share/drupal7/sites/all/modules/civicrm';
  Was:

  define( 'CIVICRM_TEMPLATE_COMPILEDIR', '/usr/share/drupal6/sites/psfmember.or	g/files/civicrm/templates_c/' );
  Is:
  define( 'CIVICRM_TEMPLATE_COMPILEDIR', '/usr/share/drupal7/sites/psfmember.org/files/civicrm/templates_c/' );

  Was:
  define( 'CIVICRM_TEMPLATE_COMPILEDIR', '/usr/share/drupal6/sites/psfmember.org/files/civicrm/templates_c/' );
  Is:
  define( 'CIVICRM_TEMPLATE_COMPILEDIR', '/usr/share/drupal7/sites/psfmember.org/files/civicrm/templates_c/' );

  Is:
  define( 'CIVICRM_UF_BASEURL'      , 'https://psfmember.org/' );
  Is:
  define( 'CIVICRM_UF_BASEURL'      , 'http://dev-rs7.psfmember.org/' );

  Note: the previous change is only needed for a development site, but it is
  important there to avoid impacting the production site.

  Was:
  define( 'CIVICRM_MAIL_LOG', '/usr/share/drupal6/sites/dev-do.psfmember.org/files/civicrm/templates_c//mail.log' );
  Is:
  define( 'CIVICRM_MAIL_LOG', '/usr/share/drupal7/sites/dev-do.psfmember.org/files/civicrm/templates_c//mail.log' );

Copy the D6 CiviCRM .../sites/all tree into the D7 location::

  # cd /etc/drupal/7/sites
  # cp -ar /etc/drupal/6/sites/all/ all

Remove the D6 CiviCRM tarballs::
  
  # cd /etc/drupal/7/sites/all/modules
  # rm civicrm-3* civicrm-4.1.6-drupal6.tar.gz

Install the D7 CiviCRM 4.1.6 files::

  # rm -rf civicrm
  # tar xzvf civicrm-4.1.6-drupal.tar.gz

Setup access to the D7 site. First, set the Rackspace Cloud DNS to get an A
record for dev-rs7.psfmember.org. Then, add to
/etc/apache2/sites-enabled/dev-rs7.psfmember.org::

  <VirtualHost *:80>
          ServerName dev-rs7.psfmember.org
          ##ServerAlias www.psfmember.org psfmember.net www.psfmember.net psfmember.com www.psfmember.com
          ##RedirectPermanent / https://psfmember.org/
          DocumentRoot /usr/share/drupal7/
          ServerAdmin webmaster@localhost
  </VirtualHost>

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

  # a2ensite dev-rs7.psfmember.org
  # apachectl graceful

Take a Rackspace image at this point.

Perform the Drupal 7 Upgrade
===============================

..
   Tried an update.php.
   "The website encountered an upexpected error"
   Set $update_free_access=TRUE; in .../sites/psfmember.org/settings.php
   Repeat the update.php
   This time it got to the update page.
   136 pending updates

Set update free access::

  edit /etc/drupal/7/sites/psfmember.org
  Change: $update_free_access = TRUE;

Navigate to dev-rs7.psfmember.org/update.php

This will spin for a couple of minutes, and then open the update
webpage. Continue with the update.  The next screen will be a list of changes.
Take a screen shot.

Clear update free access::

  edit /etc/drupal/7/sites/psfmember.org
  Change: $update_free_access = FALSE;

Navigate to dev-rs7.psfmember.org/login/ and log in as Drupal user 1. In this
case, that is user psf.

Navigate to .../civicrm/  You are now running CiviCRM 4.1.6 in D7.

Set the Drupal 7 cron key::
  
  The key can be found in the Drupal Status Report.

  edit .../sites/psfmember.org/settings.php

  Was:
  # $cron_key = '<cron_key>';
  Is:
  $cron_key = 'h8euBg5LHiBXLfTi3xUSw8pRqy5opGd4X5anx4pkm2Q';

Uninstall D6 Modules:  The following modules need to be disabled and uninstalled in Drupal Modules page, then delete their files in ``...sites/all/modules``::

  Advanced Help
  Civicrm Theme
  Ckeditor
  Jquery Update
  Logintoboggan
  Node Privacy by Role
  Rules
  Wysiwyg

Uninstall CiviGroup Roles Sync and CiviMember Roles Sync

Download and install D7 versions of the following modules::

  Advanced Help
  Ckeditor
  Entity API
  Jquery Update
  Logintoboggan
  Rules
  Wysiwyg Version 7.x-2.2 only!

Enable those modules.

Shutdown and take a Rackspace image.

Upgrade CiviCRM by Minor Versions
=================================

Navigate to http://dev-rs7.psfmember.org/civicrm/admin/setting/misc?reset=1
and set Logging to "No".  
Then navigate to http://dev-rs7.psfmember.org/civicrm/admin/setting/debug
and set Enable Drupal Watchdog to "No"
This is important!

The ``.../sites/psfmember.org/civicrm.settings.php`` file must have the following text added just above the line reading "Do not change anything below..."::

  // These lines should appear just above the line "Do not change anything below this line. Keep as is"
  /**
   * This setting logs all emails to a file. Useful for debugging any mail (or civimail) issues.
   * This will not send any email, so ensure this is commented out in production
   */
  // define( 'CIVICRM_MAIL_LOG', '/home/lnp/public_html_test/sites/default/files/civicrm/templates_c/mail.log' );

  /**
   * Settings to enable external caching using a Memcache server.  This is an
   * advanced features, and you should read and understand the documentation
   * before you turn it on.
   *
   * @see http://civicrm.org/node/126
   */

  /**
   * If you have a memcache server configured and want CiviCRM to make use of it,
   * set the following to 1.  You should only set this once you have your memcache
   * server up and working, because CiviCRM will not start up if your server is
   * unavailable on the host and port that you specify.
   */
  define( 'CIVICRM_USE_MEMCACHE', 0 );

  /**
   * Change this to the IP address of your memcache server if it is not on the
   * same machine (Unix).
   */
  define( 'CIVICRM_MEMCACHE_HOST', 'localhost' );

  /**
   * Change this if you are not using the standard port for memcache (11211)
   */
  define( 'CIVICRM_MEMCACHE_PORT', 11211 );

  /**
   * Items in cache will expire after the number of seconds specified here.
   * Default value is 3600 (i.e., after an hour)
   */
  define( 'CIVICRM_MEMCACHE_TIMEOUT', 3600 );

  /**
   * If you are sharing the same memcache instance with more than one CiviCRM
   * database, you will need to set a different value for the following argument
   * so that each copy of CiviCRM will not interfere with other copies.  If you only
   * have one copy of CiviCRM, you may leave this set to ''.  A good value for
   * this if you have two servers might be 'server1_' for the first server, and
   * 'server2_' for the second server.
   */
  define( 'CIVICRM_MEMCACHE_PREFIX', '' );

Then, at the very end of the file, add these lines::

  require_once 'CRM/Core/ClassLoader.php';
  CRM_Core_ClassLoader::singleton()->register();

Clear the caches and delete templates_c::

  # cd /var/lib/drupal7/files/civicrm/templates_c
  # rm -rf en_US/*

  # drush -v -r /usr/share/drupal7 -l dev-rs7.psfmember.org -s cc all

Shutdown and make a Rackspace image.

Install civi 4.2.20 files::

  # cd .../sites/all/modules
  # rm -rf civicrm
  # tar xzvf civicrm-4.2.20-drupal.tar.gz

It is necessary to disable mysql binary logging during the upgrade to 4.2.20.
Temporarily comment out these lines in ``/etc/mysql/my.cnf``::

 #log_bin                        = /var/log/mysql/mysql-bin.log
 #expire_logs_days       = 90
 #max_binlog_size         = 100M

Restart mysql::
 
 # service mysql restart 


Navigate to dev-rs7.psfmember.org/civicrm/upgrade?reset=1

Note: there are four contribution records in this clone that are multiply
linked.  They will be deleted from the production site.  Here, accept the
automated patch-up.

.. Made an image at 4.2.20

Install CiviCRM 4.3.11 files, clear the cache, delete templates.

Do a CiviCRM upgrade.  Take a screenshot of the notices.

Repeat for CiviCRM 4.4.6

.. got a whitescreen.  Go back to 4.3.11 files and database.

.. The owner of en_US was root - even though deleted before upgrade.
   Change owner to www-data, and delete.  Why created by root?

.. Move forward to 4.4.6 with debug. templates_c/en_US was being created by
   root and didn't have permissions for www-data.  Changed the permissions and
   didn't delete it, delete the directories under it.

Repeat for CiviCRM 4.5.8

Repeat for CiviCRM 4.6.27

Navigate to dev-r6.psfmember.org/update.php to do a database update.

.. Turn off Drupal and Civi debugging

.. Evaluate later whether mysql binary logging can be switched back on.

Take the D7 site out of maintenance mode.

Research how to replace the missing Front Page module.

You can also take dev-d6.psfmember.org out of maintenance mode, if useful.
