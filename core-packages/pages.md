# Pages

Pages are essentially static parts of your public website, such as a home page or an about page. By default, a page has a title, a URL and status. The URL defines where the user will be able to access the page relative to the website domain.

To help non-tech users better be able to manage the content that appears on pages without doing any coding themselves, fields may be attached to a page creating a "PageField". Utilizing this feature a developer, for example, could define hero fields, content sections using the `FieldRichText` field, basically enabling the user to go into the admin and modify the content in these fields. The developer would then modify the page template to display these values in the appropriate places.

To customize the vue component for a page, you will find it in this path:

```text
/packages/Adaptcms/Site/ui/pages/pages/{name}.vue
```

Please note also that you can customize the data that is passed to the view by modifying the `PagesController` which is also in the `Site` package.

