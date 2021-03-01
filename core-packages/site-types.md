# Site Types

Site types are a way to quickly set up your own category of website. The first site type we have is `SiteTypePizza`, which allows someone who either owns their own pizza restaurant or is making a website for a pizza company, to have their very own pizza website running in moments. Developers can then customize the public website, and otherwise, content management is already setup.

{% hint style="info" %}
**Note:** Instances of `SiteTypePizza` are simply an example. Whatever you name as your site type will take the place of that reference in the below docs.
{% endhint %}

### Activating a Site Type

Coming soon...

### Creating a Site Type

**CLI Command**

Coming soon...

**Base Config**

This first page on the site type activation screen is used to store general info for your site type. That may be the site name, a logo image, or other things that can be used in building a layout, for example:

```text
src/SiteType/SiteTypePizza.php

/**
* Base Config
*
* @return array
*/
public $config = [
  [
    'name'     => 'Site Name',
    'field'     => 'Adaptcms/FieldText',
    'required' => true
  ]
];
```

Provide a valid `{vendor}/{package}` namespace for a field, define a name for the field, can require the field value to be provided, and can pass in meta-information as seen in an example below:

```text
src/SiteType/SiteTypePizza.php

/**
* Base Config
*
* @return array
*/
public $config = [
  [
    'name'     => 'Site Logo',
    'field'     => 'Adaptcms/FieldImage',
    'required' => false,
    'meta'     => [
      'mode' => 'single'
    ]
  ]
];
```

`FieldImage` has an option to support either a single or multiple images above, so providing a `meta` key with key/value of `mode => single` would create the field so a single image can be uploaded to the provided module, or in this case, configuration for the site type.

**Custom Modules**

Using the Pizza example, we want a `Location` module so the owner can enter in their different store locations to show on the website:

```text
src/SiteType/SiteTypePizza.php

/**
* Custom Modules
*
* @return array
*/
public $modules = [
  [
    'name'  => 'Location',
    'fields' => [
      [
        'name'     => 'Title',
        'field'     => 'Adaptcms/FieldText',
        'required' => true
      ],
      [
        'name'     => 'Address',
        'field'     => 'Adaptcms/FieldPlace',
        'required' => true
      ],
      [
        'name' => 'Notes',
        'field' => 'Adaptcms/FieldTextarea'
      ]
    ]
  ]
];
```

So we want a module called `Location`, with a title field \(ex. Downtown Atlanta\), address \(of the store\), and notes \(ex. store hours or parking info\).

**Custom Pages**

The other piece is static pages. For our example pizza restaurant, we may want an `About Us` page to talk about the history and mission of the pizza chain, a contact page with information on how to get in contact, a catering page with information on how to get pizza catered to you, and so on.

For this example, we'll just show a simple `About Us` page:

```text
src/SiteType/SiteTypePizza.php

/**
* Custom Pages
*
* @return array
*/
public $pages = [
  [
    'name'  => 'About Us',
    'url'   => '/about',
    'fields' => [
      [
        'name'     => 'Body',
        'field'     => 'Adaptcms/FieldRichText',
        'required' => true
      ]
    ]
  ]
];
```

**UI - Overwrite Layout**

When creating a Site Type, you can choose to overwrite the public layout in the `src/SiteType/SiteTypePizza.php` file:

```text
class SiteTypePizza
{
  /**
  * @var bool
  */
  public $overwriteLayout = true;
}
```

This value is set to `false` by default, but switching to true will copy the layout in your site type path `ui/layouts/layout.vue` to the `Site` package folder where the public layout resides.

Using the power of package fields, you can easily build PHP arrays that contain the configuration used when activating the site type.

**UI - Activate Site Type**

When activating a site type, there is a basic warning near the top of the page explaining that current data may be overwritten by continuing and below that is where you may choose to show whatever you choose. You may want to simply thank the user for using your site type, show a preview of what it will look like, or other notes.

Simply edit, to your heart's content, the file at `ui/ActivateSiteType.vue` within your Site Type's folder.

