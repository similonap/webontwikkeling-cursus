# Labo 3

{% hint style="info" %}
**Alle oefeningen van dit labo dienen in een folder `labo_3` te staan**
{% endhint %}

### Oefening: Timers

Maak een nieuwe folder **timers** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Een van de meest bekende functies in TypeScript die callbacks gebruiken is de `setTimeout` en de `setInterval` functie.

Je kan de documentatie van deze functies hier vinden

* [https://developer.mozilla.org/en-US/docs/Web/API/setTimeout](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout)
* [https://developer.mozilla.org/en-US/docs/Web/API/setInterval](https://developer.mozilla.org/en-US/docs/Web/API/setInterval)

#### timers\_1

Kopieer de onderstaande text in een bestand `timers_1.ts`

```
console.log('setTimeout! - 1');

const delayInMilliseconds = 1000; // this is one second

console.log('setTimeout! - 2');

const doLater = () => {
  console.log('setTimeout! - 3');
};

console.log('setTimeout! - 4');

setTimeout(doLater, delayInMilliseconds);

console.log('setTimeout! - 5');
```

Denk eens na wat de output van dit bestand zal zijn als je dit uitvoert. Schrijf het in een bestand `timers_1.txt` en vergelijk het daarna met de echte output. Zorg dat je goed begrijpt wat hier gebeurd!

#### timers\_2

Maak een nieuw bestand `timers_2.ts` en schrijf een programma dat elke seconde een getal ophoogt en vervolgens op je scherm laat zien. Gebruik hiervoor `setInterval`

Voorbeeldinteractie:

```
1
2
3
4
5
...
```

### Oefening: calculation

Maak een nieuwe folder **calculation** waarin je jouw bronbestanden voor deze oefeningen kan plaatsen. Maak een nieuw bestand `calculation.ts` aan.

Maak een functie `printCalculationResult` aan. Ze heeft 3 parameters:

* a, een getal
* b, een getal
* func, een functie van het type Calculation

```typescript
interface Calculation {(a:number, b:number):number}
```

De `printCalculationResult` functie print het resultaat van een functie van het type Calculation.

Maak 2 functies aan: een `mult` functie die a en b vermenigvuldigd, en een `add` functie die a en b optelt. Deze functies zijn van het type Calculation.

Zorg dat volgende code werkt:

```typescript
printCalculationResult(2,4,add); //print 6
printCalculationResult(2,4,mult); // print 8
```

### Oefening: robotFactory

Maak een nieuwe folder **robotFactory** waarin je jouw bron bestanden voor deze oefening kan plaatsen.

{% hint style="info" %}
Installeer chalk met `npm install chalk@4` anders zal deze NIET werken.
{% endhint %}

Maak een nieuw bestand `robotFactory.ts` met de volgende inhoud:

```
const chalk = require("chalk");

interface CreateFunction {
    (name: string): void
}

const createRobotFactory = (color: string) : CreateFunction => {
    
}
```

Vul nu de functie **createRobotFactory** aan zodat deze een functie teruggeeft die voldoet aan de `CreateFunction` interface. Deze functie zal

```
Robot <name> ready for duty!
```

op het scherm laten zien als deze wordt aangeroepen. Hij zal dit doen aan de hand van de kleur die meegegeven wordt aan de **createRobotFactory** functie.

**Voorbeeld:**

```
let createYellow = createRobotFactory("yellow");
createYellow("Roby");
createYellow("Eve");

let createRed = createRobotFactory("red")
createRed("Botty");
createRed("Megatron");
```

![](<../../.gitbook/assets/Screenshot 2022-03-02 at 20.54.32.png>)

{% hint style="info" %}
chalk\[color]\("Hello World") geeft de tekst HelloWorld in de kleur weer die in de variabele color is gedefinieerd.
{% endhint %}

### Oefening: atLeastTwo

Maak een nieuwe folder **atLeastTwo** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Maak een nieuw bestand `atLeastTwo.ts` met de volgende inhoud.

```
interface TestFunction {
    (n: number): boolean
}
```

* Schrijf een arrow functie `isOdd` die deze interface implementeert die teruggeeft of een getal oneven is.
* Schrijf een arrow functie `isEven` die deze interface implementeert die teruggeeft of een getal even is.
* Verzin twee andere functie's die deze interface implementeert.
* Schrijf een arrow functie genaamd `atLeastTwo` die twee argumenten aanvaard. Het eerste argument is een array van getallen en de tweede argument is een functie van het type `TestFunction`
* Deze functie geeft true terug als minstens twee elementen voldoen aan de meegegeven functie.

Bijvoorbeeld:

```
console.log(atLeastTwo([2,3,4,6,8], isOdd));
console.log(atLeastTwo([2,3,4,5,6,8], isOdd));
```

geeft de volgende output:

```
false
true
```

### Oefening: printHandler

Maak een nieuwe folder **printHandler** waarin je jouw bronbestanden voor deze oefening kan plaatsen. We gaan gebruik maken van de `chalk` library om gekleurde tekst te laten zien op het scherm (vergeet dus niet deze te installeren met npm install)

Maak een nieuw bestand `printHandler.ts` met de volgende inhoud.

```
interface PrintHandler {
    (str: string): void
}
```

* Schrijf een arrow functie `printBlue` die deze interface implementeert en de meegegeven tekst afprint in het blauw
* Schrijf een arrow functie `printRed` die deze interface implementeert en de meegegeven tekst afprint in het rood
* Schrijf een arrow functie `printDouble` die deze interface implementeert en die elk karakter van een meegegeven string dubbel afprint
  * TEST wordt TTEESSTT, WEB wordt WWEEBB,...
* Verzin nog een functie die iets met tekst doet en deze interface implementeert (niets met kleuren!)
* Schrijf een arrow functie `sum` met als argumenten twee getallen a,b en een functie van het type `PrintHandler`
* Deze functie maakt een som van a en b en gebruikt de printHandler om deze af te printen.
* Probeer deze functie uit.

Bijvoorbeeld:

```
sum(1,5, printBlue);
sum(1,5, printRed);
sum(1,5, printDouble);
```

geeft de volgende output:

![](<../../.gitbook/assets/Screenshot 2022-03-02 at 10.54.38.png>)

### groupBy

Maak een nieuwe folder **groupBy** en maak een groupBy.ts bestand aan met de volgende inhoud

```
interface Person {
  name: string;
  yearOfBirth: number;
  placeOfBirth: string;
}

const input: Person[] = [
  {
    name: "Andie",
    yearOfBirth: 1984,
    placeOfBirth: "Mortsel",
  },
  {
    name: "Joachim",
    yearOfBirth: 1995,
    placeOfBirth: "Mortsel",
  },
  {
    name: "Bert",
    yearOfBirth: 1995,
    placeOfBirth: "Edegem",
  },
  {
    name: "Timo",
    yearOfBirth: 2005,
    placeOfBirth: "Antwerpen",
  },
];
```

Schrijf nu een functie `groupBy` die de personen groepeert gebruik makende van een meegegeven functie.

**Voorbeeld interactie:**

```
console.log(groupBy(input, (p: Person) => p.placeOfBirth));
{
  Mortsel: [
    { name: 'Andie', yearOfBirth: 1984, placeOfBirth: 'Mortsel' },
    { name: 'Joachim', yearOfBirth: 1995, placeOfBirth: 'Mortsel' }
  ],
  Edegem: [ { name: 'Bert', yearOfBirth: 1995, placeOfBirth: 'Edegem' } ],
  Antwerpen: [ { name: 'Timo', yearOfBirth: 2005, placeOfBirth: 'Antwerpen' } ]
}

console.log(groupBy(input, (p: Person) => p.yearOfBirth));
{
  '1984': [ { name: 'Andie', yearOfBirth: 1984, placeOfBirth: 'Mortsel' } ],
  '1995': [
    { name: 'Joachim', yearOfBirth: 1995, placeOfBirth: 'Mortsel' },
    { name: 'Bert', yearOfBirth: 1995, placeOfBirth: 'Edegem' }
  ],
  '2005': [ { name: 'Timo', yearOfBirth: 2005, placeOfBirth: 'Antwerpen' } ]
}
```

Gebruik nu de groupBy functie dat je ook deze gegevens groepeert aan de hand van hun leeftijdsklasse. Bv: \[10-20], \[20-30],....

```
{
  '[30-40]': [ { name: 'Andie', yearOfBirth: 1984, placeOfBirth: 'Mortsel' } ],
  '[20-30]': [
    { name: 'Joachim', yearOfBirth: 1995, placeOfBirth: 'Mortsel' },
    { name: 'Bert', yearOfBirth: 1995, placeOfBirth: 'Edegem' }
  ],
  '[10-20]': [ { name: 'Timo', yearOfBirth: 2005, placeOfBirth: 'Antwerpen' } ]
}
```
