---
title: Avoid Magic Strings
tags: code-quality-principles
---
Replace literal values with named constants for clarity.

## Description

Magic strings are literal values that are used directly in code without explanation. They are often difficult to understand and can lead to bugs when they are changed in one place but not in others. To avoid this, replace magic strings with named constants that describe their purpose [^1].

## Examples

### Incorrect

```typescript
function getErrorMessage(code) {
  switch (code) {
    case "ERR001":
      return "Connection Error"; // "ERR001" is a magic string
    case "ERR002":
      return "Authentication Error"; // "ERR002" is another magic string
    default:
      return "Unknown Error";
  }
}
```

### Correct

```typescript
const CONNECTION_ERROR_CODE = "ERR001";
const AUTHENTICATION_ERROR_CODE = "ERR002";

function getErrorMessage(code) {
  switch (code) {
    case CONNECTION_ERROR_CODE:
      return "Connection Error";
    case AUTHENTICATION_ERROR_CODE:
      return "Authentication Error";
    default:
      return "Unknown Error";
  }
}
```

[^1]: https://dev.to/ruben_alapont/magic-numbers-and-magic-strings-its-time-to-talk-about-it-ci2