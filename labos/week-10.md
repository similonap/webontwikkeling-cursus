# Week 10

DAG studenten: Pushen naar Github VOOR vrijdag 7/5/2021 23:59\
AVOND studenten: Pushen naar Github VOOR zondag 9/5/2021 23:59

## Setup

Maak een folder `Labo9` in jouw webontwikkeling folder aan. Maak daar een bestand aan dat noemt `index.ts`en commit/push die file, en **kijk na of je die ook op Github ziet staan!**

{% hint style="info" %}
**Belangrijk:** Na elk stukje code dat je schrijft, test je jouw code. Wanneer die werkt, commit je die code! Zo kan je altijd terugkeren naar een werkende versie, en kunnen wij ook jouw vooruitgang volgen.
{% endhint %}

{% hint style="info" %}
**Belangrijk**: We werken met **TypeScript**. Type dus ook alle variabelen en functies
{% endhint %}

{% hint style="info" %}
**Belangrijk:** Vergeet niet `tsc --init` en `npm install @types/node` te doen voor het project te initialiseren.
{% endhint %}

## Express

Je maakt het volledig labo in het bestand `index.ts`

* Maak een Express applicatie aan die luistert op poort 3000 (zie syllabus).

{% hint style="info" %}
Stuur voor elke route gewoon een standaard "hello world" terug
{% endhint %}

{% hint style="danger" %}
Commit dit naar git (!) en ga verder.
{% endhint %}

## Header

Maak een aparte header template die een titel van jouw app, een logo en link naar een css file bevat

* het logo bevindt zich op jouw server. Gebruik dus geen externe urls om het logo te tonen
* gebruik css om jouw header en de andere paginas die we gaan maken te stylen. Hiervoor gebruik je een externe css file die je in jouw header linkt.

## Landing page

Maak een welkom pagina die we kunnen oproepen via http://localhost:3000.&#x20;

* zorg dat je zeker de header template importeert
* zorg dat de landingspagina wat info over jouw app bevat (wat tekst)

## Movies

Maak een movies pagina die we kunnen oproepen via http://localhost:3000/movies

Maak een globale variabel aan movies zoals hieronder:

```typescript
let movies = [
    {name: "The Matrix", myScore: 90},
    {name: "Pulp Fiction", myScore: 100},
    {name: "Monster Hunter", myScore: 5},
    {name: "Blade Runner", myScore: 100}
];
```

* zorg dat je zeker de header template importeert
* toon een lijst van de films van de movies variabel op deze pagina. Gebruik CSS om deze lijst wat stijl te geven.
* zorg dat de landing page naar deze pagina wijst (pas dus de landing page aan)
* zorg dat je via een link naar de landingpage kan

## Movie

Maak een movie pagina die we kunnen oproepen via http://localhost:3000/movies/X waar X een getal is.

* zorg dat je zeker de header template importeert
* toon de film die zich op index X bevindt in de movies array
* zorg dat je bij elke movie op de movies pagina naar de movie pagina van die specifieke film kan gaan via een link (pas dus movies aan)
* zorg dat je via een link terug naar de movies pagina kunt

## EXTRA UITDAGING: AddMovie

Maak een addmovie pagina aan die we kunnen oproepen via http://localhost:3000/addmovie .

* toon een form met 2 velden: Title en My Score
* dit form gebruikt de POST methode
* zorg dat de submit knop de data verstuurt en toevoegt aan de movies array

{% hint style="info" %}
app.get('/addmovie',.. en app.post('/addmovie',.. zijn 2 verschillende routes. Gebruik de get route om het formulier te tonen. Gebruik de post route om de data te ontvangen. Beiden kunnen dezelfde EJS file als response terugsturen (zo ziet de gebruiker opnieuw het formulier na het de submitten)
{% endhint %}

Vergeet niet alles te commiten en te pushen naar Github.
