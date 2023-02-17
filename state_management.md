### Signal
```rust
let state = create_signal(cx, 0);
state.get(); // 0
state.set(1);
state.updt(|prev| prev + 1)
// or
state.put(|prev| prev + 1)
// TODO: patch
```

### Effect
```rust
let state = create_signal(cx, 0);
create_effect(cx, || println!("The state changed. New value: {}", state.get()));
// Prints "The state changed. New value: 0"
// (note that the effect is always executed at least 1 regardless of state changes)

state.set(1); // Prints "The state changed. New value: 1"
state.set(2); // Prints "The state changed. New value: 2"
state.set(3); // Prints "The state changed. New value: 3"
```

### Memos
```rust
let state = create_signal(cx, 0);
let double = create_memo(cx, || *state.get() * 2);

assert_eq!(*double.get(), 0);
state.set(1);
assert_eq!(*double.get(), 2);
```
