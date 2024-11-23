---
title: Database Context
---

Il database context è un'interfaccia che rappresenta un'unità di lavoro. Implementa il pattern Unit of Work e permette di eseguire operazioni di lettura e scrittura sul database.

## Database Context

```typescript
interface IDatabaseContext {
    readonly session: ClientSession | undefined;
    readonly sessionOrNull: ClientSession | null;

    runWithTransaction<T>(fn: () => Promise<T>): Promise<T>;
}
```

### ``session``
Il campo `session` rappresenta la sessione corrente. Se non è presente nessuna sessione, il campo sarà `undefined`.
Questo dovrà sempre essere utilizzato quando facciamo qualsiasi operazione sul database, quindi all'interno della [repository](code/repo).
