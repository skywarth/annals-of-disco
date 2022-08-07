# Best practices for conditions statements


## 1. Return early
`debatable`
If the conditions are distinct and exclusive, it might be valid strategy to return early. By return I mean anything that can end the execution of the subroutine. E.g: throwing exception, return statement...
```
function fizz(state) {
  if (state instanceof buzz) {
    return "Nooo you can't just .....";
  }
  if (state>50) {
    throw new NopeException("this ain't it fam")
  }
  return "Suceess";
}

```
