# Does switch expression make sense?
An analysis if switch expression make any sense in modern code base.

# Introduction
Every now and then, I hear that a modern C# feature like `switch` expressions are bullshit. Programming (*do not confuse programming with software development*) is a complex task. It is definitely dynamic, challenging and time-to-time opinion based.

I made this repo as a proof with hard core evidence how much equivalent are `switch` cases and `switch` expressions.

As a main metric, I've used a build-in Visual Studio Code Metric analyser with the Maintainability index. The code maintainability is popular buzzword these day because a maintenance of the obsolete, non-transparent code is expensive.

# Analysed function definition
A task is simple. Design a function which analyses an input object and if it is a string, return "One word" if string has `Length` property is lower than 5, "God knows what" for any another `string` and an empty `string` when the input object is not a `string` at all.

# Solution
I designed several solutions that I could come up with. They are sorted according the maintainability index in ascending order.

## 1. Junior developer solution (MI 77)
A very poor solution based on C# 6, coding style around 2015 and lack of experience.

![Preview](/Assets/MI77.png)

## 2. Junior developer solution (MI 78)
Same as before, just some reduced nesting at `if` statement.

![Preview](/Assets/MI78.png)

## 3. Solution with switch/case and some pattern matching (MI 81)
Another example of nasty code. The code is avoiding a nesting in `if` statement and uses a simple pattern matching with condition. Still quite a mess. Multiple return statements are a code smell.

![Preview](/Assets/MI81.png)

## 4. Solution from a (tired) senior developer (MI 88)
This solution has a single return statement. That is good. It used good old ternary operator to branch runtime flow. What is a code smell is a negative condition test `!(expression)`. This is one of the classic code smells that could easily avoided, see below.

![Preview](/Assets/MI88.png)

## 5. Clean solution by switch/case (MI 88)
A clean, old-fashion `switch` and `case` solution from a senior developer. This could be accepted solution for this task. It is easy to read, easy to extend but it has a ton of boiler plate code. If the business logic would require more switch/case branches, you would end up with boring, repeating typing. This is a reason why we have a switch expressions at the first place.

![Preview](/Assets/MI88-1.png)

## 6. Not really good solution (MI 89)
Believe or not, this solution based on the ternary operator that is not the best in easy-to-read discipline has higher maintainability index than the previous solution. Why? It has less boiler-plate code, lower cyclomatic complexity so you need less unit tests to cover it.

![Preview](/Assets/MI89.png)

## 6. Switch expression solution (MI 90)
And the winner is... Surprise, surprise... A solution based on the switch expression. Why? Well, it was design to reduce the boiler-plate code and speed up the coding. It produce the least amount of source code that a quite easy to read.

![Preview](/Assets/MI90.png)

# Conclusion
In this simple task, we can see that the `switch` expressions actually have some positive impact at code base and based on this fact, we can conclude that the **switch expressions should not be avoided in modern C# code bases**.
