### ~~Lazy~~ Clever programmers alphabet
```
$alphabet=range('A', 'Z');
```

### Order in Alphabet
```
function orderInAlphabet($letter){
 return ord(strtoupper($letter)) - ord('A') + 1;
}
```

### ASCII value of a char
```
ord("a");
//uppercase differs!
```

### Iterate array (don't use this)
```
//8 times slower than foreach, don't use this
$test = array_fill(0, 10000, 'test_data');
array_walk($test, function($value, $index)
{
    $value = 'testdata';
});
//foreach equivalent
foreach ($test as $key => $value)
{
    $result[$key] = 'testdata';
}


```


### Array push
```
//is the arr first or second param ? lulz
//this is the reason i miss prototype functions, extensions 
array_push($arr, "apple");
```

### Array to string 
```
$comma_separated = implode(",", $array);
```


### Split a string into an array (by delimeter)
```
$pieces = explode(" ", $pizza);
```


### Uniques of an array
```
$unique = array_unique($arr); 
//this messes up the indexes, so maybe use it like this

$unique = array_values(array_unique($arr)); 
//basically array_values just changes indexes to numeric and order based.
```


### Amount of duplication for each duplicate in an array
*count duplicate amounts*

```
$counts=array_count_values($arr)

//Example var_dump($counts)
/*
array(8) {
  [20]=>
  int(2)
  [1]=>
  int(2)
  [-1]=>
  int(2)
  [2]=>
  int(2)
  [-2]=>
  int(2)
  [3]=>
  int(2)
  [5]=>
  int(3)
  [4]=>
  int(2)
}
//Means 5 as value has occured 3 times in the array.
*/

```
