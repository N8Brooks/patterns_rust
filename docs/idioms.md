# Idioms

## [Use borrowed types for arguments](https://rust-unofficial.github.io/patterns/idioms/coercion-arguments.html)

### Prefer using the **borrowed type** over **borrowing the owned type**.

This is briefly covered in the [Rust Book](https://doc.rust-lang.org/book/ch04-03-slices.html#string-slices-as-parameters).

- `&str` over `&String`
- `&[T]` over `&Vec<T>`
- `&T` over `&Box<T>`

### The gist

It's better to use a reference to the static version because the borrowed heap types can be implicitly converted to the static versions.
