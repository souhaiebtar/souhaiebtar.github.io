---
layout: post
date: 2021-05-11 10:41:09
title: Setup a php composer mysql environment on windows without admin access
description: >-
 Setup a php composer mysql environment on windows without admin access
main-class: 'tools'
color: '#7AAB13'
tags:
- tools
twitter_text: >-
  Setup a php composer mysql environment on windows without admin access
introduction: "Setup a php composer mysql environment on windows without admin access"
---

# How to setup php + composer + mysql  environment on windows without installer


1. Download files

* a mysql 5.7 community server zip archive from `https://dev.mysql.com/downloads/mysql/5.7.html`
* a php zip file (non threaded version) from `https://windows.php.net/download/`
* composer.phar file download from `https://getcomposer.org/download/`
* download cmder full version from `https://cmder.net/`

the file i ended with ls

```
php-7.4.19-nts-Win32-vc15-x64.zip
mysql-5.7.34-winx64.zip
composer.phar
cmder.7z
```


2. Create a folder under your Personal folder (or wherever you want), let say may name is `unknown`, so i created a folder under `C:\Users\tunknown\apps`

now under `C:\Users\tunknown\apps`

extract `mysql-5.7.34-winx64.zip`, you will get a `mysql-5.7.34-winx64` folder
extract the content of `php-7.4.19-nts-Win32-vc15-x64.zip` file inside a `php7_4` folder (make sure that vc 15 is installed, just google it and download the file)
copy `composer.phar` inside a `composer` folder
extract the content of `cmder.7z` to a `cmder` folder (we use cmder because it come with openssl and git baked in)

now you will get

```
C:\Users\tunknown\apps
|_cmder
|_composer
|_mysql-5.7.34-winx64
|_php7_4
```

now open `cmder` (if settings view shows you can choose whatever, for me i choose in `Choose your startup task`: {PowerShell:PowerShell}),
now type `cd C:\Users\tunknown\apps\composer` after that type `Set-Content composer.bat '@php "%~dp0composer.phar" %*'`,

know we will modify the user path (we don't need to modify the system path first because files are in my account folder also in this way even if we are in a limited account we can do our work), if you type `path` in the Start Menu (the menu that show after clicking on the bottom left icon in windows), normally in the options that shows somthing like `edit environment variables for your account`, in the window that will display modify User variable `Path`, by adding in my case:
* `C:\Users\tunknown\apps\php7_4`
* `C:\Users\tunknown\apps\composer`
* `C:\Users\tunknown\apps\mysql-5.7.34-winx64\bin`

now normally if we go back and open `cmder` (from C:\Users\tunknown\apps\cmder), and we type `php -v` version should show,

the same for composer (using `composer -V`),

know type `cd C:\Users\tunknown\apps\php7_4`, than `cp .\php.ini-development .\php.ini`,
edit `php.ini` file, go to line `;extension_dir= "ext"` and uncomment it (remove the `;`) than scroll down to extensions and enable what ever you want ( extension are line that start with `;extension=`, just remove the `;` if you want to enable a specific extension)

mysql turn,

on `cmder`, type `mysql` the command should be known, to initialize the mysql server type `mysqld.exe --initialize-insecure`, database will be initialized, know run `mysqld.exe` again (process to run mysql server), open another `cmder` window\tab and type `mysql.exe -uroot`, you should be able to access the database.

you can start by creating a password for the mysqlserver using

```
ALTER USER 'user-name'@'localhost' IDENTIFIED BY 'NEW_USER_PASSWORD';
FLUSH PRIVILEGES;
```

know

### Resources
[1]: https://getcomposer.org/doc/00-intro.md#installation-windows
[2]: http://kizu514.com/blog/install-php7-and-composer-on-windows-10/
[3]: https://roytuts.com/installing-mysql-zip-archive-in-windows/
