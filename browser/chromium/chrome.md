"Great power comes with great responsibility."

Well it's like that old friend from high school who is pretty successful. You might ask him to do you a favor, but it is certain that he is an arse-hole. And it's no surprise since chrome is a proprietary software. There could be ton of zero-day exploits, some anti piracy mechanism or a watchdog which violates privacy rights.

Yeah it's fast, updates smoothly (looking at you firefox), doesn't have obvious bugs. But since it's proprietary, it starts the race far behind in comparison, it's a giant con.



### Idle Detection API

I don't know which one of y'all thought of this but you either didn't think it through or just don't give a damn anymore. I know it's possible to implement your own idle detection mechanism in JS, fairly easy. But helping everyone use it out-of-the-box might not be the greatest idea.

**Thankfully it's a decision-based API, you can easily opt-out. Dodged a bullet here for sure.**

#### Possible maleficent use cases:
- Ad services: can stop playing the ad if you  aint active. I mean everyone does that if ads are forced, you just look around, browse other tabs etc. And its fun to piss-off ad publishers. But after idle detection API it'll no longer be possible. 
- Mine crypto coin when user is idle.
- Charter time scheme of a person. How often they get up to go to toilet, when do they have lunch, do they use the computer on lunch.
- Home-office physical intrusion. Assume that i were to develop an app for certain people to use. And since now i can detect if they are idle or not, i can do a home-intrusion comfortably. E.g when door is broke down, i can know if they heard it or not. Disclaimer: don't do home-intrusion. Just don't.
- Spying on your employees, like c'mon. 
//meme here
//maybe also pepe


#### Beneficent
- Logout off app authentication and return to main screen. Banking, sensitive information apps, chat apps and more.
- Show some notification, a zen-desk pop-up
