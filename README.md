# Useful scripts

This repository contains some of my useful scripts. 

Linux/macOS, not Windows. Some scripts work only on some systems as described below.

## Listing

* [email2file](#emailtofile) - catches all emails and writes them to files instead of sending them to recipients
* [hback](#hback) – what is the web server host name of the site?
* [kcpass](#kcpass) – get the macOS keychain password in shell for the URL
* [set-file-url](#set-file-url) – set "downloaded from" macOS metadata for a file
* [sign-phostorm](#sign-phpstorm) – a workaround for annoying PhpStorm network connections prompt in macOS

## License

No warranty, no support, use at your own risk, feel free to copy, modify, distribute.

## Scripts

### <a name="email2file"></a>email2file

"All mail catcher".

This script puts all sent emails to files. I use it from TYPO3 CMS and from Postfix.

In both cases you need to put the file to the file system. Preferably the path to the script should not have spaces.

**[!!!]** You need to check and possibly adjust `EMAIL_DIR` constant inside the script.

On macOS captured emails will be excluded from the Time Machine backups. You can test mass mailing this way without adding many files to your backups.

#### Using with TYPO3 CMS

For TYPO3 CMS you can create a `bin/` directory inside the project and add the script there. Than the script will put all captured emails inside `tmp/` of the project (autocreated if necessary).

Configuration for the `AdditionalConfiguration.php` in CMS:

```php
$GLOBALS['TYPO3_CONF_VARS']['MAIL']['transport'] = 'sendmail';
$GLOBALS['TYPO3_CONF_VARS']['MAIL']['transport_sendmail_command'] = '/home/myproject/bin/email2file -t -i';
```

If you use Posfix, you can follow the next section but it will add additional overhead. It is easier just to configure the system to use mail catcher directly. You cna also add `if` statements to do this only in the development environment (or add this confuration only to your [development context](https://usetypo3.com/application-context.html)).

#### Using with Postfix

Add the following to `master.cf`:

```
file_route unix -    n    n    -    -    pipe user=dmitry argv=/opt/local/bin/email2file
```

Add the following to `main.cf`:

```
default_transport = file_route
```

### <a name="hback"></a>hback

The script resolves the name of the site to the actual name of the web server where it is hosted. Usage:

```sh
$ hback www.apple.com
a172-227-107-104.deploy.static.akamaitechnologies.com

$ hback www.microsoft.com
www.microsoft.com does not resolve to any other host.
```

### <a name="kcpass"></a>kcpass

macOS only. Shows a keychain password for the given URL in shell. Example:

```sh
$ kcpass test.dev
testpass
```

This may show a prompt from the keychain to allow access. Note that "Always allow" can be clicked but has no effect. If you use this often and dislike the prompt, select the item in the keychain app and set `Allow all applications to access the item` in item's `Access control` tab.

### <a name="set-file-url"></a>set-file-url

macOS only. Set a "Download from" field in macOS metadata. This is visible when you use `Get info` Finder menu on the file. Useful if you download the file with `wget` or alike and want to preserve the downloaed URL somewhere. Example:

```sh
$ set-file-url 'https://www.whonix.org/download/13.0.0.1.1/Whonix-Workstation-13.0.0.1.1.ova' Whonix-Workstation-13.0.0.1.1.ova
```

### <a name="sign-phpstorm"></a>sign-phpstorm

macOS only. This is a workaround for the [annoying PhpStorm bug](https://youtrack.jetbrains.com/issue/IDEA-129941), which makes macOS to prompt for network connection each time when you start PhpStorm. It just re-signs the binary to prevent the issue. Example:

```sh
sign-phpstorm
```
