# Idioms

## [Use borrowed types for arguments](https://rust-unofficial.github.io/patterns/idioms/coercion-arguments.html)

### Prefer using the **borrowed type** over **borrowing the owned type**.

This is briefly covered in the [Rust Book](https://doc.rust-lang.org/book/ch04-03-slices.html#string-slices-as-parameters).

- `&str` over `&String`
- `&[T]` over `&Vec<T>`
- `&T` over `&Box<T>`

### The gist

## Cancatenating Strings with format!

`format!`

It's better to use a reference to the static version because the borrowed heap types can be implicitly converted to the static versions.

## [Constructors](https://rust-unofficial.github.io/patterns/idioms/ctor.html)

Add a `impl Default for X` and a `fn new() -> X` always. Even if they are duplicated or new is empty. People just expected `new` to be there. Default is useful for `*or_default` functions!

## The Default Trait

`impl Default for X`

## Collections are Smart Pointers

They can be implicitly dereferenced like in Preferring the **borrowed type**.

## Finalisation in Destructors

Destructors - `impl Drop for Foo` - are commonly used in place of `finally` paradigms from other languages.

## Keep owned values in changed enums

- Use `mem::take()` to move some value to a replacement when modifying its owner.
- If it doesn't implement the `Default` trait then you can use `mem::replace`.
- If you are working with the `Option` enum there is `option.take()`.

## On-Stack Dynamic Dispatch

- Lighter notes here because I don't plan on using this.\*

Uses the `dyn` keyword in place of a `Box`. Monomorphisation is the process of compiling code for different types. Since rust has dynamic dispatch it can avoid this. This is good because it avoids the heap.

## Foreign function interface (FFI)

_Lighter notes here because I don't plan on using this._

### Enums variants can have values

```rs
enum DatabaseError {
  IsReadOnly = 1,
  IOError = 2,
  FileCorrupted = 3,
}
```

## Iterating over an option

`Option` implements `IntoIterator`. It's like a collection with optionally 1 element. It can be used for cool stuff like `.chain()` on an iterator and `.extend()` on a vector. It can be mis-used such as running a `for` loop over it instead of using `if let x = Some(option)`.

## Pass variables to closure

Closures can capture variables, move variables with `move`, but usually you just need a few. Use a closure with rebinding.

## Private fields

### Adding a variant to an enum is a breaking change

To avoid this, initialize your enum with `#[non_exhaustive]` so that you can add stuff without it being a breaking change going forward.

### If you are doing so intra-crate

Then you can use private variants - variants that are not marked `pub`.

## Easy doc initialization

Talks about fairly advanced ways to write examples for documentation comments.

## Temporary mutability

Can add a new block specifically for a mutable version or redefine a variable as immutable.
