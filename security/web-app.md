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

### Content Security Policies

```
<meta http-equiv="Content-Security-Policy" content="
  default-src;
  script-src 'self';
  style-src 'self';
  img-src 'self' data:;
  font-src;
  connect-src 'self';
  media-src 'self';
  object-src 'none';
  child-src;
  frame-src;
  form-action;
  base-uri;
  manifest-src 'self';
">
```
##### There is also a generator for CSP:
https://report-uri.com/home/generate

https://www.cspisawesome.com/content_security_policies

##### Also check this
https://developers.google.com/web/fundamentals/security/csp
