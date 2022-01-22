# Programming Questions

***
- In a standard MVC architecture based framework, how are variables and sessions shared for the application ? Is it true that for each user, an instace of the program will be created. Are static varibles shared between individual sessions/users. (Web App). Language is PHP or C#.

*Well I think it depends on how the given module (controller/service) is initialized.If dependency injection is in effect, then yes it'll be shared.*
### Assume the following scenario 
*Pseudo code*
```
public class  foo{
public static bar=5;//Careful, not const.

}
```
```
//Now user [A] on A1 client(computer and network) connects to the web app and through some  API method this line gets executed: 

foo.bar=8;//exact timestamp for this action is UTC 4:30 PM 
```
```
//Another user [B] on B1 client(different computer and network) connects to web app at (UTC 4:20 PM) and through some  API method this line gets executed

console.log(foo.bar);//exact timestamp for this action is UTC 4:32 PM 

//What is the output ?
```

***
