---
title: React Context Guide
---

# Introduzione al Context di React

Il [Context](glossary/React%20Context.md) di React è uno strumento potente che permette di passare dati attraverso l'albero dei componenti senza dover passare esplicitamente le props a ogni livello. È utile per condividere dati che sono considerati "globali" per un albero di componenti, come l'utente autenticato, il tema o la lingua preferita.

## Creare un Context

Per creare un Context, utilizziamo la funzione `createContext` di React. Ecco un esempio di come creare un Context per un tema:

```jsx
import React, { createContext } from 'react';

const ThemeContext = createContext('light');
```

## Fornire un Context

Per fornire un valore di Context ai componenti figli, utilizziamo il componente `Provider` del Context. Ecco un esempio:

```jsx
import React from 'react';
import { ThemeContext } from './ThemeContext';

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Toolbar />
    </ThemeContext.Provider>
  );
}
```

## Consumare un Context

Per consumare un valore di Context in un componente, utilizziamo il hook `useContext` o il componente `Consumer`. Ecco un esempio con `useContext`:

```jsx
import React, { useContext } from 'react';
import { ThemeContext } from './ThemeContext';

function Toolbar() {
  const theme = useContext(ThemeContext);
  return <div style={{ background: theme === 'dark' ? '#333' : '#fff' }}>Toolbar</div>;
}
```

## Conclusione

Il Context di React è uno strumento utile per gestire dati globali in un'applicazione React. Utilizzando `createContext`, `Provider` e `useContext`, possiamo facilmente condividere e consumare dati attraverso l'albero dei componenti senza dover passare props manualmente a ogni livello.

Per ulteriori informazioni, consulta la [documentazione ufficiale di React](https://react.dev/learn/passing-props-to-a-component).
