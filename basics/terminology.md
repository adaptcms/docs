# Terminology

While using the admin interface, or exploring the code base, here is a simple dictionary of common terminology we use in either/both places.

#### Packages

So packages can be a few different things! In general it refers to a "package" in the base folder `packages`. Within that may contain our own packages, or plugins. Plugins themselves will also reside in here, as well as Fields. It's the central point for all of those, but with different configuration that will be mentioned below to differentiate.

#### Modules

For those coming from Laravel Nova, a "module" is similar to a "resource" in that software. If I had a restaurant, I would create a location module. So it can be seen as a category of content items, or a content type that is defined. Upon creation of a module, a `/app/Modules/{moduleName}.php` is created with the option to customize various aspects of behavior in the admin.

#### Fields

Fields are, at their base, "Field Types". By default, a "Text" field exists, as well as "Textarea". A field you may create, or download could be "Google Places" with a google places address lookup input, for example.

#### InertiaJS

InertiaJS is one of the most powerful tools we are using. With it enabled, developers can create a route, a HTTP controller with action, and then they create a `page.vue` file with data being received by the aforementioned controller action, as well as a lot of helpful stuff such as flash message support, redirect support, validation, and more :\)

