# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2026-04-02

### Added

- Initial release extracted from the ClaudioOS bare-metal operating system
- Tokenizer with support for all JS operators, string/template literals, regex, hex/binary numbers
- Recursive descent parser producing a full AST
- Tree-walking interpreter with:
  - Variable declarations (var, let, const)
  - Functions (declarations, expressions, arrows, closures)
  - Control flow (if/else, for, while, do-while, switch, for-in, for-of)
  - Error handling (try/catch/finally, throw)
  - Objects and arrays with method calls
  - Template literals with interpolation
  - Ternary operator, nullish coalescing, optional chaining
  - All bitwise operators
  - typeof, instanceof, delete, void
  - Spread syntax
- Built-in globals: Math, JSON, console, document, navigator, location, screen
- Built-in functions: parseInt, parseFloat, encodeURIComponent, decodeURIComponent, btoa, atob, eval, setTimeout/setInterval (immediate execution stubs)
- String methods: charAt, charCodeAt, indexOf, lastIndexOf, includes, startsWith, endsWith, slice, substring, substr, split, replace, trim, toUpperCase, toLowerCase, repeat, padStart, padEnd, match, search
- Array methods: push, pop, shift, unshift, join, indexOf, includes, slice, splice, concat, reverse, sort, map, filter, reduce, forEach, find, findIndex, some, every, fill, flat, flatMap
- Number methods: toString(radix), toFixed
- Regex test and exec (basic pattern matching, no full regex engine)
- document.cookie get/set with Cloudflare challenge solving support
- no_std compatible with alloc
- 29 tests covering all major features
