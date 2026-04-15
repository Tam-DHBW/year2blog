# How I (Bogdan) Learned to Refactor Legacy Java Code (Without Breaking Everything)

I'm not a Java developer. And I just had to get that out of the way. Here's what I did, step by step.

## The Starting Point

The project was a simple movie rental store — a classic example, apparently based on Martin Fowler's refactoring book. Three classes: `Movie`, `Rental`, and `Customer`. The `Customer` class had a `statement()` method that did... well, everything. It calculated rental amounts, figured out bonus points, and built the output string — all in one big method.

It worked. But it was messy. Even though we love to say "If it's works, don't touch it", there is a way to tocuh without breaking ->

## Before Touching Anything: Get It Running

First things first — I couldn't even run the project. There was no build tool, just raw `.java` files. I learned that Java needs to be compiled aka (`.java` → `.class` files) before you can run it, and doing that manually every time is painful.

So I set up Gradle. Created a `build.gradle` file that handles compiling, dependency management, and running tests. One command — `gradle build` — and everything compiles and tests run. That was a game changer.

I also added a `.gitignore` to keep compiled files and build artifacts out of git.

## The Refactoring Rhythm

Here's the pattern I followed for every change:

1. Run `gradle build` — make sure tests pass
2. Make one small change
3. Run `gradle build` again — still green?
4. Commit with a clear message
5. Repeat

Small steps. That's the whole secret. And here I could say my ultimate refactoring Guide is complete ;). Buuuut here all the changes made:

## Change 1: Move `amountFor()` to Rental

The `Customer` class had a method called `amountFor()` that calculated how much a rental costs. But it only used data from `Rental` and `Movie` — it didn't need anything from `Customer`. So I moved it to the `Rental` class and renamed it to `getAmount()`.

The logic stayed exactly the same. I just put it in the class that owns the data. The only thing that changed was replacing `each.getMovie()` with `getMovie()` — because now the method lives inside `Rental`, it doesn't need an external reference anymore.

```
refactor: move amountFor() from Customer to Rental
```

## Change 2: Move Frequent Renter Points to Rental

Same story. The `statement()` method had this chunk of code calculating bonus points — checking if a movie is a new release, if it was rented for more than a day, etc. All of that logic depends on `Rental` and `Movie` data, not `Customer` data.

I created `getFrequentRenterPoints()` on `Rental` and replaced the inline logic in `statement()` with a simple call.

```
refactor: move frequent renter points calculation to Rental
```

## Change 3: Modernize the Collections

The code was using `Vector` and `Enumeration` — Java 1.0 stuff. I swapped them for `ArrayList<Rental>` and a for-each loop. Cleaner, type-safe, and no more manual casting.

```
refactor: replace Vector/Enumeration with ArrayList and for-each loop
```

## Change 4: Separate Calculation from Formatting

The `statement()` method was still doing two things: calculating totals and building the output string. I extracted `getTotalAmount()` and `getTotalFrequentRenterPoints()` as separate methods. Now `statement()` only handles formatting — it asks for the numbers instead of computing them.

```
refactor: extract getTotalAmount and getTotalFrequentRenterPoints from statement
```

## What I Learned

- Refactoring isn't about rewriting code. It's about moving things to where they belong, one small step at a time.
- Tests are your safety net. Without them, you're just hoping nothing broke.
- Each commit should be one logical change. If something goes wrong, you can pinpoint exactly where.
- The code doesn't have to be perfect after one pass. Each round makes it a little better.
- Or just write good code in the first place lol 

---

## How Kiro's Spec Mode Could Have Helped

Now, there's another way I could have approached this whole thing — using my fav agent Kiro (which is btw made by Amazon). Using Kiro's spec mode. Let me explain how that works and what it have looked like. Funny enough, since I didn't exactly knew how this mode works, Kiro wrote the way it's works with spec mode as well.

### What Is Spec Mode?

Kiro has a feature called specs, which is basically a structured way to plan and execute a feature or refactoring task. Instead of jumping straight into code, you iterate with Kiro through three phases:

1. **Requirements** — You describe what you want to do. Kiro helps you formalize it into clear, specific requirements. For my case, that would be something like: "Refactor the Customer class to move business logic to the appropriate classes, modernize legacy collections, and separate concerns in the statement method."

2. **Design** — Kiro proposes a technical design based on the requirements. It would outline which methods move where, what the new class structure looks like, and what the expected behavior should be. You review it, give feedback, and iterate until the plan makes sense.

3. **Tasks** — The design gets broken down into concrete implementation tasks — small, ordered steps. Each task is a specific change, like "Move amountFor() from Customer to Rental" or "Replace Vector with ArrayList." Kiro then works through them one by one.

### How It Would Look for This Refactoring

Instead of me figuring out the order of changes and what to move where, I'd tell Kiro: "I need to refactor this movie rental codebase. The Customer class is doing too much."

Kiro would analyze the code and come back with a structured plan:

- **Requirements**: Clean separation of concerns, move business logic to domain classes, modernize legacy Java patterns, maintain existing test coverage.
- **Design**: `Rental` gets `getAmount()` and `getFrequentRenterPoints()`. `Customer` uses `ArrayList<Rental>` instead of `Vector`. `statement()` delegates calculations to extracted methods.
- **Tasks**:
  - Task 1: Move `amountFor()` to `Rental`
  - Task 2: Move frequent renter points logic to `Rental`
  - Task 3: Replace `Vector`/`Enumeration` with `ArrayList`/for-each
  - Task 4: Extract `getTotalAmount()` and `getTotalFrequentRenterPoints()`

Each task gets executed, tested, and I can review the changes before moving on. The spec also serves as documentation — anyone looking at the project later can see exactly what was planned and why.

### Why That's Useful

The big advantage is that you think before you code. When I did it manually, I had to figure out the right order of changes as I went. With spec mode, the plan is laid out upfront. You can spot issues in the design phase before writing a single line of code.

It's also great for bigger refactorings where the scope is less obvious. My project was small — four classes. But imagine doing this on a codebase with dozens of classes and complex dependencies. Having a structured plan with incremental tasks keeps you from getting lost.

The spec becomes a living document. You can reference it, share it with teammates, and use it to track progress. It's refactoring with a map instead of wandering through the code hoping you end up somewhere good. And as a cherry on top of a pie you can add ALL of your documentation as reference for Kiro just by adding a documentatio folder.
And if you want to check the repo out: here you go: https://github.com/Bogdan1323234/Refactoring-by-Fowler
