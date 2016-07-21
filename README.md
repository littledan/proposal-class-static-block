# Static blocks for ES classes

This proposal defines static initialization blocks which run in the scope of the class.

## Motivation

Classes create a nested scope for their execution. Within this scope, there is
- An immutable binding of the class itself
- In the [Private Fields](https://github.com/tc39/proposal-private-fields) proposal, the ability to read and write private fields of instances which is inaccessible externally
- (more?)

This proposal gives syntactic space for some code to run within the class scope, at the time the class definition is executed. The static blocks may be used to share getters or setters for private with particular chosen friends.

## Examples

```js
let barGetter;
class Foo {
  #bar;
  static {
    barGetter = instance => instance.#bar
  }
}
```

## Details of the scope and time

Private state and the class binding is visible. The code executes after the whole class has been evaluated, including decorators, and therefore the class binding is no longer in TDZ.
