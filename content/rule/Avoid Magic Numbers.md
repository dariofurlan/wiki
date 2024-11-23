---
title: Avoid Magic Numbers
tags: code-quality-principles
---
Replace [literal](gls/literal) values with named constants for clarity.

## Description

Magic numbers are [literal](gls/literal) values that are used directly in code without explanation. They are often difficult to understand and can lead to bugs when they are changed in one place but not in others. To avoid this, replace magic numbers with named constants that describe their purpose [^1].


## Examples

### Incorrect

```typescript
function calculatePrice(total) {
  if (total > 1000) {
    return total * 0.9; // 0.9 is a magic number
  } else {
    return total * 0.95; // 0.95 is another magic number
  }
}
```

### Correct

```typescript
const LARGER_DISCOUNT = 0.9;
const SMALLER_DISCOUNT = 0.95;

function calculatePrice(total) {
  if (total > 1000) {
    return total * LARGER_DISCOUNT;
  } else {
    return total * SMALLER_DISCOUNT;
  }
}
```

[^1]: https://dev.to/ruben_alapont/magic-numbers-and-magic-strings-its-time-to-talk-about-it-ci2
