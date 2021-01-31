### Drop caps, wrapping around
```
p:first-child:first-letter {
  color: #903;
  float: left;
  font-family: Georgia;
  font-size: 75px;
  line-height: 60px;
  padding-top: 4px;
  padding-right: 8px;
  padding-left: 3px;
}
```



### Drop shadow for transparent images
```
//https://codepen.io/teamxenox/pen/KKgMPzm

filter: drop-shadow(30px 10px 4px #4444dd);

//box shadow will always work as a box, use drop-shadow for image
```
### Smooth Scroll
```
html {
  scroll-behavior: smooth;
}
```


### Three dot for long text, truncate
```
.truncate {
  width: 250px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

### Change input blinking caret color
```
input {
  caret-color: orange;
}
```
