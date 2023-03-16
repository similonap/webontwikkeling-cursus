# Week 6

DAG studenten: Pushen naar Github VOOR vrijdag 19/3/2021 23:59\
AVOND studenten: Pushen naar Github VOOR zondag 21/3/2021 23:59

## Setup

Maak een folder `Labo5` in de folder die we vorige week hebben aangemaakt. Maak daar een bestand aan dat noemt `oefening1.ts`en commit/push die file, en **kijk na of je die ook op Github ziet staan!**

{% hint style="info" %}
**Belangrijk:** Na elk stukje code dat je schrijft, test je jouw code. Wanneer die werkt, commit je die code! Zo kan je altijd terugkeren naar een werkende versie, en kunnen wij ook jouw vooruitgang volgen.
{% endhint %}

{% hint style="info" %}
**Belangrijk**: We werken met **TypeScript**. Type dus ook alle variabelen en functies
{% endhint %}

## Oefening 1: arrow notatie

Deze oefening maak je in bestand `oefening1.ts`.

Schrijf de volgende functies in de kortst mogelijke arrow notaties:

```typescript
const printStuff = (amount: number, text: string):void => {
    console.log(`Hello ${text}, you are number ${amount}`);
}
const twoDArray = (element1: string, element2: string): string[] => {
    return [element1, element2];
}
const numberToString = (number: number): string => {
    return `${number}`;
}
```

## Oefening 2: functie als parameter

Deze oefening maak je in bestand `oefening2.ts`.

Maak een functie `sum` die alle getallen van een array optelt. Als de functie klaar is, gebruikt ie de onderstaande functie om het resultaat op de console te printen:

```typescript
const printToConsole = (number : number) : void => console.log(`the result is ${number}`); 
```

{% hint style="danger" %}
Je moet printToConsole als parameter meegeven aan jouw eigen functie!
{% endhint %}

Pas nu jouw functie aan zodat je 2 functies als parameters kan meegeven. Wanneer het resulterende getal groter is dan 10, roep je `printToConsole` aan zoals hierboven. Wanneer het kleiner is dan 10, roep je onderstaande anonieme functie op (zonder deze aan een variable toe te wijzen):

```typescript
number => console.log(`the result ${number} is a very small number`)
```

{% hint style="info" %}
Je kan een functie definieren rechstreeks in de call van een andere functie (zie theorie!)
{% endhint %}

## Oefening 3: interfaces

Deze oefening maak je in bestand `oefening3.ts`.

Maak een functie `printCalculationResult` aan. Deze functie print het resultaat van een functie van het type Calculation. Ze heeft 3 parameters:

* a, een getal
* b, een getal
* func, een functie van het type Calculation

```typescript
interface Calculation {(a:number, b:number):number}
```

Maak 2 functies aan: een `mult` functie die a en b vermenigvuldigd, en een `add` functie die a en b optelt.

Zorg dat volgende code werkt:

```typescript
printCalculationResult(2,4,add); //print 6
printCalculationResult(2,4,mult); // print 8
```

## Oefening 4: functie als returnwaarde

Deze oefening maak je in bestand `oefening4.ts`.

Schrijf hier een functie genaamd `calculateDogAge`die:

* 1 argument heeft: de leeftijd van je hond
* de leeftijd van je hond berekent: 1 mensenjaar is 7 hondenjaren
* die deze leeftijd terug geeft als return waarde

```typescript
calculateDogAge(3); //  21 
```

Maak een nieuwe functie `calculateAnimalAge` die naast de leeftijd ook een 2de argument mee aanvaard dat de omzettingsverhouding uitdrukt. Om de functie dan aan te roepen voor een hond van 2 jaar doe je `calculateAnimalAge(2, 7)`

{% hint style="danger" %}
Zorg ervoor dat  calculateDogAge deze functie aanroept zodat je niet twee keer dezelfde code hebt staan
{% endhint %}

Maak een nieuwe functie `calculateAnimalAgeFunctional` die&#x20;

* 1 argument heeft: de omzettingsverhouding
* als return waarde de functie `(age) => { return calculateAnimalAge(age, omzettingsverhouding); }` \
  teruggeeft.
* Gebruik deze variabele om de functie `calculateHamsterAge` te definiëren en gebruik deze om de leeftijd van een hamster van een half jaar te berekenen

```typescript
const calculateHamsterAge = calculateAnimalAgeFunctional(26);
console.log(calculateHamsterAge(.5));
```
