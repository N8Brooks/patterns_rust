# Idioms

## [Use borrowed types for arguments](https://rust-unofficial.github.io/patterns/idioms/coercion-arguments.html)

### Prefer using the **borrowed type** over **borrowing the owned type**.

This is briefly covered in the [Rust Book](https://doc.rust-lang.org/book/ch04-03-slices.html#string-slices-as-parameters).

- `&str` over `&String`
- `&[T]` over `&Vec<T>`
- `&T` over `&Box<T>`

### The gist

It's better to use a reference to the static version because the borrowed heap types can be implicitly converted to the static versions.

## [Constructors](https://rust-unofficial.github.io/patterns/idioms/ctor.html)

Add a `impl Default for X` and a `fn new() -> X` always. Even if they are duplicated or new is empty. People just expected `new` to be there. Default is useful for `*or_default` functions!

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
