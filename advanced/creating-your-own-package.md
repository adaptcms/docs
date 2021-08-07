# Creating Your Own Package

### Creating the Package

#### Commands

```text
php artisan cms:command:make {vendor} {package} {commandName}
php artisan cms:migration:make {vendor} {package} {migrationName}
php artisan cms:model:make {vendor} {package} {modelName}
php artisan cms:module:create {name}
php artisan cms:module:update {oldName} {newName}
php artisan cms:module:delete {name}
```

#### Package Configuration File

```text
/packages/{vendorName}/{packageName}/src/{packageName}.php
```

You will find your package file within the above path. Below are different configuration options.

**syncPermissions\(\)**

Here is an example from the Notifications package. We recommend sticking to the prefix **{packageName}.admin.{controllerName}.{actionName}** syntax to be consistent. The name of your permission must also match the route name it corresponds to.

```text
<?php

namespace Adaptcms\Notifications;

use Adaptcms\Auth\Models\Permission;

class Notifications
{
  /**
  * Sync Permissions
  *
  * @return void
  */
  public function syncPermissions()
  {
    $permissions = [
      // admin
      'notifications.admin.settings.edit',
  
      // frontend
      'notifications.front.settings.edit'
    ];
  
    Permission::syncPackagePermissions($permissions);
  }
```

**registerAdminSettingsPage\(\)**

Another example is from the Notifications package. Simply pass the vendor name, package name, and permission/route name.

```text
<?php

namespace Adaptcms\Notifications;

use Adaptcms\Base\Models\Setting;

class Notifications
{
  /**
  * Register Admin Settings Page
  *
  * @return void
  */
  public function registerAdminSettingsPage()
  {
    Setting::registerAdminSettingsPage('Adaptcms', 'Notifications', 'notifications.admin.settings.edit');
  }
```

**registerFrontSettingsPage\(\)**

```text
<?php

namespace Adaptcms\Notifications;

use Adaptcms\Base\Models\Setting;

class Notifications
{
  /**
  * Register Front Settings Page
  *
  * @return void
  */
  public function registerFrontSettingsPage()
  {
    Setting::registerFrontSettingsPage('Adaptcms', 'Notifications', 'notifications.front.settings.edit');
  }
```

**onInstall\(\)**

This method is required to at least register the package with the CMS. You may put in whatever you want for code that is needed, such as calling an install command for your package, within the onInstall method.

```text
<?php

namespace Adaptcms\Notifications;

use Adaptcms\Base\Models\Package;

class Notifications
{
  /**
  * On Install
  *
  * @return void
  */
  public function onInstall()
  {
    Package::syncPackageFolder(get_class());
  }
```

### Package Options

#### Vue Plugin File\(s\)

You may create a plugin or numerous plugins inside your package's UI folder. In the UI folder simply create a folder called `plugins` and any JS files in this folder will be autoloaded and globally usable. Please use Vue conventions to have this plugin able to be registered. Users may see an example in the Base package here:

```text
/packages/Adaptcms/Base/ui/plugins/Base.js
```



