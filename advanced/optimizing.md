# Optimizing

### Compress JS/CSS

For production use, you may want to utilize gzip for your static CSS/JS assets. This is easy enough! Install `bread-compressor-cli` in a separate folder, such as a folder before your root path and use this package.json file:

```text
{
  "name": "adaptcms",
  "scripts": {
    "dev": "npm run development",
    "local": "npm run dev",
    "prod": "npm run production",
    "compress": "bread-compressor -a gzip -s mysite/public/css/*.css mysite/public/js/*.js"
  },
  "private": true,
  "dependencies": {
    "bread-compressor-cli": "^1.1.0"
  }
}
```

Keep in mind, any time you run `npm/yarn run prod`, you will need to run the compressor since your browser should still be loading the gzip version of your asset files. Also, if you would like to build brotli files along with gzip, simply remove `-a gzip`.

