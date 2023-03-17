# Week 4

DAG studenten: Pushen naar Github VOOR vrijdag 5/3/2021 23:59\
AVOND studenten: Pushen naar Github VOOR zondag 7/3/2021 23:59

## Setup

Maak een folder `Labo3` in de folder die we vorige week hebben aangemaakt. Maak daar een bestand aan dat noemt `oefening1.ts`en commit/push die file, en **kijk na of je die ook op Github ziet staan!**

{% hint style="info" %}
**Belangrijk:** Na elk stukje code dat je schrijft, test je jouw code. Wanneer die werkt, commit je die code! Zo kan je altijd terugkeren naar een werkende versie, en kunnen wij ook jouw vooruitgang volgen.
{% endhint %}

{% hint style="info" %}
**Belangrijk**: We werken met **TypeScript**. Type dus ook alle variabelen en functies!
{% endhint %}

### Oefening 1: Getallen zoeken

Deze oefening maak je in bestand `oefening1.ts`.&#x20;

```javascript
let items = [2, 5, 3, 7, 8, 10, 15, 18, 24, 111, 12, 19, 87];
```

* schrijf een functie die een getal zoekt in een array en de index teruggeeft in de array.
* voorbeeld:

```javascript
 console.log(search(items, 5)); // 1 
 console.log(search(items, 15)); // 6
```

{% hint style="info" %}
Vergeet niet alles een type te geven! Incl bv. de lijn let items!
{% endhint %}

### Oefening 2: Strings omdraaien

Deze oefening maak je in bestand `oefening2.ts`.&#x20;

* Schrijf een functie `reverseString`die een string omdraait
* De functie heeft 1 parameter
* De functie geeft een string terug
* voorbeeld input:  **hello**;\
  verwachte return waarde: **olleh**

{% hint style="info" %}
for loops kunnen in 2 richtingen lopen!
{% endhint %}

### Oefening 3

Deze oefening maak je in bestand `oefening3.ts`.&#x20;

* Schrijf een functie `multiplyText` die 2 parameters heeft: `amount` en `text`
* De functie geeft een string terug. Deze string bevat de inhoud van text het aantal keer dat in amount staat bv:

```javascript
let result: string = multiplyText(3, "flower");
//result is "flower flower flower
```

* Wanneer geen waarde voor de tweede parameter wordt meegegeven, dan is de waarde van die parameter het woord "default"
* Voeg nu een derde, **optionele** parameter toe genaamd `appendix` van het type string
* Deze appendix wordt toegevoegd achteraan de finale string bv.

```javascript
let result: string = multiplyText(3, "flower", "!");
//result is "flower flower flower!
```

* roep deze functie op met jouw naam als 2e parameter en print dit naar de console
* roep deze functie op maar laat de functie default waarde voor `text` gebruiken (geef dus geen waarde mee met de 2e parameter) en geef `?` als appendix mee

### Oefening 4

Deze oefening maak je in bestand `oefening4.ts`.&#x20;

{% hint style="info" %}
`Require` zal standaard niet werken. Hiervoor installeer je eerst het volgende: `npm install @types/node --save-dev`
{% endhint %}

{% hint style="info" %}
Je kan ook het volgende gebruiken indien `require` errors blijft geven:\
`import * as chalk from "chalk";`
{% endhint %}



\


* installeer het npm package chalk: [https://www.npmjs.com/package/chalk](https://www.npmjs.com/package/chalk)
* lees goed de uitleg over de module zodat je weet hoe je die moet gebruiken
* kopieer de functie van oefening 3 in oefening 4.ts en hernoem ze naar `multiplyTextColor`
* Maak een enum aan die 3 kleuren bevat: red, green, blue
* Maak een nieuwe parameter aan in jouw functie, `color` van het type van de enum die je hebt aangemaakt
* In deze functie ga je nu geen string meer teruggeven, maar je gaat rechtstreeks naar de console printen in de kleur van de nieuwe parameter `color` \
  bv:

```typescript
multiplyText(3,"flower",Color.Red,"!");
```

![](<../.gitbook/assets/image (3) (1).png>)

### Commit/push!

Zorg dat je al jouw commits pusht naar Github voor vrijdag 23:59.
