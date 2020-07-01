# Fields

Fields are a sort of "field type" grouping which is used for Modules and Pages. A basic example is a "Text" field which is a simple text input and is used as a module field upon creation of a module.

### CLI Commands

#### Create Field

To create a new "field" which can become a GitHub package later on, simply run this:

```text
php artisan cms:field:create {vendor} {package}
```

Upon creation, you will find a new folder path under `/packages` following the vendor/package naming you entered. Creating a field in the admin ends in the same result. Within this folder there are several key files.

Sync UI components

When creating a field, if you make any changes within the default components inside of `/packages/{vendor/Field{package}/ui/field/` - you must run a CLI sync command for your changes to take effect within your website. Simply run this below with yarn/npm running, or build afterwards:

```text
php artisan cms:fields:sync
```

### Field Class File

First, under `/packages/{vendor}/Field{package}/src/Field/Field{package}.php` is the primary method for API usage where you may adjust default settings. `$storeRules` and `$updateRules` are default validation rules that will be passed in when the field is used with a module, or page. An example would be an email field which would pass in an attribute to assure a proper email address:

```text
public $storeRules = [
  'email'
];
```

If your validation needs to be dynamic, then you can instead hook into the `getStoreRules` and the `getUpdateRules` methods. The params depend on if it's a page field, or a module field. `getStoreRules($moduleField = null, $pageField = null)` is what the declarations look like. Basically, it will be one or the other.

The other important methods include a `getValue()` and `setValue($value)` methods. This will be the default getter/setter for any module/page fields created. If a developer modifies the module file this field is attached to, a mutator would override the getValue/setValue methods.

The `migrationCommand` method contains a string value of the migration command that will be ran upon creation of a module field, or a page field. The example should be pretty self-explanatory. Just keep in mind to go by the Laravel documentation on column modifiers, ensure `->nullable()` is attached unless the field is built for a specific website, and keep the same syntax standard seen in the default.

Uncommenting the `shouldNotSetData` attribute and having it return true is mostly used for relationship fields. That way a `hasMany` doesn't try to save data to a column that does not exist.

`formatColumnName` controls the value saved to the database for a module field, as does `formatName`. It should be noted that the column name is set first.

The methods `afterStore` and `afterUpdate` are called after a module field is stored with this field type. You may use this to update configuration, sync custom database structure, or whatever else you would like.

When a custom module item is saved and has a module field linked to your field type, the `afterModelStore` and `afterModelUpdate` methods are called, respectively. The same basic idea is used as with the above after methods. For a relationship field, for example, we hook into this method to manually save data for a `HasMany` relationship.

Another relationship related method is `withLoadedRelationships`, although it can be used for other purposes. Primarily it is used to dynamically define relationships, [as first introduced in Laravel 7](https://laravel.com/docs/7.x/eloquent-relationships#dynamic-relationships). Another important usage is loading relationships that will be returned to the VueJS layer. This second piece can be of great use for those building fields with specific purposes - such as a field for a particular website to achieve specific results. That way your code is still abstracted from the core CMS code, but can still load in the data you need.

The `withFormMeta` is yet another helper method, this one allowing a field to pass in data within the create/edit actions for a custom module. An example being that you need to pass in possible select-able values from the database to a select field.

`afterModuleRename` is called after a module name has been changed. This method looks for any field classes linked to the module in question with this available method. The individual `ModuleField` model class is passed through. An example use is with the `FieldRelationManyToMany` field that needs to rename the join table/column references.

#### UI Customization

There are three UI components that will be used to control how the field value is shown in the admin create/edit pages, index/show pages, and public side views.

**/packages/{vendor}/Field{package}/ui/field/AdminField.vue**

This field returns the HTML input which will be used for create/edit pages within a created module.

**/packages/{vendor}/Field{package}/ui/field/AdminOptions.vue**

When creating a module field, for example, you may save `meta` info for use within these other views, or within the field PHP class file. An example of this is with `FieldNumber` which allows a customization of minimum value, maximum value, and increment/step value. We store these values in the database and can then use this when rendering the field with the above `AdminField.vue` component.

**/packages/{vendor}/Field{package}/ui/field/AdminShow.vue**

Used for the index & show pages within the admin panel for a created module.

**/packages/{vendor}/Field{package}/ui/field/PublicShow.vue**

This is used anywhere a custom module entry, which is related to this field, returns it's value. An example might be returning a google maps image for a google places address picker field.

