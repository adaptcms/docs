# Auth

The Auth package is exactly how it sounds! It manages logging in, registration, roles, users, and permissions. In this section we'll be covering the specifics of how these work, and include helpful resources for developers so they can take advantage of internally built in helpers, as well as libraries used within this package.

#### Users

Here are the columns:

* name
* email
* timezone

Here are the core relations:

* roles
* permissions

The database table is created out of the box, as well as the first user being created upon installation. Details on roles and permissions can be seen below.

Login and registration are handled by the base Laravel configuration out of the box, but may be modified per the [Laravel Docs](https://laravel.com/docs/authentication). The UI views may be modified below:

* /packages/Adaptcms/Auth/ui/pages/login.vue
* /packages/Adaptcms/Auth/ui/pages/register.vue

#### Permissions

For permissions and roles, we use a package from Spatie that features full documentation:

{% embed url="https://docs.spatie.be/laravel-permission/v3/introduction" %}

Permissions are in use in every aspect you will see, from the admin to the public side. Menu links are checked, buttons such as create or delete, search, and all routes are protected by permissions. The base permission for being able to access the admin area at all is named `base.admin.access`. A user that does not belong to a role with that permission will not be able to enter the admin area, regardless of any other permissions attached.

Package specific permissions, which are synced upon `composer update`, can be seen in the core class for that Package. For example with the Pages module, the list of permissions that must always exist can be seen in this file:

`/packages/Adaptcms/Pages/Pages.php`

The method `syncPermissions` will contain this list. If you create a package yourself, such as a plugin, be sure to include this so that there is no issues with missing permissions. Any route name defined with a reference to `admin` will, by default, be attached to all roles that have the aforementioned attached permission `base.admin.access`. Roles without that permission will not have access by default to those permissions, but will for any routes that have no reference to `admin` in it's name. Of course, any of this can be overridden within the admin UI.

All permissions can be managed in the admin UI, but we recommend not changing any core permission names as to avoid issues that will occur. Same with deletion of core permissions. Roles can be easily attached, or detached within this UI as well.

Lastly, if you manually modify permissions, or the permissions seem to be out of date - run this command:

```text
php artisan permission:cache-reset
```

#### Roles

Roles are used as sort of a middle-man grouping of permissions for users. Rather than directly assigning permissions to users, although you are free to do that within PHP code, roles are assigned permissions - then users are assigned roles.

By default, a User role, Admin role, and Super Admin role are supplied upon installation. Admin and Super Admin are exactly the same, but are separated for those who would like to alter assigned permissions so only one or two people may have super admin access, and others may have admin access - an example being a restaurant admin where some users would only need access to manage locations, but not to have access to sensitive areas such as permissions, roles, etc.

