## React context

Ve složitějších aplikacích potkáme situace, kdy potřebujeme povýšit stav opravdu vysoko, někdy až do kořene samotné aplikace. Pokud je strom komponent hluboký, snadno se nám stane, že budeme vysoce povýšený stav předávat pomocí props skrze mnoho úrovmí. Této sitauci se v React terminologii říká **props drilling**. Pokud je situace už neúnosná, můžeme se props drillingu vyhnout použitím React contextu.

Pomocí React contextu můžeme zařídit, že nějaká část naší aplikace má přistup k určitým hodnotám bez nutnosti předávat je pomocí props. Typickým příkladem je napříkad informace o přihlášeném uživateli. Mnoho komponent na různých místech v aplikaci potřebuje informaci o tom, zde je přihlášený nějaký uživatel. Provrtávat props o uživateli do všech těchto komponent by byla ohromná a nevděčná práce.

Představme si, že máme v naší aplikaci nastavení, která mají být dostupná v celé aplikaci. Může jít například o nastavení měny nebo světlého/tmavého tématu. V naší aplikaci budeme chtít mít dostupný takovýto objekt:

```tsx
{
  currency: 'CZK',
  theme: 'light',
}
```

Za tímto účelem vytvoříme React context s názvem `SettingsContext`. Pro context vytvoříme separátní soubor `settings-context.tsx`.

```js
import { createContext } from 'react';

export const SettingsContext = createContext();
```

Nyní je potřeba tu část aplikace, kde chceme náš context používat, obalit speciální komponentou zvanou **context provider**. My chceme context používat v celé aplikaci, dáme tedy provider rovnou do kořene celé naší aplikace a zabalíme do něho všechno.

```jsx
import { SettingsContext } from './settings-context';

const App = () => {
  return (
    <SettingsContext.Provider value={{ currency: 'CZK' }}>

      <div className="container">
        <Header />
        <Banner />
        <Cart />
      </div>

    </SettingsContext.Provider>
  );
};
```

V každé komponentě, která se nachází ve stromě komponent uvnitř context provideru, pak máme přístup k hodnotě předané pomocí prop `value`. Použijeme k tomu hook `useContext`.

```jsx
import { SettingsContext } from "../../settings-context";

const Product = ({ name, price }) => {
  const { currency } = useContext(SettingsContext);

  return (
    <div className="product">
      <span>{name}</span>
      <span>{price} {currency}</span>
    </div>
  )
};
```

### Vlastní hook

Je zvykem pro použití contextu vytvářit vlastní hook, který má přiléhavější název a zlepšuje čitelnost kódu.

```js
import { createContext, useContext } from 'react';

export const SettingsContext = createContext();

export const useSettings = () => useContext(SettingsContext);
```

Pak nám stačí v komopnentě `Product` psát jednodušeji:

```jsx
import { useSettings } from "../../settings-context";

const Product = ({ name, price }) => {
  const { currency } = useSettings();

  return (
    <div className="product">
      <span>{name}</span>
      <span>{price} {currency}</span>
    </div>
  )
};
```


---

Pokračuj samostatně na → [Cvičení na předávání na context](cviceni-ukolnicek-context.md)