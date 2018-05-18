# Coding Guidelines

The two over-arching things to know about AdaptCMS are this, in regards to coding philosophy:

1. We currently use the Laravel PHP framework
2. We try to use the latest stable technology we can

That said, there are some things we ask for people to watch out for and to try the best they can, to adhere to. Some are very basic things, and others are a personal preference.

## Github Workflow

We ask that you follow the traditional github workflow. Pull down the repo and make changes to it based off of a current issue, or open a new issue and work on it. If we have people starting to do work on the CMS, without using the current structure, it will be very hard to keep things organized.

## Avoid the normal PHP annoyances

* Test out your code
* Name methods in a way that makes sense and isn't super long. Same with variables. No process\(\) methods or $a variables.
* Don't over-abstract. If you're not sure, submit the pull request and we'll let you know.
* Use a standard editor so the code formatting isn't super different between everyone.
* Follow MVC standards as much as possible. If you need to dynamically query for data in a view file, and can't pass the data from the controller - create a service.

## AdaptCMS-specific guidelines

* Be conscience of where your code goes. We try to keep the **Core** module to internal functionality and the rest goes to the appropiate module. \(such as a new feature for categories, belonging in the **Posts** module\)
* Follow MVC standards as much as possible. If you need to dynamically query for data in a view file, and can't pass the data from the controller - create a service.
* Use Laravel code when needed. Please don't create a crazy custom super model class that isn't needed.
* When using filters/events, don't over-do it
* Talking about events, the reason is - speed. Along with testing out your code before you do a pull request, please ensure that the speed of your code isn't an issue.
* Use caching when appropiate
* For new features, think outside the box! If X CMS has this really useful feature where, for example, you can stay logged into the admin - that's fine. But try and think about, too, how can it be better? What's not great about the implementation on X CMS?
* Working on this CMS is not a solo adventure. While you can have as much space as you want, for new features, please reach out so we can get a discussion going if it's with the core system. If you're making a plugin, you should still reach out \(even if it's through private channels\), that way we could always bounce ideas. But it is not required at all.

