# Useful scripts

This repository contains some of my useful scripts.

## Listing

* [hback](#hback) – what is the web server host name of the site?
* [kcpass](#kcpass) – get the macOS keychain password in shell for the URL
* [set-file-url](#set-file-url) – set "downloaded from" macOS metadata for a file
* [sign-phostorm](#sign-phpstorm) – a workaround for annoying PhpStorm network connections prompt in macOS

## License

No warranty, no support, use at your own risk, feel free to copy, modify, distribute.

## Scripts

### <a name="hback"></a>hback

The script resolves the name of the site to the actual name of the web server where it is hosted. Usage:

```sh
$ hback www.apple.com
a172-227-107-104.deploy.static.akamaitechnologies.com

$ hback www.microsoft.com
www.microsoft.com does not resolve to any other host.
```

### <a name="kcpass"></a>kcpass

Shows a keychain password for the given URL in shell. Example:

```sh
$ kcpass test.dev
testpass
```

This may show a prompt from the keychain to allow access. Note that "Always allow" can be clicjked but has no effect. If you use this often and dislike the prompt, select the item in the keychain app and set `Allow all applications to access the item` in item's `Access control` tab.

### <a name="set-file-url"></a>set-file-url

Set a "Download from" field in maxOS metadata. This is visible when you use `Get info` Finder menu on the file. useful if you download the file with `wget` or alike anbd want to preserver the downloaed URL somewhere. Example:

```sh
$ set-file-url 'https://www.whonix.org/download/13.0.0.1.1/Whonix-Workstation-13.0.0.1.1.ova' Whonix-Workstation-13.0.0.1.1.ova
```

### <a name="sign-phpstorm"></a>sign-phpstorm

This is a workarounf for the [annoying PhpStorm bug](https://youtrack.jetbrains.com/issue/IDEA-129941), which makes macOS to prompt for network connection each time when you start PhpStorm. It just re-signs the binary to prevent the issue. Example:

```sh
sign-phpstorm
```