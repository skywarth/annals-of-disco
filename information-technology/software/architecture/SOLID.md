# SOLID


## S.O.L.I.D stands for
- Single responsiblity (hell yeah)
- Open closed
- Liskov substitution
- Interface segregation
- Dependency inversion


## Conclusion:
- Single responsibility: Rules, absolutely makes sense.
- Open Closed: Sounds good, doesn't work. I mean do you honestly believe that we can simply make all those classes ready to be inherited ??
- Liskov substitution: Duh, it's cool.
- Interface Segregation: meh, pretty similar to Liskov anyways.
- Dependency Inversion: Dependency Injection is great and prohibiting relation between high and low level modules DIRECTLY is logical. But for real, we can't create 5 classes with complex dependency if we can do it with 2 class and simple call. Ain't nobody got time for that ??


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

### Break the hierarchy

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

### Tell, don't ask

If you hold an array/collection/generic/list etc. with type of a parent class (like so: ```List<Animal> animalsList=new List<Animal>();```), and you have condition like this while iterationg/deleting/inserting/updating over it similar to ```if(someHorse.GetType() == typeof(Dog))``` you are probably doing something wrong. A generic collection/array/whatever should work seamlessly with all it's children as much as possible.


## Interface Segregation (ISP, p for principle)

"No clients should be forced to depend on methods it does not use"

What the hell, this is the same as Liskov substitution ??

Whatever methods does an interface has, it should be present (and non-blank) in those who implement it. Also don't group unrelated behavior in one interface. Split them.

### How to identify
- Chonker interfaces
- Low cohession (unrelated elements)
- Empty overloads, implementations to trick OOP gods


## Dependency Inversion (DIP, p for principle)
> "High-level modules should not depend on low-level modules. Both should depend on abstractions."

> "Abstraction should not depend on details. Details should depend on abstractions."

> "When a change occurs in High Level modules, child modules should comply and change themselves to fit/suffice. But when a low level module experiences a behavioural change, it shouldn't affect high level modules."


In really short summary: high level class should directly aggregate/contain low level class instances like so:

**Without DI**
```
class Chef{
    public Oven $oven=new Oven();
    cook(){
        $oven->heat();
    }
}

class Oven{
    heat(){
        $oven->heat();
    }
}
```

As you can see, `Chef` class is tightly coupled with `Oven` class. Because if a change is to occur on `Oven` class, it would devastate the `Chef` class. So we can put a layer of abstraction to isolate us from the shenanigans of the low-level `Oven` class: 

**With DI**
```
class Chef{
    public HeatingDevice $heatingDevice=new Oven();//you may apply dependency injection 
    cook(){
        $heatingDevice->heat();
    }
}

interface HeatingDeviceInterface{//may as well be a abstract class too
    heat();
}

class Oven implements HeatingDeviceInterface{
    heat(){
        $this->turnOnGas();
        $this->lightTheGas();
    }
    
    turnOnGas(){
    //stuff
    }
    
    lightTheGas(){
    //other stuff
    }
}

//you may even define and integrate Microwave class easily
```





Can't say i'm the biggest fan of this one.
For example, a controller shouldn't depend on some service/repository/model directly. Scenario: 

Before implementing this principle:

```
class CarController(){
public function carsList(){
  $carServiceInstance=new CarService();
  $cars=carServiceInstance->getCars();
  return response()->json($cars);
}
}
```
```
class CarService{
public function getCars(){
  return Car::all();
}
}
```

As you can see, high level module CarController's carsList() method tightly depends on low level module CarService's getCars() method. This breaks the principle. To fix this:
```
class CarController(){
public function carsList(){
  ICarService $carServiceInstance=CarServiceRepository::create(); //mind the variable type
  $cars=$carServiceInstance::getCars();
  return response()->json($cars);
}
}
```

```
interface ICarService{
  public function getCars();
}
```

```
class CarService implements ICarService{
public function getCars(){
  return Car::all();
}
}
```

```
class CarServiceFactory(){
  public static create():ProductRepository{
      return new CarService();
  }
}
```

Now high level module is no longer dependent on low level module directly. Well if you ask me, now there is 4 classes/interfaces instead of 2. Yeah it probably reduced coupling but still a little bit too much of an overhead.

### Dependency Injection 

In this context; it means instead of creating the ICarService instance directly in the CarController, we add a construct method which takes a parameter with type of ICarService. Dependency injection greatly reduced coupling.

```
class CarController(){

protected ICarService $ICarServiceInstance;
public function __construct(ICarService $ICarServiceInstance){
  $this->$ICarServiceInstance=$ICarServiceInstance;
}

public function carsList(){

  $cars=$this->ICarServiceInstance::getCars();
  return response()->json($cars);
}
}
```

### Inversion of Control

Yeah Dependency Injection is cool and all but what if we wanted to isolate the injection process from the upper layer. Because it's bloating my workflow.

Most frameworks do this and has dedicated stuff related to it. E.g Java Spring IOC container, Laravel Service Container




