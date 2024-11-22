---
title: Enum
aliases:
  - dizionario
---

## Dettagli
Sono degli object javascript 

Definiamo quello che si chiama un "literal", ossia una stringa che può assumere valori ben definiti come in questo caso:
```typescript
type Food = "Carrot" | "Steak" | "Orange";
```

Il dizionario va creato indicando specificando innanzitutto il tipo in questa maniera:
```typescript
const FoodDict: { [key in Food]: key } = {};
```
Letteralmente sta a significare che il dizionario (`FoodDict`) sarà un oggetto (`{ ... }`) che possiede una chiave (`key`) per ogni valore all'interno di Food (`[key in Food]`)  dove il **valore** assegnato ad ogni **chiave** sarà identico alla chiave stessa (`[key in Food]: key`). 

Il nostro IDE ci obbligherà ora a completare l'oggetto esattamente in questa maniera:
```typescript
const FoodDict: { [key in Food]: key } = {
	Carrot: "Carrot",
	Steak: "Steak",
	Orange: "Orange"
};
```

Così facendo avremo un oggetto javascript iterabile che rappresenta tutti i valori ammissibili di Food.

### Utilizzare un Dict
#### Accedere ad un valore
L'utilizzo più frequente e il più semplice.
è un normalissimo accesso ad una proprietà di un oggetto.
Si è addirittura aiutati dall' IDE stesso che ci indica il contenuto del dizionario.
```typescript
const favourite_food = FoodDict.Carrot
```
#### Ottenere l'elenco dei valori
Il primo metodo è preferito in quanto viene meglio gestito da typescript e dal nostro IDE
```typescript
const FoodList = Object.values(FoodDict); // [ "Carrot", "Steak", "Orange" ]
```
Il secondo metodo è tecnicamente equivalente e da lo stesso risultato perché le chiavi sono uguali ai valori,  ma typescript non è molto d'accordo con noi.
Meglio evitarlo, ma è il seguente
```typescript
const FoodList = Object.keys(FoodDict); // [ "Carrot", "Steak", "Orange" ]
```
#### Verificare se un valore appartiene al dizionario
Facciamo uso di [Type Predicates](https://www.typescriptlang.org/docs/handbook/2/narrowing.html?#using-type-predicates)

è possibile definire una funzione che ci aiuta a capire se una variabile di tipo sconosciuto rientra all'interno dei valori consentiti dal dizionario.

Nel nostro esempio equivale a dire se una stringa è uno dei valori di `Food` 
```typescript
function isFood(val: string): val is Food {
	return val in FoodDict;
}
```
Questa funzione non ci ritorna solo un boolean, ma fa molto di più!
Infatti nel caso ritornasse true, da quel momento in poi il nostro IDE tratta il valore come Food.
```typescript
const maybeFood: string = "Nails";

if (isFood(maybeFood)) {
	// maybeFood is of type Food now
	console.log("Yummii 😋, I'm eating " + food);
} else {
	// maybeFood is definitely NOT of type Food
	console.log("Oouuuchh!!");
}
```