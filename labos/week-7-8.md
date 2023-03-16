# Week 7

DAG studenten: Pushen naar Github VOOR vrijdag 2/4/2021 23:59\
AVOND studenten: Pushen naar Github VOOR zondag 4/4/2021 23:59

{% hint style="info" %}
Voor dit labo heb je 2 weken tijd. Indien je sneller klaar bent, gebruik die tijd om vragen te stellen over theorie of vorige labos tijdens het labo van week 8
{% endhint %}

{% hint style="info" %}
Voor studenten die graag de debugger gebruiken. Volg de uitleg op [https://code.visualstudio.com/docs/typescript/typescript-tutorial](https://code.visualstudio.com/docs/typescript/typescript-tutorial), onderdeel Debugging. Vergeet niet dat je `npx tsc --init` kan uitvoeren in de Terminal om de `tsconfig.json` file te genereren.
{% endhint %}

## Setup

Maak een folder `Labo6` in de folder die we vorige week hebben aangemaakt. Maak daar een bestand aan dat noemt `oefening1.ts`en commit/push die file, en **kijk na of je die ook op Github ziet staan!**

{% hint style="info" %}
**Belangrijk:** Na elk stukje code dat je schrijft, test je jouw code. Wanneer die werkt, commit je die code! Zo kan je altijd terugkeren naar een werkende versie, en kunnen wij ook jouw vooruitgang volgen.
{% endhint %}

{% hint style="info" %}
**Belangrijk**: We werken met **TypeScript**. Type dus ook alle variabelen en functies
{% endhint %}

{% hint style="info" %}
**Belangrijk:** Vergeet niet `tsc --init` en `npm install @types/node` te doen voor het project te initialiseren.
{% endhint %}

## Oefening 1: Spread Operator

Deze oefening maak je in bestand `oefening1.ts`.

```javascript
let numbers1: number[] = [1,2,3];
let numbers2: number[] = [4,5,6];
let numbers3: number[] = [7,8,9];
```

{% hint style="info" %}
Gebruik voor deze oefening de spread operator
{% endhint %}

Maak een variabele **allNumbers** die een array van alle getallen bevat van de bovenstaande arrays.&#x20;

Maak nu een nieuwe array **extraNumbers** die eerst de getallen van **allNumbers** bevat, en dan de getallen 10,11,12.

Maak een nieuwe array **evenMoreNumbers** die de getallen -2,-1,0 bevat, dan de getallen van **extraNumbers**, dan 13, 14, 15.

## Oefening 2: Omzetten naar hoofdletters

Deze oefening maak je in bestand `oefening2.ts`.

```javascript
let names: string[] = ['joske','franske','donald','achmed']
```

Maak een variabele **capitalNames1 en capitalNames2** die een array van alle bovenstaande namen bevat maar in hoofdletters. Gebruik hiervoor ook de functie [toUpperCase()](https://www.w3schools.com/jsref/jsref\_touppercase.asp). Doe dit op twee manieren:

* gebruik foreach
* gebruik map

## Oefening 3: map, filter, reduce, sort!

Deze oefening maak je in bestand `oefening3.ts`.

```javascript
interface Pokemon {
    name: string
    xp: number
    type: string
}

let starterPokemonGen1 : Pokemon[] = [
    {name: 'Bulbasaur', xp: 30, type: 'grass'},
    {name: 'Charmander', xp: 50, type: 'fire'},
    {name: 'Squirtle', xp: 45, type: 'water'}
];
let starterPokemonGen2 : Pokemon[]  = [
    {name: 'Chikorita', xp: 30, type: 'grass'},
    {name: 'Cyndaquil', xp: 50, type: 'fire'},
    {name: 'Totodile', xp: 45, type: 'water'}
];
```

**Opmerking**: In dit bovenstaande voorbeeld geeft xp weer hoe sterk deze pokemon is. Dit is natuurlijk in de realiteit niet het geval.

**Spread**

1. Maak een variabele **starters.** Zorg ervoor dat **** die de pokemon van beide arrays bevat. \
   _(Gebruik hiervoor de spread operator voor arrays)_
2. Gebruik **console.log** om de starters pokemon in je terminal venster te laten zien.

**Map**

1. Maak een variabele **names.** Zorg ervoor dat deze een array van de namen van de starters pokemon bevat. \
   _(Gebruik hiervoor de **map** functie voor arrays)_
2. Gebruik **console.log** om deze array van namen in je terminal venster te laten zien.

{% hint style="info" %}
Krijg je een error: "Cannot redeclare block-scoped variable 'names'.ts" dan kan je deze oplossen door `export {};`onderaan al je bestanden te zetten in die directory.
{% endhint %}

**Filter**

1. Maak een variabele **weakPokemon**. Zorg ervoor dat deze een array van de starters pokemon bevat waarvan de xp waarde kleiner is dan 40\
   _(Gebruik hiervoor de filter functie voor arrays)_
2. Gebruik **console.log** om deze array van weak pokemon in je terminal vester te laten zien.

**Combineren (Map+Filter)**

1. Maak een variabele **weakPokemonNames**. Zorg ervoor dat deze een array van namen van pokemon bevat waarvan de xp waarde kleiner is dan 40. \
   _(Je kan deze verkrijgen door eerst de filter functie te gebruiken en vervolgens de map functie te gebruiken.)_
2. Gebruik **console.log** om deze array van de namen van weak pokemon in je terminal venster te laten zien.

**Reduce**

1. Maak een variable **sumOfAllXp.** Zorg ervoor dat deze de som van de xp waarden van alle pokemon bevat.\
   _(Gebruik hiervoor de reduce functie voor arrays)_
2. Gebruik **console.log** om deze om te laten zien in je terminal venster.
3. Maak een variabele **strongestPokemon**. Zorg ervoor dat deze de pokemon bevat met de hoogste xp waarde.
4. Gebruik **console.log** om deze om te laten zien in je terminal venster.

**Combineren (Reduce + Filter** )

1. Maak een variabele **sumOfAllXpOfWeakPokemon**. **** Zorg ervoor dat deze de som van de xp waarden van alle **weakPokemon** bevat.\
   _(Je kan deze verkrijgen door eerst de filter functie te gebruiken en vervolgens de reduce functie te gebruiken)_
2. Gebruik **console.log** om deze te laten zien in je terminal venster.

**Sorteren**

1. Maak een variabele **sortedStarters**. Zorg ervoor dat deze een array bevat die pokemon bevat die gesorteerd zijn van lage xp naar hoge xp.
2. Gebruik **console.log** om deze te laten zien in je terminal venster.
3. **Extra:** Zorg ervoor dat als twee pokemon gelijke xp hebben dat deze dan alfabetisch gesorteerd worden op naam.

