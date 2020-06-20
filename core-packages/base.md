---
description: >-
  The base package is used as a repository of neutral functionality that may be
  used by many other packages.
---

# Base

#### Back-end Helpers

One of the most important functions at this time for Base is the various CLI commands that will be of great use for developers:

```text
php artisan cms:command:make {vendor} {package} {commandName}
php artisan cms:migration:make {vendor} {package} {migrationName}
php artisan cms:model:make {vendor} {package} {modelName}
```

Another useful utility is the ability to get a full list of installed packages, with fields excluded:

```text
use Adaptcms\Base\Models\Package;

Package::getList();
```

#### UI Helpers

On the UI side of things, base contains a large amount of components and helpers that are in use in every core package. We won't be listing out every single component, you can see them all at - `/packages/Adaptcms/Base/ui/components` - but here are some that may slip past the radar.

```text
this.modules

Returns list of custom modules created. Looping through this array will return an
array of data for the module.
```

Modifying the admin dashboard can be done in this page: `/packages/Adaptcms/Base/ui/pages/admin/dashboard.vue` 

Admin Utility Mixin: `/packages/Adaptcms/Base/ui/mixins/AdminUtilityMixin.js`

Admin Form Mixin: `/packages/Adaptcms/Base/ui/mixins/AdminFormMixin.js`

