# Polymorphism

Same interfaces applied (morph) for many different (poly) data types.

This is the tool of the man who doesn't care. In a good way. Explained in use-cases.

- Shared functionality
- Shared methods
- Shared application areas


1. Compile-time polymorphism
Just method overloading.

2. Runtime polymorphism
Method overriding



Analogy examples: 
- `int` and `float` are technically polymorphic, because they provide the same set of operations and extensions, such as addition (`+`) and substraction (`-`)
- All sea creatures `swim()`, but they `swim()` in their own style. 
- Cafe's have hundreds of various drinks from hot to cold, bitter to sweet, colorful to dreadful. But no matter what you choose, you always `drink()` it.



## Use Cases:

### `#1` Just Do It, I don't care how

```php
abstract class Terrestrial{

public abstract function walk():string;

}
```

```php
class Elephant extends Terrestrial{

public function walk():string{
  return "tump-tump";
}

}
```

```php
class Dog extends Terrestrial{

public function walk():string{
  return "pat-pat";
}

}
```

```php

$arr=[];
$arr[]=new Dog();
$arr[]=new Elephant();

foreach($arr as $animal){
echo $animal->walk();
}

```

---

`#2` Gimme something that can do something, I don't care how 


Consider this code:
```php
class WaterSource{

$pond=[];

public function addToThePond($swimmer):void{
    $pond[]=$swimmer;
    //echo different messages for each different animal type
}

}
```

How can I output different message for each animal type. Without polymorphism, it would look something like this:

```php
class WaterSource{

$pond=[];

public function addToThePond($swimmer):void{
    $pond[]=$swimmer;
    if(get_class($swimmer)=='Whale'){
      echo 'dude I'm drowning';
    }else if(get_class($swimmer)=='Frog'){
      echo 'Ribbit-ribbit, refactor it.';
    }else{
      //what am I gonna do, it is not some expected type ???? Because it is not guaranteed
    }
}

}
```

Here the similar thing with polymorphism. 


```php
abstract class Animal{

}
```

```php
interface SwimmerInterface{

function swim(WaterSource $waterSource):string;

}
```

```php
abstract class Aquatic extends Animal implements SwimmerInterface{

//notice that functions of SwimmerInterface is not implemented here, it is enforced on the child class

}
```

```php
class Whale extends Aquatic{

public function swim(WaterSource $waterSource):string{
     return "nice water source man (?), it's hella deep.";
}

}
```

```php
abstract class Amphibian extends Animal implements SwimmerInterface{

//notice that functions of SwimmerInterface is not implemented here, it is enforced on the child class

}
```

```php
class Frog extends Amphibian{

public function swim(WaterSource $waterSource):string{
     $waterSourceName=$waterSource->name;
     return "yeahh, I'm swimming in ${waterSourceName}. ribbit-ribbit...";
}

}
```


```php
class WaterSource{

$pond=[];

public function addToThePond(SwimmerInterface $swimmer):void{
    $pond[]=$swimmer;
    echo $swimmer->swim();
}

}
```



