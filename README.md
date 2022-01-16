# Rust Workshop - lesson 2

So, we have learnt about and you have most probably setup the rust-lang developer environment on your machine, with rustup. If not, you can still follow along for most of this lesson by logging onto https://play.rust-lang.org, to try out what we are about to learn. Lets get started.

As a rust programmer, the first program that you need to know about, much like the rest of them is one to print "Hello, World!". This is what it might look like:
```rust
fn main() {
  println!("Hello, World!");
}
```
Here, we are introduced to two important concepts in rust, functions and macros. Functions take in input and produce an output and in this example, `main()` is a function that takes 0 inputs and gives 0 outputs. Well, not exactly, but lets think of it that way. Macros on the other hand are different in that they are just replaced by more code when expanded, i.e. `println!(..)` expands to code that actually formats the string, sends it as input to the underlying system libraries that then interact with the hardware to print to screen, makes sense?

### Why should I learn about functions and macros?
There are a lot of treats that you can pack into your programs by making use of functions and macros when necessary. The second most important aspect of writng code, after making it executable ofcourse(duh), is to make it readable, not just for others, but for yourself. Code readability will greatly improve your productivity when you get back to your code in the future, believe me. Functions help you make your code readable as they greatly reduce repetitive code, you can just shove code that does something into a function and call it multiple times, let's see an example:
```rust
fn main() {
  println!("1 + 2 = 3");          // We know about printing stuff already
  println!("1 + 2 = {}", 1 + 2);  // With the ability to format code, we can actually let rust do the calculation for us and place the result in the output
  print_add(1, 2);                // This is a function call, we just pass values to a function that does everything from here on...
  print_add(3, 3);
  print_add(1, 10);
}

fn print_add(a: i32, b:i32) {     // We define a function that takes in two i32 values and prints them along with their sum to screen using println!()
  println!("{} + {} = {}", a, b, a + b);
}
```
We will learn more about functions later, but it's enough to know that they take inputs and give outputs and in-between perform some computations that is defined inside them, they are most effectively used when you have to make these calls multiple times.

Macros on the other hand are parts of your code that get filled-in when you compile. They are a slightly more complex topic and for that reason, we won't delve into them much, but do keep in mind that they only have an impact on your compilation, while functions actually are separate computing blocks that have some impact on the execution of your code.

### Aight, where do I go next?
Write your own functions and use macros like `println!()`, `format!()`, etc. Once you are done, checkout the `lesson-3` branch.
