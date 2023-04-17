# Week 9

DAG studenten: Pushen naar Github VOOR vrijdag 23/4/2021 23:59\
AVOND studenten: Pushen naar Github VOOR zondag 25/4/2021 23:59

## Setup

Maak een folder `Labo8` in jouw webontwikkeling folder aan. Maak daar een bestand aan dat noemt `index.ts`en commit/push die file, en **kijk na of je die ook op Github ziet staan!**

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
* Zorg dat volgende urls werken:
  * `localhost:3000`
  * `localhost:3000/whoami`
  * `localhost:3000/whoamijson`
  * `localhost:3000/pikachujson`
  * `localhost:3000/pikachuhtml`

{% hint style="info" %}
Stuur voor elke route gewoon een standaard "hello world" terug
{% endhint %}

{% hint style="danger" %}
Commit dit naar git (!) en ga verder.
{% endhint %}

**Localhost:3000**

* Zorg dat `localhost:3000` een html pagina stuurt waarin je een header met de titel van jouw applicatie (kies zelf iets) met een kleine paragraaf die een beschrijving geeft

**Localhost:3000/whoami & Localhost:3000/whoamijson**

{% hint style="warning" %}
Gebruik EJS om de HTML pagina te tonen!
{% endhint %}

*   Maak een globale variabele aan `thisisme` die een object bevat met 3 properties:

    * `name`
    * `age`
    * `profilePic`

    De `profilepic` property bevat een url van een online foto (kies zelf iets)\

* Zorg dat `localhost:3000/whoami` een HTML pagina toont met:
  * de zin "My name is _XXX_ and I am _YYY_ years old" met XXX en YYY de waarden van de properties van de `thisisme` variabel en
  * de foto uit profilePic
* Zorg dat `localhost:3000/whoamijson` de inhoud van `thisisme` stuurt als JSON.

{% hint style="info" %}
Test met curl -v dat de content-type correct is!
{% endhint %}

**Localhost:3000/pikachujson & Localhost:3000/pikachuhtml**

{% hint style="warning" %}
Gebruik EJS om de HTML pagina te tonen!
{% endhint %}

* Doe een API call naar [https://pokeapi.co](https://pokeapi.co)  om de data van Pikachu op te halen en steek die in een globale variabel `pikachu`.
* Zorg dat `localhost:3000/pikachujson` de data van `pikachu` als JSON terugstuurt
* Zorg dat `localhost:3000/pikachuhtml` een mooie pikachu HTML pagina toont. Deze moet de volgende zaken zeker bevatten:
  * de naam
  * id
  * gewicht
  * een image van Pikachu's voorkant (zie sprites)
  * een image van Pikachu's achterkant (zie sprites)



&#x20;
