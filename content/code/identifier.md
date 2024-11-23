---
title: identifier
---



```typescript
interface IIdentifier<T> {
	equals(id: IIdentifier<T>): boolean;
	readonly value: T;
	toString(): string;
}
```