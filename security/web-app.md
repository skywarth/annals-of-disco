### Use integrity thingy incase cdn gets hacked, "Subresource Integrity"
- most of the large CDN's and script-delivery-services support it. 
- For unpkg-scripts, append ?meta to the end of the url
- This will return a json-string/object:
```
{
  "path":"/dist/smoothscroll.min.js",
  "type":"file","
  contentType":"application/javascript",
  "integrity":"sha384-EYn4rWu1DHvYD0sSSSbMEtXQmMl58CFJd897806+RT1jJVYbhuZlZMN6yG9nCyFa",
  "lastModified":"Tue, 26 Mar 2019 18:21:19 GMT",
  "size":3968
}
```
- Profit:
```
<script defer
  src="https://unpkg.com/smoothscroll-polyfill@0.4.4/dist/smoothscroll.min.js"
  integrity="sha384-EYn4rWu1DHvYD0sSSSbMEtXQmMl58CFJd897806+RT1jJVYbhuZlZMN6yG9nCyFa"
  crossorigin="anonymous">
</script>
```

### If using npm, do audit
```
npm run audit --fix
```
