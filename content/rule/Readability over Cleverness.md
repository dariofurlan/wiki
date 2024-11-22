---
title: Readability over Cleverness
tags: code-quality-principles
---
Write code that is easy to read and understand, even if it’s less “clever.”. Clever code can be difficult to understand and maintain, and can lead to bugs. Prioritize readability over cleverness.

## Bad Example

```typescript
const isPalindrome = (str: string) => str === str.split('').reverse().join('');
```

## Good Example

```typescript
const isPalindrome = (str: string) => {
  const reversed = str.split('').reverse().join('');
  return str === reversed;
};
```