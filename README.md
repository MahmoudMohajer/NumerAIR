# NumerAir

A fixed-point arithmetic library providing constrained fixed-point operations for [Stwo](https://github.com/starkware-libs/stwo.git)-based circuits.
The library implements fixed-point arithmetic using M31 field elements with configurable decimal precision.

## Usage

### Basic Arithmetic

```rust

// Create fixed-point numbers
let lhs = Fixed::from_f64(3.14);
let rhs = Fixed::from_f64(2.0);

// Basic arithmetic operations
let sum = lhs + rhs;
let diff = lhs - rhs;
let (prod, rem) = lhs * rhs;
```

### In Circuit Constraints

To use fixed-point operations in your Stwo Prover circuit, use the constraint evaluation functions:

```rust
use numerair::eval::{eval_add, eval_mul, eval_sub};

// In your circuit component's evaluate function:
fn evaluate<E: EvalAtRow>(&self, mut eval: E) -> E {
    let lhs = eval.next_trace_mask();
    let rhs = eval.next_trace_mask();
    let rem = eval.next_trace_mask();
    let res = eval.next_trace_mask();

    // Constrain mul.
    eval.eval_fixed_mul(lhs, rhs, SCALE_FACTOR.into(), res, rem)

    eval
}
```

## Contributing

Contributions are welcome! Please submit pull requests with:

- New arithmetic operations
- Improved constraints
- Additional tests
- Documentation improvements
- Performance optimizations
