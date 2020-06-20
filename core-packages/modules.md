# Modules

Modules are at the very core of this software. Think of them as manageable "content types". A restaurant website may want a "Location" module. A video game website may have a "Console" module, and a "Game" module. They can also be seen as sort of a "category" management too.

Managing these modules can be entirely done in the admin, as well as the ability to customize individual modules, and use the command line to manage modules too.

#### CLI Commands

You can create, update, and delete modules with the below commands:

```text
php artisan cms:module:create {name}
php artisan cms:module:update {oldName} {newName}
php artisan cms:module:delete {name}
```

#### Admin

When creating a module, a module file will also be created within this path - `/app/Modules/{module}.php`. A module file is simply a base model file with some extra options.

The `indexQueryFilter()` method can be used to modify the query for the index page of a module within the admin. You receive request data, as well as the Eloquent query object, which you also will return. Any filtering here may be done.

We also have, commented out, several examples of code for getter/setter attributes of module fields. Keep in mind these overwrite any default getter/setter on a specific Field file.

One other helpful method is an example of query filtering for a relation field. An example with a video game website - you have a relationship where a "console" hasMany "game" models. However, you want to filter what consoles are shown when an admin goes to create a game. Utilizing the `fieldQueryFilterConsole()` method would allow you to customize this for the create/edit pages in the admin.

