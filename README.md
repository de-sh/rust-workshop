# Rust Workshop - lesson 3

After having seen how we defined the function in the last lesson, you might have a few questions like, what's with the `:i32`? Well, since rust is compiled, it needs to know what kind of data functions will take in and give out, so we use "Type Annotations" to let the compiler know. We will now learn about variables, which are basically locations in memory that your program can access to read or write values to, which as we will demonstrate can be defined and initiated as follows:
```rust
let a = 1;                      // The variable is set with a generic type called {integer} and will be cast into a type based on later usage
let mut b = 1i32;               // We have annotated the type to the actual value when initiated, and also made it mutable, rust variables are by default immutable
b = 2;                          // Since b was defined as mutable, one can change it's value till the binding exists, given the new values are also of the same type(i32)
let c: i32 = 1;                 // The variable is defined with a type annotation and defined on the same line
let d: String = "Hello".into(); // Types can have methods like .into() and T::from() that allows the programmer to perform type conversion
```
Note, as you can see we use the let keyword to perform variable definition.

Similar to how variables are annotated, functions can be annotated as follows:
```rust
fn hello(name: &str) -> String {  // A function that takes in a raw string reference and returns a String type
  "Hello, ".to_string() + name + "!"
}

fn add(a: i32, b: i32) -> i32 {
  a + b
}

fn float_to_in
```

### Why are we learning about types again?
Rust as a language tries to make sure that the programmer has specified everything necessary to make sure that the program doesn't screw-up. As a part of this caution, it runs a tool called the type checker on your code, making sure that all variables have the right type and are being used properly. Expanding on this is the concept of borrow checking, which is what makes rust a whole lot better for writing memory safe code. Why? Because it ensures that variables in code are allocated memory and when the times comes, also deallocated properly. Thus we end up having no part of the code refering to any location in memory that is not actually holding values that the code supposedly thinks it should. All this without having to do stuff such as garbage collection(a concept you'll be familiar with if you have used python/java/golang).

To explain the above with an analogy, take the example of a neighbourhood that has many homes, each home being able to house a single person, with each house getting an address and you are the phone operator who's supposed to route calls coming in for the folks living in the neighbourhood. The calls are supposed to reach the end-person, no matter if the person changes homes, has a second address for their office, or in the case that such a house doesn't actually exist, in which case the call shouldn't be allowed in the first place. This is exactly what the concepts of ownership, borrowing and lifetimes manages to achieve for your code, i.e. making sure that at no part your code is trying to call(access) a house(variable) that doesn't actually exist anymore. To write the above as code, consider the following:

```rust
fn main() {
  let a = 1;
  let b = a;
  println!("{} : {}", a, b);
}
```
The above should compile and run properly, because types such as i32 are small and easy to copy, but when you consider larger/bulkier objects like string which are tough to keep copying, this isn't the response.

```rust
fn main() {
  let a = "Hello".to_string();
  let b = a;
  println!("{} : {}", a, b);
}
```
As you might have noticed, the compiler won't let you compile the code because: "move occurs because `a` has type `String`, which does not implement the `Copy` trait". To solve this, we could actually use the `clone()` method, which would create a whole new location in memory and perform what's known as a deep copy.

Why is all of this important to know? If you know the concept behind why copying is compute intensive, you can write more performant code, easy. Hope we are on the same page, let us continue.

### What shall I do now?
Try practicing your newly learned skill, dealing with types, to write code that takes two numbers as input from the user through the command line and outputs to screen their sum. Once you are done with that, head over to the `lesson-4` branch.
