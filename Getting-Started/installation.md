# Installation

## Requirements

Below you will find the requirements necessary to run AdaptCMS Alpha. Since the CMS is using modern technologies, the versions of software required are newer than normal. The good news is, outside of the ZIP PHP extension, all the requirements are based on L[**aravel**](https://laravel.com/docs/5.4#server-requirements).

* PHP &gt;= 5.6.4
* OpenSSL PHP Extension
* XML PHP Extension
* PDO PHP Extension
* Tokenizer PHP Extension
* Mbstring PHP Extension
* ZIP PHP Extension \(for installation of plugins/themes and upgrades inside the Admin\)
* MySQL Server/Client \(support for more database types coming soon\)
* Apache, NGINX
* URL Rewriting enabled \(mod\_rewrite, try\_files, etc\)

## Install

### With SSH Access \(Cloud Server/SSH for Shared Hositng\)

There's a few options here. First, you can always use [**Composer**](https://getcomposer.org/download/) via the command line:

```
composer require adaptcms/adaptcms
```

You can also grab the latest version, at any time below:

```
wget https://s3.amazonaws.com/adaptcms/latest.zip && unzip latest.zip
```

Or if you would like to get the newest stable version:

```
wget https://s3.amazonaws.com/adaptcms/stable.zip && unzip latest.zip
```

### No SSH Access \(Shared Hosting\)

So, assuming your PHP version is newer than 5.6.4 you can simply download one of the ZIP files below:

**Stable**

[https://s3.amazonaws.com/adaptcms/stable.zip](https://s3.amazonaws.com/adaptcms/stable.zip)

**Latest**

[https://s3.amazonaws.com/adaptcms/latest.zip](https://s3.amazonaws.com/adaptcms/latest.zip)

Then simply unzip the contents of the file locally.



