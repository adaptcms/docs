# Upgrading

With the CMS installed and when in the admin, you will see a button on the navigation that will show if an upgrade is available. Along with upgrading through the CMS, you have one other option when proceeding.

**Git Pull**

If you pulled down the repository manually, you can simply run a `git pull` which will update the necessary files in the new version of the CMS.

**CMS Upgrade**

Otherwise, if you did a `composer require` to pull in the CMS, continue on after clicking on upgrade to proceed with the update. If anything failed, there should be a rollback that occurs. Otherwise, you may need to manually look at any files that changed. We highly recommend setting up the CMS in a git repo under your control, especially since running `git status` can quickly help you find any issues that popped up.

After the upgrade is complete, run `yarn run prod` to ensure the latest UI has been built for the admin and public side.

