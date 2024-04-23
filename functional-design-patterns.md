Functional programming emphasizes the use of pure functions, immutability, and higher-order functions to solve problems. While many traditional design patterns from object-oriented programming still apply in functional programming, there are also several design patterns specific to functional programming paradigms. Here are some common functional design patterns:

1. **Pure Function**: A pure function is a fundamental concept in functional programming. It produces the same output for the same input and has no side effects. Pure functions are deterministic, easy to test, and enable referential transparency.

2. **Immutability**: Immutability is a core principle in functional programming. Immutable data structures ensure that data once created cannot be changed. Instead of modifying existing data, functions create new data structures with the desired modifications, promoting safety and predictability.

3. **First-Class and Higher-Order Functions**: Functions are first-class citizens in functional programming languages, meaning they can be assigned to variables, passed as arguments to other functions, and returned as values from functions. Higher-order functions take one or more functions as arguments or return a function as a result, enabling composition and abstraction.

4. **Function Composition**: Function composition is the process of combining two or more functions to produce a new function. Functional programming encourages the composition of small, pure functions to create complex behaviors, enabling code reuse, modularity, and maintainability.

5. **Recursion**: Recursion is a powerful technique in functional programming for defining algorithms. Instead of using loops, recursive functions call themselves with modified parameters until a base case is reached. Recursion is commonly used for tasks such as tree traversal, list processing, and mathematical computations.

6. **Pattern Matching**: Pattern matching is a feature found in many functional programming languages that allows for concise and expressive pattern-based conditional branching. It enables deconstruction of data structures and matching them against patterns, facilitating elegant and readable code.

7. **Monads**: Monads are a design pattern used to encapsulate computations with additional context or side effects, such as error handling, asynchronous computations, or state manipulation. Monads provide a uniform interface for composing and sequencing computations, enabling modular and composable code.

8. **Functors, Applicatives, and Monads (FAM)**: Functors, applicatives, and monads are higher-level abstractions used to model sequential computations with side effects. Functors apply a function to a value within a context, applicatives apply a function in a context to a value in another context, and monads sequence computations in a context while handling side effects.

9. **Currying and Partial Application**: Currying and partial application are techniques used to transform functions with multiple arguments into a series of functions with a single argument. Curried functions enable function composition and create more flexible and reusable code.

10. **Memoization**: Memoization is a technique used to cache the results of expensive function calls to improve performance. By storing the results of previous function calls, memoization avoids redundant computations for the same inputs.

These functional design patterns help developers write concise, modular, and expressive code in functional programming languages, promoting maintainability, scalability, and correctness. By leveraging these patterns, developers can take full advantage of the functional programming paradigm and build robust and elegant software solutions.
