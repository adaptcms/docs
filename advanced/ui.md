# UI

### Override Core UI Views

With this feature, you could fully customize every single view rendered from the CMS. For more practical purposes, lets look at a realistic use-case of wanting to override the default login page with your own designed login page.

All it takes in this example is creating a file at `/packages/Adaptcms/Site/ui/pages/Adaptcms/Auth/login.vue` 

That path can be used with anything. In the example above the full path to the Auth login view is `/packages/Adaptcms/Auth/ui/pages/login.vue` - so as you can see we snip out the `ui/pages` part, essentially taking the vendor, the package name, and the path within the pages folder.

The only exception to overriding views are ones with a vendor/package explicitly set in the controller, although this method is strictly used at the moment to render `Site` views from a different package.



