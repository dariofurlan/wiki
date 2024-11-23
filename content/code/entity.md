---
title: Entity
---

La "logica di dominio" in ambito Domain-Driven Design (DDD) si riferisce alla parte del software che gestisce e implementa le regole, le politiche e le operazioni specifiche di un determinato dominio o settore di applicazione.

## Identifier

Ogni Entità è definita da un identificatore univoco chiamato [Identifier](code/identifier)

## Entità

```typescript
interface IEntity<I extends IIdentifier<any>> {
	_id: I;
	equals(entity: IEntity<I>): boolean;
	
	isNew: boolean;
	isDeleted: boolean;
}
```

Quando si definisce una entità è importante stare attenti ai setter che si espongono.

### Costruttore
Il costruttore sarà privato faremo uso del [[Structural Patterns#Factory Method]]

### Metodo Statico Create
Ogni entità dovrà predisporre un metodo statico create.
Il metodo create rappresenta la creazione di una nuova entità in ottica di business.
Se creo una entità potrei non aver bisogno di tutte le proprietà.

Sarà la logica di business che determina quali proprietà è essenziale inizializzare manualmente quali automaticamente e in caso di inizializzazione automatica, a che valore vengono definiti di default.

Buona prassi è tenere il meno possibi

```typescript
class Esempio implements IEntity<I> {
	//...
	
	public static create(props: { /* ... */ }, _id: I): Esempio {
		return new Esempio() {
			
		}
	}
}
```

## Rules

### Getter per ogni proprietà
E' generalmente buona prassi creare un getter per ogni proprietà specilamente per 
### Non servono setter per ogni cosa
Applicare sempre il [Principio YAGNI](Principles#YAGNI).
Ci serve modificare una proprietà **ORA** ?  No -> al 99% non ci servirà mai
### Non usare setter standard
Usare setter come funzione

CORRETTO
```typescript
class Esempio implements IEntity<I> {
	//...
	
	setProperty(val: string) { 
		this.val = val 
	} 

	//...
}
```

SBAGLIATO
```typescript
class Esempio implements IEntity<I> {
	//...
	
	set property(val: string) { 
		this.val = val 
	} 

	//...
}
```
