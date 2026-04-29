# js-lite

[![no_std](https://img.shields.io/badge/no__std-compatible-green.svg)](https://rust-embedded.github.io/book/)
[![License: MIT OR Apache-2.0](https://img.shields.io/badge/license-MIT%2FApache--2.0-blue.svg)](LICENSE-MIT)

A minimal `no_std` JavaScript interpreter written in Rust. Supports variables, functions, objects, arrays, control flow, try/catch, and built-in functions needed for Cloudflare challenge solving.

This is **not** a spec-compliant JavaScript engine. It is "JavaScript-shaped" enough that real-world challenge scripts (math, string manipulation, cookie setting) run correctly. Originally built for [ClaudioOS](https://github.com/suhteevah/claudio-os), a bare-metal Rust OS that runs AI coding agents.

## Features

**Language**
- Variable declarations: `var`, `let`, `const`
- Functions: declarations, expressions, arrow functions, closures
- Control flow: `if`/`else`, `for`, `while`, `do-while`, `switch`/`case`, `for-in`, `for-of`
- Error handling: `try`/`catch`/`finally`, `throw`
- Objects and arrays with property access (dot and bracket notation)
- Template literals with `${expr}` interpolation
- Ternary operator, nullish coalescing (`??`), optional chaining (`?.`)
- All bitwise and logical operators
- `typeof`, `instanceof`, `delete`, `void`
- Spread syntax (`...`)
- Regex literals with `.test()` and basic pattern matching
- Dynamic code evaluation

**Built-in Globals**
- `Math` (floor, ceil, round, abs, min, max, pow, sqrt, log, sin, cos, tan, random, PI, E, ...)
- `JSON` (stringify, parse)
- `Object` (keys, values, entries, assign, freeze)
- `Array` (isArray, from)
- `String` (fromCharCode)
- `Number` (isInteger, isFinite, isNaN, parseInt)
- `Date` (now stub)
- `console` (log, info, warn, error, debug)
- `document` (cookie get/set, createElement, getElementById stubs)
- `navigator`, `location`, `screen`, `window`

**Built-in Functions**
- `parseInt`, `parseFloat`, `isNaN`, `isFinite`
- `encodeURIComponent`, `decodeURIComponent`, `encodeURI`, `decodeURI`
- `btoa`, `atob` (base64)
- `setTimeout`, `setInterval` (run callback immediately)
- `escape`, `unescape`
- `Number()`, `String()`, `Boolean()`, `Array()`, `Object()`, `RegExp()`

**String Methods**: charAt, charCodeAt, indexOf, lastIndexOf, includes, startsWith, endsWith, slice, substring, substr, split, replace, trim, trimStart, trimEnd, toUpperCase, toLowerCase, repeat, padStart, padEnd, match, search, concat

**Array Methods**: push, pop, shift, unshift, join, indexOf, includes, slice, splice, concat, reverse, sort, map, filter, reduce, forEach, find, findIndex, some, every, fill, flat, flatMap

**Number Methods**: toString(radix), toFixed

## Usage

Add to your `Cargo.toml`:

```toml
[dependencies]
js-lite = "0.1"
```

For `no_std` environments:

```toml
[dependencies]
js-lite = { version = "0.1", default-features = false }
```

### Basic evaluation

```rust
use js_lite::execute;

let output = execute("
    var x = 2 + 3;
    console.log('result: ' + x);
").unwrap();
assert_eq!(output.trim(), "result: 5");
```

### Cookie extraction (Cloudflare challenges)

```rust
use js_lite::execute_for_cookie;

let cookie = execute_for_cookie("
    var value = Math.floor(47 * 31 + 16);
    document.cookie = 'cf_clearance=' + value + '; path=/';
").unwrap();
// cookie == "cf_clearance=1473"
```

### Full browser context

```rust
use js_lite::execute_with_context;

let (output, cookie) = execute_with_context(
    "document.cookie = 'session=abc; path=/';",
    "existing=value",       // initial cookie
    "example.com",          // hostname
    "/page",                // path
).unwrap();
```

### Direct interpreter access

```rust
use js_lite::{Interpreter, Value};
use js_lite::tokenizer::tokenize;
use js_lite::parser::parse;

let tokens = tokenize("var x = 42;").unwrap();
let ast = parse(tokens).unwrap();

let mut interp = Interpreter::new();
let _ = interp.exec_block(&ast);

// Read variables, set globals, etc.
```

## Safety and Limits

- Maximum call depth: 256 (stack overflow protection)
- Maximum loop iterations: 1,000,000 (infinite loop protection)
- No file system or network access
- No unsafe code in the interpreter itself

## License

Licensed under either of

- [Apache License, Version 2.0](LICENSE-APACHE)
- [MIT License](LICENSE-MIT)

at your option.

## Contributing

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

---

## Support This Project

If you find this project useful, consider buying me a coffee! Your support helps me keep building and sharing open-source tools.

[![Donate via PayPal](https://img.shields.io/badge/Donate-PayPal-blue.svg?logo=paypal)](https://www.paypal.me/baal_hosting)

**PayPal:** [baal_hosting@live.com](https://paypal.me/baal_hosting)

Every donation, no matter how small, is greatly appreciated and motivates continued development. Thank you!
