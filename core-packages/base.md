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
php artisan cms:controller:make {vendor} {package} {controllerName}
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

### Package Fields

A large piece of functionality is package fields. Currently this links a field to a specific page, or a field to a specific module. The package field then serves as the director of storing custom data into a pages table, or in the case of modules, a particular modules table \(such as a column "overall\_rating" on a games table\), as an example.

It also serves to be usable by plugins of any sort. To implement this functionality into a plugin you are creating, or better understand this feature, we will document how to do so and what configuration is available with a lot of flexibility. For example, the relation to pages is one where there is only one pages table with all custom columns on that one table. Whereas with modules, there is a table for each module with it's respective package fields contained on it's own table, yet both itself and Pages use Package Fields.

**Add new trait usage**

To start off with, you need the trait to implement some methods automatically for you:

```text
<?php

use Adaptcms\Base\Traits\IsPackageFieldOwner;

class MyClassName extends Model
{
  use IsPackageFieldOwner;
}
```

**Required columns**

* id
* name
* slug \(this will be filled automatically when using the above trait\)

**toSearchableArray\(\)**

Per the [Laravel Scout docs](https://laravel.com/docs/scout), please create this method.

**getPrimaryFieldAttribute\(\)**

A primary field should be defined in your model of choice for implementation. If you have a column in your table that is set in stone, such as "name" for the pages table, simply return a stdClass with the `column_name` object property value returning this column name.

**shouldCreateColumnMigration\(PackageField $packageField\) \(optional method\)**

**shouldRenameColumnMigration\(PackageField $packageField\) \(optional method\)**

**shouldDropColumnMigration** **method\(PackageField $packageField\) \(optional method\)**

If you want to use conditions to determine if the migration for creating a column for the package field should be made, then implement any \(or all\) of these methods. Named respectively for creation of a column, renaming a column \(on update of a package field name\), or dropping a column \(upon deletion of a package field\).

**getModelFileContents\(\)**

**putModelFileContents\(string $contents\)**

These two methods are necessary for fields such as `FieldFile` and `FieldImage` which require traits to be inserted into the model file. An example with Pages would be pointing to the Page model file as a fallback, but we avoid this for the package by applying the required implements and use call described in the [Spatie Media Library docs, which you may do as well](https://docs.spatie.be/laravel-medialibrary/v8/basic-usage/preparing-your-model/). For modules, we use the `Storage` helper to return and put contents into the path `/app/Modules/{moduleName}.php`. Simple as that!

**fillCustomData\(array $data\)**

This method is used to set data from package fields before saving the record in the database. The best way to utilize this method is looking at the code for this within the `Modules` and `Pages` packages. Here are those model paths:

```text
/packages/Adaptcms/Pages/Model/Page.php
/packages/Adaptcms/Modules/Model/Module.php
```

**syncSearch\(\)**

Upon creating a package field, renaming, or dropping - the search index will need to be updated. Here is an example below, from the `Pages` package:

```text
/**
* Sync Search
*
* @return void
*/
public function syncSearch()
{
  // run scout import
  $items = $this->all();

  $items->searchable();
}
```

**Admin Link Show**

A package that implements the package fields functionality should be searchable. To that end, a standard that is in use for all searchable packages is in place. Here again we show below how the `Pages` package implements this:

```text
use URL;

/**
* @var array
*/
protected $appends = [
  'admin_link_show'
];

/**
* Get Admin Link Show Attribute
*
* @return string
*/
public function getAdminLinkShowAttribute()
{
  return URL::route('pages.admin.show', [
    'page' => $this->id
  ]);
}
```

**Global Warnings**

Packages may take advantage of a global warning system that stores messages in a session and will return them within the admin UI.

Use cases will vary, but one example is an API key not being entered in for a new field type that requires it. You'll want to alert any admins so they can easily fix this issue. To get started, below is an example of creating a warning - note, a URL is optional:

```text
use Adaptcms\Base\Models\GlobalWarning;

GlobalWarning::storeWarning(
  'enter-a-unique-warning-key-here',
  'This is a test warning that should be taken very seriously!',
  route('route.name.here')
);
```

Once a user has taken the required action to fix this issue, you will want to remove the warning. Simply do the below:

```text
GlobalWarning::deleteWarning('enter-your-unique-warning-key-here');
```

That's it! Messages will appear on every admin page until the session has expired/been flushed, or until the warning has been removed with the code above - otherwise if the user deletes the warning. One other utility you may require is to check if the warning is active for your package - here's how to do that below:

```text
GlobalWarning::hasWarning('enter-your-unique-warning-key-here');
```

