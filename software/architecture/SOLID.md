# SOLID

## S.O.L.I.D stands for
- Single responsiblity (hell yeah)
- Open closed
- Liskov substitution
- Interface segregation
- Dependency inversion


## Glossary:

### Cohesion: basically similary of elements in a cluster.
We strive for high cohesion, it means all methods and functions that does similar actions in a context are grouped together. Low cohesion is basically god class, all my homies hate it.

Grouping/Clustering can be made according to responsibility, similarity or alternatibility (not sure if this is an actual word).

### Coupling
Dependency between components. Not sure if agree with this one. If there is slim-to-none dependency between components that means you're probably doing many unrealted actions in said component.




## Single Responsibility

### Single reason to change
IMHO this is some utopian bullcrap. If you really aim to have one reason to change for each software component in a goddamn triple-A big-corpo multinational titan of a software it will take centuries to develop. Like one terrible manager once said "Come on, we are an Agile company. Deploy it now. !" (production goes down in a moment). Single responsibility is far more logical compared to this. And they are NOT the same.

## Open Closed

### Oper for extension, closed for modification
Write once, extend everywhere. After a software component is done, it's a big no to modify it. It should be developed it such way that it can easily be extended/inherited. 

**Do not follow this principle blindly, or it'll overwhelm your whole system.**

Imagine this scenario:

```
public funtion calculateWolfProwess(Wolf $wolf){
return $wolf->prowess;
  
  
}
```
But what if we also started to integrate birds, giraffes, elephants (you're cool), penguins etc. This function would have to be cloned and Wolf model parameter has to change, to reflect override. Like so:
```
public funtion calculateWolfProwess(Wolf $wolf){
return $wolf->prowess;
  
  
}

public funtion calculatePenguinProwess(Penguin $penguin){
return $penguin->prowess;
  
  
}
public funtion calculateElephantProwess(Elephant $elephant){
return $elephant->prowess;
  
  
}

```

And this sucks big time. How about we do it like this.

```
(A new model, Animal)
class Animal{
public $prowess;
}

class Wolf extends Animal{
}
class Elephant extends Animal{
}
class Penguin extends Animal{
}

public funtion calculateAnimalProwess(Animal $animal){
return $animal->prowess;
  
  
}
```

Now we can have thousands of animals integrated and our little function won't ever fail and we won't have to add any hotfix or not-sure implementations.



## Liskov substitution

"If it looks like a duck, and quacks like a duck, but it needs batteries; then you have wrong abstraction."

Basically this principle says: All child objects should be able to replace their parents. In other words, whatever method does parent have, child gotta implement them (override or just inherit). **Not sure if this applies to only immediate inheritance or in-depth** Take this example:

Before:
```
class Mammal{

  public function getArmLength(){
    return $this->arm_length;
  }

}
```

```
class Penguin extends Mammal{

  public function getArmLength(){
    //penguins don't have arms, they have flippers (or wings if you are illiterate)
    throw new NotImplemented;
  }
  //therefore there this violates liskov subsitution principle. We have to change abstraction and inheritance.
}
```

After:

```
class Animal{
  //pretty much is a interface actually
  public function getPrimaryLimbLength(){
      //message to those who extend/inherit this, override it.
  }
}
```

``` 
class Mammal extends Animal {
   
   //overriding it
   @override
   public function getPrimaryLimbLength(){
      return $this->getArmLength();
   }
    
   public function getArmLength(){
      return $this->arm_length;
   }
}
```

```
class Penguin extends Animal{
   
   //overriding it
   @override
   public function getPrimaryLimbLength(){
      return $this->getFlippersLength();
   }
    
   public function getFlippersLength(){
      return $this->flipper_length;
   }
}
```


