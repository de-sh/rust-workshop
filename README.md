# Rust Workshop - lesson 4

So far we have learnt about the rust compiler, writing code that is readable using functions and macros and about some of the types in rust-lang. Though we have only begun, now seems like the right time to introduce you to the concept of control-flow, especially what we have in rust-lang.

If you are familiar with any other programming language, you are sure to have used a few of them, but let's see them in code and figure out how we can use it to make our program actually do stuff.

## Why should you learn about control flow?
Because it is the heart of almost every programming language. What is the use of a program that you can't use to do stuff? The actual doing of stuff requires the computer to keep moving forward, perform something, something else and so on. This includes doing something if the conditions are right, repeating a set of actions while a particular set of conditions are met, perform something for all objects in a group and so on... 

We will start out with conditional statements. In rust, it's as simple as using the key words `if` and `else`. Say you have a number a, you must only print it's value if it is either 1 or -1, the code might look something like this:
```rust
fn main() {
  let a = _;      // set the value as you wish
  if a == 1 || a == -1 {
    println!("{}", a);
  }
}
```
You might know of most of these as the regular old equality and logical operators. To the above program, we can add another block that adds 2 to a and then print the result if it is neither 1 nor -1:
```rust
fn main() {
  let a = _;      // set the value as you wish
  if a == 1 || a == -1 {
    println!("{}", a);
  } else {
    println!("{}", a + 2);
  }
}
```
You can achieve the same with lesser code by converting this into a single line of code like:
```rust
fn main() {
  let a = _;      // set the value as you wish
  println!("{}", if a == 1 || a == -1 { a } else { a + 2 });
}
```
This actually decreases your code's readability, hence writing code like this is not a recommended practice.

You can add more complex conditions such as "if neither 1 nor -1 but odd, subtract 3 and print value", which would look something like:
```rust
fn main() {
  let a = _;      // set the value as you wish
  if a == 1 || a == -1 {
    println!("{}", a);
  } else if a % 2 == 1 {
    println!("{}", a - 3);
  } else {
    println!("{}", a + 2);
  }
}
```

Rust also allows you to write repetitive code, like if you want to print to screen while a number is positive and being decremented in value:
```rust
fn main() {
  let mut a = 100i32;
  while a.is_positive() {
    println!("{}", a);
    a -= 1;
  }
}
```
If you are coming from a language like C/C++, java, you might be slightly sadened by the lack of the `++`/`--` keywords, but don't fret, it's for the better :D

The above program seems to have been written by someone who wasn't very considerate of the fact that all positive numbers starting from 100 down are in a range, this is where rust's range operators come in handy. Here's an example of what I mean:
```rust
let r = 0..100; // Numbers 0, 1, 2... 99 (not inclusive of 100)
let s = 0..=100; // Numbers 0, 1, 2... 100(inclusive of 100)
```
Ranges are iterable, i.e. you can go from one to the other, this is achieved by using the concept of iterators. You can use iterators to perform repetitive tasks with the help of `for` keyword. Reimplementing the earlier example we get:
```rust
fn main() {
  for a in (1..=100).rev() {
    println!("{}", a);
  }
}
```
Much simpler and easier to read, no? Now let's learn about the loop keyword. Repetition needs a simple loop, but only if you have a stopping condition should you use `while`/`for`, if you want a forever loop, which is possible with `while true`, you should use the `loop` keyword instead. This you can use to keep getting user input like:
```rust
loop {
  let input = _;          // Get user input here, you might have to use something like stdin, we will cover this later
  println!("{}", input);  // Print it to screen
}
```

As we were mentioning above with conditionals, there's a better way to handle more complex ones. Say you have to perform a  calculation depending on the arithment operator the user inputs along with the two numbers, you can achieve that with the help of the match key word, as follows:
```rust
fn calculate(op: char, a: i32, b: i32) {
  match op {
    '+' => println!("{} + {} = {}", a, b, a + b),
    '-' => println!("{} - {} = {}", a, b, a - b),
    '*' => println!("{} * {} = {}", a, b, a * b),
    '/' => println!("{} / {} = {}", a, b, a / b),
    na => println!("Not an arithmetic operator: '{}'", na),
  }
}
```

You can write match statements that are more complex, similar to the `if`-`else if`-`else` ladder we wrote earlier, but with an added condition that multiplies any number between 2 and 10 with 5, no matter odd or even:
```rust
let a = _;
match a {
  2..10 => println!("{}", x * 5);
  1 | -1 => println!("{}", x),
  x if x % 2 == 1 => println!("{}", x - 3),
  x => println!("{}", x + 2),
}
```

We had earlier learnt about functions, these can also be incorporated as part of the program's control-flow. Recursion is basically iteration, but using funtions, let's see how this is achieved in rust by reimplementing an earlier example:
```rust
fn iterate(a: i32) {
  if a > 0 {
    println!("{}", a);
    iterate(a-1);
  }
}

fn main() {
  iterate(100);
}
```

## But why are we learning this?
As mentioned earlier, control flow is an important part of programming. We can use it to build something like a game...

### Games? I am all ears, how do I build a game?
Not exactly a game, we will be writing a simple rust project to take inputs from the CLI and perform actions on as set of state variables and display the consequences of the users various actions, kind of like a game. This is the first challenge of the workshop, go and write a loop that takes user inputs and updates a value which was initially set to 0 and then after each update, display it on screen. (HINT: use `loop`, `match`, `stdin` and most importantly a bit of research and reading the documentation ;)

Once you are done, checkout to the `lesson-5` branch.

P.S: If you are stuck on the challenge, checkout to the `lesson-4-solved` branch