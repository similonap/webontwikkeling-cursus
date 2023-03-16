# Week 5

DAG studenten: Pushen naar Github VOOR vrijdag 12/3/2021 23:59\
AVOND studenten: Pushen naar Github VOOR zondag 14/3/2021 23:59

## Setup

Maak een folder `Labo4` in de folder die we vorige week hebben aangemaakt. Maak daar een bestand aan dat noemt `oefening1.ts`en commit/push die file, en **kijk na of je die ook op Github ziet staan!**

{% hint style="info" %}
**Belangrijk:** Na elk stukje code dat je schrijft, test je jouw code. Wanneer die werkt, commit je die code! Zo kan je altijd terugkeren naar een werkende versie, en kunnen wij ook jouw vooruitgang volgen.
{% endhint %}

{% hint style="info" %}
**Belangrijk**: We werken met **TypeScript**. Type dus ook alle variabelen en functies
{% endhint %}

## Modules

We gaan nog eventjes opnieuw een module inladen. Om ons `require` probleem op te lossen, kunnen we gebruik maken van hetvolgende in de terminal (in jouw Labo4 folder):

```
npm i --save-dev @types/node
npx tsc --init
```

{% hint style="info" %}
Als npx tsc niet werkt, kan je ook `tsc --init` doen
{% endhint %}

Dit initialiseert jouw project voor TypeScript en maakt een bestand genaamd `tsconfig.json`. Kijk gerust eens rond in dit bestand. Dit laat ons ook toe `require` te gebruiken zoals de meeste npm packages voorstellen. Dit doen we door de lijn `"moduleResolution": "node",` te activeren. Verwijder de `//` die zorgen dat dit uitgecomment is. Om te testen of alles werkt, maak oefening 1!

## Oefening 1: Cat-me

Deze oefening maak je in bestand `oefening1.ts`.&#x20;

Niet alle oefeningen moeten moeilijk zijn ;) We gaan gebruik maken van de module[ cat-me](https://www.npmjs.com/package/cat-me). Volg de instructies op de npm pagina en print een kat op jouw console. Zorg dat je zeker `require` gebruikt!

## Oefening 2a: Interfaces

Deze oefening maak je in bestand `oefening2.ts`.&#x20;

Hieronder zie je een json object:

```javascript
{
    "title": "The Matrix",
    "year": 1999,
    "actors": ["Keanu Reeves", "Laurence Fishburne", "Carrie-Anne Moss"],
    "metascore": 73,
    "seen": true
}
```

In jouw ts file, maak een variable `thematrix` van het Interface type `Movie` en zorg dat die variable de properties en waarden van hierboven bevatten.

{% hint style="info" %}
De interface Movie maak je natuurlijk zelf
{% endhint %}

{% hint style="info" %}
Vergeet niet dat er een verschil in notatie is tussen JSON en een object in TypeScript
{% endhint %}

Maak een tweede variable aan `myfavoritemovie` van het type Movie en geef die een object mee die de info over jouw favoriete film bevat.

Maak een derde variable aan `myworstmovie` van het type Movie en geef die een object mee die de info over jouw meest gehate film bevat.

## Oefening 2b: Functions

Deze oefening maak je in **OOK in bestand `oefening2.ts`.**&#x20;

In deze oefening maken we 2 functies aan:

*   de functie `wasMovieMadeInThe90s`&#x20;

    * met de parameter `movie` van type `Movie`
    * met return waarde `true` or `false` (of de film in de jaren 90 is gemaakt of niet)
    * roep deze functie op met The Matrix en jouw favoriete film


*   de functie `averageMetaScore`&#x20;

    * met de parameter `movies` die een array van het type `Movie` bevat
    * met return waarde de gemiddelde score van alle films in die array&#x20;
    * print het gemiddelde van metascore van de 3 films adhv deze functie


*   de functie `fakeMetaScore`

    * met de parameters
      * &#x20;`movie` van het type `Movie`&#x20;
      * `newscore` die een nieuwe score bevat
    * met return waarde een nieuw `Movie` object met de nieuwe score



## Oefening 2c: Functions

Deze oefening maak je in **OOK in bestand `oefening2.ts`.**&#x20;

Maak 3 interfaces aan:

* een interface die de functie `wasMovieMadeInThe90s` omschrijft
* een interface die de functie `averageMetaScore` omschrijft
* een interface die de functie`fakeMetaScore`omschrijft



###

### Commit/push!

Zorg dat je al jouw commits pusht naar Github voor vrijdag 23:59 (DAGstudenten) of zondag 23:59 (AVONDstudenten)
