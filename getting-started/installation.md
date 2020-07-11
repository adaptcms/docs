# Installation

## Setup

After ensuring your web server meets the requirements, you will also need NPM/Yarn installed, as well as composer:

```text
composer require charliepage88/adaptcms
```

After composer is finished, enter the `adaptcms` directory and modify your `.env` file with your database credentials, mail, anything that you see that you can enter credentials, or to choose drivers.

Next, run composer & npm/yarn to install the dependencies:

```text
composer install
yarn OR npm install
```

Once your `.env` file has been saved, run this command to trigger the initial install, as well as setting up your first admin account:

```text
php artisan cms:install
```

If you're looking for a new web host by the way, we highly recommend [**DigitalOcean**](https://m.do.co/c/083895eaa907)!

![](../.gitbook/assets/rsz_do_logo_horizontal_blue-3db19536.png)

## Permissions

We know setting permissions sucks, but one day we sat down and found a good set that worked for us very well. In the root folder there is a `laravel_permissions.sh` file that you can run. Please note before running this command to ensure your apache/nginx username matches `www-data` in the file, and to either create, or edit the group name `dev` that is in the file. We've found having a properly setup user with group permissions to be a big key to getting everything working right.

If you are unsure of how to handle group management in the command line, we have a tutorial setup on this. Note in the example the group name being used is `devs`, but that name can be quickly replaced in the permissions bash file:

[https://charliepage.gitbook.io/book/tutorials/setup-ubuntu-server-2020\#non-root-user-setup](https://charliepage.gitbook.io/book/tutorials/setup-ubuntu-server-2020#non-root-user-setup)

