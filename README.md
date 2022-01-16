# Rust Workshop - lesson 4
This is a solution to the challenge in lesson 4. If you are here, either you are trying to verify your solution or otherwise don't worry, you have a long way to go, but you are still on track :)

As discussed in the challenge, we are supposed to get user input and update a value. Before we start writing the code, let us try and mock how the application must interact with the user. The CLI running the game would look something like:
```sh
$ cargo run
s: 0
Input operator: +
Input operand: 10
s: 10
Input operator: *
Input operand: 10
s: 100
Input operator: -
Input operand: 10
s: 90
Input operator: /
Input operand: 10
s: 9
```

Now that this makes some sense, let us start writing the code. For the state, I think we need a mutable integer, with the initial value of 0, let us call it s for simplicity:
```rust
fn main() {
  let mut s = 0;
  // continued
}
```

Next, we need to get user input from within a loop and perform operations on a, this calls for a quick internet search to find how we can get the user to input a character, specifically in rust-lang. The first result seems promising, here is the code I found over there:
```rust
fn user_input() -> String {
  let mut line = String::new();
  std::io::stdin().read_line(&mut line).expect("Failed to read line");
  
  line
}
```
As can be clearly infered from the annotations, everytime we call this function, we will get a line of input from the user, as a String. We must use the contents of this string according to our requirements, the first of which would be to just take the initial character in the user input and take it as the operator, I'll use some web searches to figure it out as well. We'll also put this in the loop:
```rust
// continued
loop {
  println!("s: {}", s);

  print!("Input operator: ");
  let input = user_input();
  let op = input.chars().nth(0).expect("First character missing");
  // continue
}
```
Now that we have gotten the operator value, we need to get the operand(x), we'll consider it to be an i32 value, after some research, this is what I got:
```rust
// continued
print!("Input operand: ");
let input = user_input();
let x: i32 = input.parse().expect("Not an integer");
// continue
```
Now, we need to update the value of s, this can be achieved by writing a match function on the arithmetic operators '+', '-', '*' and '/' and performing the corresponding arithmetic operation with the given operand and s. In case op has some other character, we should do nothing, like:
```rust
// continued
match op {
  '+' => s += x,
  '-' => s -= x,
  '*' => s *= x,
  '/' => s /= x,
}
```
With this, we will end up with a program that looks like the following:
```rust
fn user_input() -> String {
  let mut line = String::new();
  std::io::stdin().read_line(&mut line).expect("Failed to read line");
  
  line
}

fn main() {
  let mut s = 0;
  loop {
    println!("s: {}", s);
    
    print!("Input operator: ");
    let input = user_input();
    let op = input.chars().nth(0).expect("First character missing");

    print!("Input operand: ");
    let input = user_input();
    let x: i32 = input.parse().expect("Not an integer");

    match op {
      '+' => s += x,
      '-' => s -= x,
      '*' => s *= x,
      '/' => s /= x,
      _ => println!("Not an operator"),
    }
  }
}
```

### Why did we do this again?
Rust has a lot of uses, it can be used to write everything from a CLI application like this game to simulation software and complex cloud infrastructure. But one thing that will be very common in all of them is the use of control flow syntax that is very similar to what we have written. Cheers, you are well on your way to becoming an ace rustacean, checkout the `lesson-5` branch to learn more about Structures and Enumerators.