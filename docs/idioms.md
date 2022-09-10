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
