
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
