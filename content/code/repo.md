---
title: Repository
aliases:
  - repo
---

> [!INFO]
> A repo defines all the database actions you can perform on a specific data model.

## Importanza della Session
Passare ad ogni query la session di mongodb ci permette di associare queste operazioni all'interno della stessa transazione.
Se non si dovesse passare le operazioni non verrà garantita atomicità, consistenza, e soprattuto isolazione.
Vedere [[Principles#ACID]]

## Metodo Save

All'interno del metodo save verrà gestita l'applicazione nel database di modifiche all'entità.
Se invochiamo il metodo save è perché l'Entità è stata:
- creata
- eliminata
- altrimenti modificata

Da notare che diamo per scontato che se non è stata ne creata ne eliminata conterrà sempre delle modifiche.

```typescript
class ExampleRepo implements IRepo<> {
	/* ... */

	async save(example: Example): Promise<void> {
		const rawObj = ExampleMapper.toDTO(example);

		if (example.isNew) {
			this.ExampleModel.save(rawObj);
		} else if (example.isDeleted) {
			this.ExampleModel.deleteOne(rawObj._id);
		} else {
			this.ExampleModel.updateOne(rawObj._id, rawObj);
		}
	}
}
```

### Upsert
Se il database sottostante supporta l'operazione di upsert è possibile semplificare ulteriormente il metodo save.
Upsert è la fusione di insert e update, infatti se l'entità non esiste verrà creata, altrimenti verrà aggiornata.

```typescript
class ExampleRepo implements IRepo<> {
	/* ... */

	async save(example: Example): Promise<void> {
		const rawObj = ExampleMapper.toPersistence(example);

		if (example.isDeleted) {
			this.ExampleModel.deleteOne(rawObj._id);
		} else {
			this.ExampleModel.updateOne(rawObj._id, rawObj, { upsert: true });
		}
	}
}
