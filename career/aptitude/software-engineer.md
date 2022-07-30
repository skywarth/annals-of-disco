# Aptitude test

---

1. You have a calculator with a broken 'addition' (+) button. How do you do this calculation below. Try to define a rule if possible.

`(2+3)-4`
<details>
  <summary>Answer</summary>
  Write it like so to the calculator: ((-2-3)*-1)-4 
  Formula-rule: whenever + is encountered, wrap the each side of the sign in a parantheses and invert the content (just like boolean algebra "not, !") then multiply that parantheses with -1
  
</details>

---

---
2. Which of these are more distinct than others

A) Cube
B) Sphere
C) Square
D) Circle
E) Cone

<details>
  <summary>Answer</summary>
  E) Cylinder, because it doesn't have a corresponding two-dimensional shape for itself. E.g: Cube corresponds to square, Sphere to circle but cone doesn't correspond to any of them (it corresponds to triangle).
  
</details>

---


---

3. Assume you are in a maze. Walls are high and you can't see far away because it is so dark in here. You don't know your position in the maze and you have nothing on you. How do you get to the exit ? 

<details>
  <summary>Answer</summary>
  There are many solutions to this but 'touching the right wall and moving only right' might be the best. Answer is not confirmed yet.
  
</details>

---

4. You are in a catacomb. This catacomb features that each tunnel splits into two eventually, or it is dead end. So basically when you go down a tunnel it will either split into two new tunnels or it will be dead end where you'll face a wall. At the end of one of these tunnels there is a treasure. You have to find the treasure in least amount of time (time as in measurable unit, hours etc.). What is your strategy.

<details>
  <summary>Answer</summary>
  This one has so many different answers and almost all of them are true, participant is expected to provide an algorithm or technique that is somewhat effiecient in at least one metric.
  
</details>

---

---

5. There is a village that needs water distribution. Water source is infinite but we have to build a infrastructure to distribute it among all the houses. Problem is we have only wood as material and it is pretty scarce. Design a infrastructure that will use the minimum amount of wood to distribute the water to all the houses. Houses are placed in two rows, total of 6. So it's 3 houses next to each other and 3 other facing these houses.

House placement:

`X` represent houses, whereas `-` represent empty area.
```
X-X-X
-----
X-X-X
```
<details>
  <summary>Answer</summary>
  We basically expect bus network topology here
  
</details>

---



---

6. According to this sequance ` 1,2,3,2,1,9,10,11,10,9,121,122,123,122,121,... ` what is the next three numbers ?

<details>
  <summary>Answer</summary>
  Sequance repeats as: take the number three rows ago, get the square of it then increase it by 1 for 2 rows then reduce it by two rows. So answer is `15129, 15130, 15131`
  
</details>

---

7. You find a board with 3 switches and a led on it. You fiddle with switches and here is how the led responds:

```
Zero means off, 1 means on.
Switch_1, Switch_2, Switch_3, Led
- 0,0,0 => 1
- 0,0,1 => 1
- 0,1,0 => 0
- 0,1,1 => 0
- 1,0,0 => 0
- 1,1,0 => 1
- 1,1,1 => 1
```

<details>
  <summary>Answer</summary>
  Third switch is bogus, it doesn't affect anything. If switch_1 and switch_2 has the same value, led is on. Just like XNOR gate in logical circuits.
  
</details>

---

8. You opened your first warehouse. It is currently empty but the products are on their way to fill it to the brim. Incoming products properties range between these:

```
Weight: 200-220 Kilograms (don't consider grams, only kilos)
Color: Red, green, blue, cyan, magenta, yellow, black
Shape:  pentagonal prism, tetrahedron (or triangular), cube, hexagonal prism
Is urgent: yes, no
content type: live animal, meat products, stuffed animal 
```

What is strategy when placing these items in your warehouse, so you find find them easily and fast when needed.

---
