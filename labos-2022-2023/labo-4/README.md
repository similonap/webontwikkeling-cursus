# Labo 4

### Oefening: slowSum

Maak een nieuwe folder **slowSum** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Plaats de onderstaande code in een bestand `slowSum.ts`&#x20;

```typescript
const slowSum = (a: number, b: number) => {
    return new Promise<number>((resolve, reject) => {
        setTimeout(() => {
            resolve(a+b);
        },1000)
    });
}

const slowMult = (a: number, b: number) => {
    return new Promise<number>((resolve, reject) => {
        setTimeout(() => {
            resolve(a*b);
        },1500)
    });
}
```

Dit zijn 2 functies die een promise terug geven. Ze simuleren een trage som functie en een trage vermenigvuldigings functie.

1. Roep de `slowSum` functie aan met de getallen 1 en 5 en zorg dat ze het resultaat van deze functie op het scherm laat zien. (zie output)
2. Roep de `slowSum` functie opnieuw aan met de getallen 1 en 5 maar zorg deze keer dat na het optellen de vermenigvuldigings functie \``slowMult` wordt aangeroepen dat het resultaat vermenigvuldigd met 2 en dan op het scherm laat zien. (zie output)
3. Maak een eigen `slowDiv` functie dat een deling doet (laat deze 2000 milliseconden duren). Zorg ervoor dat als je een deling door nul doet dat je de promise afkeurt met de melding "You cannot divide by zero".
4. Roep deze functie aan met de getallen 6 en 3 en laat het resultaat op het scherm zien. (zie output)
5. Roep deze functie aan met de getallen 6 en 0 en laat de error op het scherm zien. (zie output)

**Verwachte output:**

```
➜  ts-node oefening1.ts
You cannot divide by zero
1 + 5 = 6
(6 / 3) = 2
(1 + 5) * 2 = 12
```

{% hint style="info" %}
Gebruik .then(...) om iets uit te voeren nadat de promise klaar is.
{% endhint %}

#### Uitbreiding:

Maak een kopie van het `slowSum.ts` oefening en noem deze `slowSum_async.ts`&#x20;

Gebruik nu **async/await** in plaats van promises.

### Oefening: fakeFetch

Maak een nieuwe folder **fakeFetch** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Plaats de onderstaande code in `fakeFetch.ts` en voer deze code uit. Zorg er zeker voor dat je deze code begrijpt!

Maak een nieuw bestand `fakeFetch_promises.ts` en vorm de code om zodat het gebruik maakt van promises.

```
interface Callback {
    (n: number): void
}

const getRandom = (callback: Callback) => {
    setTimeout(() => {
        callback(Math.floor(Math.random() * 100))
    },1000);
}

getRandom((n) => {
    console.log(`The number was ${n}`);
});
```

#### **Uitbreiding:**

Maak een kopie van het `fakeFetch.ts` oefening en noem deze `fakeFetch_async.ts`

Gebruik nu **async/await** in plaats van promises.

### **Oefening: Bitcoin**

Maak een nieuwe folder **bitcoin** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Deze oefening maak je in bestand `bitcoin.ts`.&#x20;

Je mag voor deze oefening gebruik maken van `node-fetch` of van `axios` (Vergeet deze niet te installeren met npm)

{% hint style="info" %}
Indien je node-fetch gebruikt installeer dan versie 2 (npm install node-fetch@2)
{% endhint %}

Gebruik de bitcoin api van coinbase om de prijs van bitcoin in euro op te vragen

{% embed url="https://api.coindesk.com/v1/bpi/currentprice.json" %}

Gebruik hiervoor **promises** en **GEEN** **async/await**

### **Oefening: All**

Na hoeveel tijd zal deze code "done!" op het scherm tonen? Voer de code dus niet uit maar denk even zelf na.

```
const delay = (delay: number): Promise<void> => {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve();
        }, delay);
    });
}

(async() => {
    await Promise.all([delay(1000), delay(10000), delay(15000)])
    console.log("Done!");
})();
```

### **Oefening: Cocktails**

Maak een nieuwe folder **cocktails** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Deze oefening maak je in bestand `cocktails.ts`.&#x20;

Je mag voor deze oefening gebruik maken van `node-fetch` of van `axios` (Vergeet deze niet te installeren met npm)

{% hint style="info" %}
Indien je node-fetch gebruikt installeer dan versie 2 (npm install node-fetch@2)
{% endhint %}

Maak gebruik van `Promise.all` om de drie volgende cocktails via de cocktail api met de volgende ids in te lezen: **11000**, **11001**, **11002** en vervolgens de naam van de drie cocktails op het scherm te laten zien.

Je kan een cocktail via een id via de volgende api call binnenhalen:

```
https://www.thecocktaildb.com/api/json/v1/1/lookup.php?i=11000
```

**Verwachte output:**

```
Mojito
Old Fashioned
Long Island Tea
```

{% hint style="info" %}
Je mag hier met het type any werken.&#x20;
{% endhint %}

### PRO Oefening: promisify

`fs.readFile` maakt gebruik van callbacks. Hier onder heb je een voorbeeld:

```
const fs = require("fs");

fs.readFile("./file.txt", "utf8", (err: Error, data: string) => {
    console.log(data);
});
```

Maak een functie `readFilePromise` die een promise teruggeeft.  Deze functie heeft de volgende interface:

```
interface ReadFilePromise {
    (fileName: string): Promise<string>
}
```

Zorg er nu voor dat je met deze functie een file kan inlezen gebruikmakende van promises en dus niet de callback. Dit proces heet 'promisification'&#x20;

**Extra:**

Zoek op het internet op hoe je `util.promisify` kan gebruiken om dit zonder een eigen functie te schrijven kan doen.
