# Interview type: Code Review

## Goal
Reason for having these kind of interviews are to gather whether the candidate is able to:
- Analyze and understand algorithm and logic
- Measure your attention to detail
- Identify risks and bug
- Designate areas of improvements
- Provide constructive feedback
- Express yourself accurately and concise

## Characteristics to mount

Be;
- **Collaborative**
- Concise,clean, but not hard. Communicate effectively.
- Vigilant


## Preparation
- Read this guide, duh.
- Watch some coding review interviews
- If you have some prior code reviewing experience (as the author or reviewer) it is fine actually


## Tips

- Don't jump straight to judging and improving. First explore the domain, environment, algorithm, techniques, methodology and reasoning. Put yourself into the author's shoe
- Gather clues on the code author's reasoning. Why did they choose that over this, why they solved it like so, what was the idea behind this structure. Then after gathering enough clues to build up a hypothesis, confront the author to validate your hypothesis. Don't be harsh, aim to have mutual agreement on their reasoning.
- Deduce the reasoning. Just because they think "the floor is dirty" doesn't justify "traversing via monkeybars".
- Back your claims and theories. It sucks to make empty claims, because anyone above room temperature IQ would question and say "why?". So do your homework, hit them with your vast knowledge and encyclopedia. Resort to anectodes only when you're out of bullets, facts come first.
  - Per PSR-4, class names and folder structure should be...
  - This code section violates Liskov principle of the SOLID
  - This abstraction is incorrect because it doesn't allow for extension, hence violating open-close principle of the SOLID
  - What you're trying to achieve here is polymorphism, one of the pillars of OOP
  - MySQL best practices dictate that you shouldn't add random indexes, you should do them per cardinality and query capabilities.
  - As Dijkstra suggests, gotos are evil so abstain from using them.
- Categorize the issues. Blocking (requires immediate action), pebble (non blocking but annoys you whenever you interact with that code), sand (non blocking, requires future consideration for refactor)
- Be direct and concise. Don't do ambigious explanations like "be more precise with the naming" or "there are bugs here". Don't generalize.
