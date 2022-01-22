
### Remove duplicate numbers (maybe even strings ?)
```
const arr = [1, 2, 2, 3]
const newArr = new Set(arr)
const unique = [...newArr]
```



## Device Orientation Event and API
- *You can test and override this with settings->more tools->sensors in chrome*
- *Guess you can't do it without event. But what if one fired the event forcefully ? Oy oy oy*
### Android, standard
```
//beware, this causes problems with apple permissions
// There is a fourth parameter 'absolute'. But let's not get into that

window.addEventListener('deviceorientation', handleOrientation);

    function handleOrientation(event) {
        const alpha = event.alpha;
        const beta = event.beta;
        const gamma = event.gamma;
        console.log(alpha+" "+beta+" "+gamma);
    }
```

### IOS and permission polyfill
```
function onClick() {
  if (typeof DeviceMotionEvent.requestPermission === 'function') {
    // Handle iOS 13+ devices.
    DeviceMotionEvent.requestPermission()
      .then((state) => {
        if (state === 'granted') {
          window.addEventListener('devicemotion', handleOrientation);
        } else {
          console.error('Request to access the orientation was rejected');
        }
      })
      .catch(console.error);
  } else {
    // Handle regular non iOS 13+ devices.
    window.addEventListener('devicemotion', handleOrientation);
  }
}
```
---
### Foreach shorthand

```
for (let i in testData) or  for (let i of testData)
```


### Null, Undefined, Empty Check (dont like it a lot)
```
// Longhand
if (first !== null || first !== undefined || first !== '') {
    let second = first;
}
// Shorthand
let second = first|| '';
```

### Multiple If conditions
```
//longhand
if (x === 'abc' || x === 'def' || x === 'ghi' || x ==='jkl') {
    //logic
}
//shorthand
if (['abc', 'def', 'ghi', 'jkl'].includes(x)) {
   //logic
}
```

### Lookup Conditions Shorthand
```
// Longhand
if (type === 'test1') {
  test1();
}
else if (type === 'test2') {
  test2();
}
else if (type === 'test3') {
  test3();
}
else if (type === 'test4') {
  test4();
} else {
  throw new Error('Invalid value ' + type);
}
// Shorthand
var types = {
  test1: test1,
  test2: test2,
  test3: test3,
  test4: test4
};

var func = types[type];
```

### List of Random Numbers
```
Array.from({ length: 1000 }, Math.random)

// [ 0.6163093133259432, 0.8877401276499153, 0.4094354756035987, ...] - 1000 items

//Or (v, i) => i for index number
```



### Valid URL
```
const isValidURL = (url) => {
  try {
    new URL(url);
    return true;
  } catch (error) {
    return false;
  }
};

isValidURL("https://google.com");
// true

isValidURL("https//invalidto");
// false

```

### N Ago
```
const fromAgo = (date) => {
  const ms = Date.now() - date.getTime();
  const seconds = Math.round(ms / 1000);
  const minutes = Math.round(ms / 60000);
  const hours = Math.round(ms / 3600000);
  const days = Math.round(ms / 86400000);
  const months = Math.round(ms / 2592000000);
  const years = Math.round(ms / 31104000000);

  switch (true) {
    case seconds < 60:
      return `${seconds} second(s) ago"`;
    case minutes < 60:
      return `${minutes} minute(s) ago"`;
    case hours < 24:
      return `${hours} hour(s) ago"`;
    case days < 30:
      return `${days} day(s) ago`;
    case months < 12:
      return `${months} month(s) ago`;
    default:
      return `${years} year(s) ago`;
  }
};

const createdAt = new Date(2021, 0, 5);
fromAgo(createdAt); // 14 day(s) ago;
```


### Route Params Deserialization
```
const getPathParams = (path, pathMap, serializer) => {
  path = path.split("/");
  pathMap = pathMap.split("/");
  return pathMap.reduce((acc, crr, i) => {
    if (crr[0] === ":") {
      const param = crr.substr(1);
      acc[param] = serializer && serializer[param]
        ? serializer[param](path[i])
        : path[i];
    }
    return acc;
  }, {});
};

getPathParams("/app/products/123", "/app/:page/:id");
// { page: 'products', id: '123' }

getPathParams("/items/2/id/8583212", "/items/:category/id/:id", {
  category: v => ['Car', 'Mobile', 'Home'][v],
  id: v => +v
});
// { category: 'Home', id: 8583212 }
```


### Serialize to Query param string
```
const generatePathQuery = (path, obj) =>
  path +
  Object.entries(obj)
    .reduce((total, [k, v]) => (total += `${k}=${encodeURIComponent(v)}&`), "?")
    .slice(0, -1);

generatePathQuery("/user", { name: "Orkhan", age: 30 }); 
// "/user?name=Orkhan&age=30"

```

### Deserialize Query params
```
const getQueryParams = url =>
  url.match(/([^?=&]+)(=([^&]*))/g).reduce((total, crr) => {
    const [key, value] = crr.split("=");
    total[key] = value;
    return total;
  }, {});

getQueryParams("/user?name=Orkhan&age=30");
// { name: 'Orkhan', age: '30' }
```


### Array to nested object (recursive)
```
function proc2(arr){
const result = arr.reverse().reduce((prev, curr) => ({[curr]: prev}), {})
return result
}
```
Non-arrow version
```
function proc2(arr){
const result = arr.reverse().reduce(function(prev, curr) {
return ({[curr]: prev})
},"mostInnerValue");

return result
}
```

### Measure function or execution time (Log)
```
console.time('TEST')

//code in between

console.timeEnd('TEST')
```

### Logging array of objects
```
// x,y,z are objects
console.table([x, y, z])
```


### Image modal to Gallery
```
/*Scenario is: there are images (duh), when clicked they open in modal. Task is to make it so that there'll be "next and prev" buttons like a gallery, and it is expected to behave respectively.*/

  $('.view-modal').on('hidden.bs.modal', function () {
              resetActiveImage();
            });

            function resetActiveImage(){
                document.querySelector(".activeImage").classList.remove("activeImage");
            }
            document.querySelector(".modal-next").addEventListener("click",function(e){
                changeModalImage(true);
            });
            document.querySelector(".modal-prev").addEventListener("click",function(e){
                changeModalImage(false);
            });
            function changeModalImage(isNext){
                let nextImg;
                let currModal=document.querySelector("#PreviewModal");
                let currImg=document.querySelector(".activeImage");
                if(isNext){
                    nextImg=currImg.closest(".image-item").nextElementSibling.querySelector("img");
                }else{
                    nextImg=currImg.closest(".image-item").previousElementSibling.querySelector("img");
                }


                $("#PreviewModal").attr('src' , nextImg.src);
                resetActiveImage();
                nextImg.classList.add("activeImage");
            }

```
```
/*CSS for arrows*/

.modal-next{
    position: absolute;
    right:-6rem;
    border-radius: 50%;
    background-color: #717171;
    color:#fff;
    top:50%;
    font-weight: bold;
    padding: 1rem;
    font-size: 3rem;
    transform: translate(0, -50%);
    border:0;
    width: 5rem;
    height: 5rem;
    opacity: 0.7;
}

.modal-prev{
    position: absolute;
    left:-6rem;
    border-radius: 50%;
    background-color: #717171;
    color:#fff;
    top:50%;
    font-weight: bold;
    padding: 1rem;
    font-size: 3rem;
    transform: translate(0, -50%);
    border:0;
    width: 5rem;
    height: 5rem;
    opacity: 0.8;
}
```
```
<!--Add this as a sibling to modal-content -->
 <button class="modal-prev">
            <
        </button>
```

