## Text Hover Transitions

https://dev.to/afif/100-underline-overlay-animation-the-ultimate-css-collection-4p40?utm_source=digest_mailer&utm_medium=email&utm_campaign=digest_email
Alt: https://codepen.io/t_afif/pens/public?cursor=ZD0xJm89MCZwPTEmdj01MDg4NDQ2MA==

---

### Increase hover area 

```
/*I guess this doesn't work for click area, hover only.*/
.btnOnlineAppointment:before {
    content: "";
    width: 100%;
    height: calc(100% + 25px);
    position: absolute;
    top: 0;
    left: 0;
}
```




### Absolute middle and center
```
//Dynamic
top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  
  
//If you know the width 
position:absolute;
left:0;
right:0;
margin-left:auto;
margin-right:auto;
```


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

### Truncate for multiline text
```
    display: -webkit-box;
    -webkit-line-clamp: 8;
    -webkit-box-orient: vertical;
    overflow: hidden;
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
