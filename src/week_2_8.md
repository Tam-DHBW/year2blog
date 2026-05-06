# Semester 2,  Week 8: Code Quality

Hello everyone!

This week was all about figuring out whether our code is actually good.

To do so, we gathered a bunch of metrics, which assign numbers to our codebase.
Our metrics are collected by Sonarqube, automatically on every push to our main branch.
This makes collecting the metrics really simple.

## Complexity
First of all, one of the most discussed metrics: complexity.
Sonar measures two types of complexity: Cyclomatic and Cognitive.

- Cyclomatic:

|Backend|Frontend|
|---|---|
|142|619|

- Cognitive

|Backend|Frontend|
|---|---|
|41|296|

# Lines of code

|Backend|Frontend|
|---|---|
|1747|5390|

# Duplicated lines of code
We are proud to say: We do not have a single duplicated line of code!
Everything is neatly DRYed out.

|Backend|Frontend|
|---|---|
|0|0|

# Code coverage

Testing is important to every serious software project,
however since this is just a toy project, only some parts of our codebase have unit test coverage.

|Backend|Frontend|
|---|---|
|17.7%|0%|

# Technical Debt

Sonar can measure "Technical Debt", the amout of time it predicts one would take to fix all found maintainability code smells.

|Backend|Frontend|
|---|---|
|16 Minutes |7 Hours 25 Minutes|

# Reliability

This metric tracks how "Bug-Free" our code is, using grades from A to E.

|Backend|Frontend|
|---|---|
|A|D|

Though for fairness, just a single large CSS file drags the frontend score in the mud.
Without thsi file the frontend also has a rating of A or B.

---

All in all, the amount of metrics sonar provides is quite impressive, especially for their free tier.
We can now be quite confident, that the backend already has pretty good code quality, and the frontend might need some more cleaning up and polishing.
Sonar also shows us which exact files and lines are dragging down our code quality, which makes refactoring quite straightforward.
