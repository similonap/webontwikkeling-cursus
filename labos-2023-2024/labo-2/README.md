# Labo 2

{% hint style="info" %}
**Alle oefeningen van dit labo dienen in een folder `labo_2` te staan**
{% endhint %}

### Oefening: arrow notatie

* Maak een nieuwe folder **arrow** waarin je jouw bronbestanden voor deze oefening kan plaatsen.
* Deze oefening maak je in bestand `arrow.ts`.
* Schrijf de volgende functies in de kortst mogelijke arrow notaties:

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

### **Oefening: TryParse**

* Maak een nieuwe folder **tryparse** waarin je jouw bronbestanden voor deze oefening kan plaatsen.
* Maak een nieuw bestand **tryparse.ts** met de volgende inhoud:

```typescript
const tryParseInt = (str: string) => {
    let number = parseInt(str);
    if (isNaN(number)) {
        throw Error("Cannot parse this number");
    }
    return number;
}
```

* Experimenteer met het gebruik van deze functie.&#x20;
* Probeer deze functie eens aan te roepen met een willekeurige string (geen getal) en kijk wat er gebeurd.
* Handel deze exception af met try catch.&#x20;

### **Oefening: Wiskunde**

* Maak een nieuwe folder **wiskunde** waarin je jouw bronbestanden voor deze oefening kan plaatsen.
* Maak een nieuw bestand `wiskunde.ts`&#x20;
* Installeer de npm package `math-expression-evaluator` (documentatie kan je vinden op [https://www.npmjs.com/package/math-expression-evaluator](https://www.npmjs.com/package/math-expression-evaluator))
* Deze package laat het toe om wiskundige uitdrukkingen uit te voeren. Als je bijvoorbeeld `math.eval("1+5")` doet zal deze 6 teruggeven.&#x20;
* Maak hiervoor steeds een nieuwe constante aan: `const mat = new mexp;`
* Vraag de gebruiker om een wiskundige uitdrukking in te geven.
* Toon het resultaat van deze uitdrukking.&#x20;
* De `math.eval` functie geeft een exception als je iets meegeeft dat geen wiskundige uitdrukking is. Dit moet je dus zelf niet maken, je moet deze exception wel opvangen en afhandelen.

**Voorbeeldinteractie**

```
Geef een berekening die je wil uitvoeren? 5+5
10
```

```
Geef een berekening die je wil uitvoeren? pi
3.141592653589793
```

```
Geef een berekening die je wil uitvoeren? stomding
Dit is geen wiskundige uitdrukking
```

### **Oefening: Moo**

* Maak een nieuwe folder **moo** waarin je jouw bronbestanden voor deze oefening kan plaatsen.
* Maak een nieuw bestand `moo.ts`&#x20;
* Installeer de npm package `cowsay` (documentatie kan je vinden op [https://www.npmjs.com/package/cowsay](https://www.npmjs.com/package/cowsay))
* Maak een **arrow functie** `say` met een stuk text als parameter. Zorg dat deze functie een interface heeft.
* Als er een lege string wordt meegegeven moet de say functie een exception throwen met de tekst "Text is a mandatory field"
* De exception wordt opgevangen bij het oproepen van de functie.&#x20;
* Vraag de gebruiker (via readline-sync) wat de koe moet zeggen.
* Zorg ervoor dat er bij een exception de vraag opnieuw gesteld wordt.
* Indien de string niet leeg is dan laat je de koe dit zeggen.

**Voorbeeld interactie:**

```
What should the cow say? Mooooooo
 __________
< Mooooooo >
 ----------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

```
What should the cow say? 
text field is mandatory.
What should the cow say? 
text field is mandatory.
What should the cow say? Moo
 _____
< Moo >
 -----
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

### \[Pro] Oefening leesStudenten

{% hint style="info" %}
**Pro oefeningen** kunnen concepten bevatten die niet altijd in de theorieles is behandeld.  Begin niet aan deze oefeningen voordat je de vorige oefeningen gemaakt hebt.&#x20;
{% endhint %}

* Maak een nieuwe folder **leesStudenten** waarin je jouw bronbestanden voor deze oefening kan plaatsen.
* Maak een nieuw bestand `leesStudenten.ts`
* Maak een nieuw bestand `studenten.csv` met de volgende inhoud

```
Andie Similon,12,14,15,17,11,10
Sven Charleer,10,12,14,13,12,9
Clark Kent,5,12,14,16,15,3
Peter Parker,15,17,18,19,15,17
```

* gebruik `require` om  de  `fs` package te gebruiken. Deze package zit ingebakken in node js dus je hoeft hier dus niets speciaal voor te installeren.
* [https://nodejs.org/api/fs.html#fsreadfilesyncpath-options](https://nodejs.org/api/fs.html#fsreadfilesyncpath-options)
* Zorg voor een interface `Student` die de volgende properties bevat (de types bepaal je zelf)
  * naam
  * punten
* Maak een arrow function met de naam `readFile`  met de naam van de file als argument.
  * Deze functie leest het bestand uit aan de hand van de `fs.readFileSync` functie
  * Daarna splitst hij deze lijn per lijn op en zorgt dat de lijn wordt omgezet naar een `Student` object.&#x20;
  * De functie geeft een array van `Student` objecten terug.
  * Zorg ervoor dat er een exception gegooid wordt als een van de cijfers geen getal is.
  * **Tip**: gebruik hiervoor de `split()` methode op een string
* Maak een arrow function met de naam `calculateAverage` die het gemiddelde berekend voor een reeks getallen.
* Roep de `readFile` functie op en zorg voor foutafhandeling met try catch
  * Test de volgende scenarios:
    * Een van de punten in de csv file is geen getal
    * Het csv bestand bestaat niet
* Print voor elke student een overzicht met zijn naam en de gemiddelde score

**Voorbeeldinteractie**

```
ts-node files.ts
Something went wrong opening the file
```

```
Naam: Andie Similon
Gemiddelde: 13
Naam: Sven Charleer
Gemiddelde: 12
Naam: Clark Kent
Gemiddelde: 11
Naam: Peter Parker
Gemiddelde: 17
```
