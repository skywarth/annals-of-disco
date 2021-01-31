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
