# Labo 1

### Voorbereiding

Voordat je dit labo start moet je de volgende topics bekeken hebben!

* NPM
* Arrow Functions
* Interfaces (Objects en Functions)

### Opzetten Git Repository

* Log in op [https://gitlab.apstudent.be/webontwikkeling20232024](https://gitlab.apstudent.be/webontwikkeling20232024) met je studenten credentials.
* Navigeer naar je klasgroep en vervolgens je persoonlijke groep (jouw naam)
  * Als je nog geen toegang hebt tot deze repository vraag dan toegang aan je lector.
* Maak een nieuwe git repository aan met de naam **Webontwikkeling**
* Zorg dat je een `.gitignore` bestand in je git repository hebt staan
  * **Bijvoorbeeld**: [https://www.toptal.com/developers/gitignore/api/node](https://www.toptal.com/developers/gitignore/api/node)&#x20;
* Maak een nieuw bestand aan README in de root van je git repository met als inhoud:\
  Voornaam Achternaam - Jouw Email Adres
* Commit en push dit bestand.

{% hint style="info" %}
**Alle oefeningen van dit labo dienen in een folder `labo_1` te staan**
{% endhint %}

{% hint style="info" %}
**Na elke oefening dien je de laatste wijzigingen te comitten en pushen naar git**
{% endhint %}

### **Oefening 1: cat-me**

Maak een nieuwe folder **cat-me** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Maak een nieuw bestand `cat-me.ts`&#x20;

We gaan gebruik maken van de module[ cat-me](https://www.npmjs.com/package/cat-me). Volg de instructies op de npm pagina en print een kat op jouw console. De `catMe()` functie heeft als return type `string` en het loggen zal je zelf moeten doen.

Zorg dat je zeker `require` gebruikt!

{% hint style="info" %}
Vergeet de commando's&#x20;

```
tsc --init
npm install --save-dev @types/node
```

niet uit te voeren in je cat-me folder.
{% endhint %}

### Oefening 2a: goodbye-functions

Maak een nieuwe folder **goodbye** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Maak een nieuw bestand `goodbye_a.ts`

Pas de volgende code aan zodat het arrow functions gebruikt in plaats van het function keyword.

```typescript
const languages = [
  "english",
  "french",
  "spanish",
  "german",
  "dutch",
  "italian",
];

function getGoodbyeInLanguage(language: string = "english"): string {
  if (language === "english") {
    return "Goodbye";
  } else if (language === "french") {
    return "Au revoir";
  } else if (language === "spanish") {
    return "Adiós";
  } else if (language === "german") {
    return "Auf Wiedersehen";
  } else if (language === "dutch") {
    return "Tot ziens";
  } else if (language === "italian") {
    return "Arrivederci";
  } else {
    return "Language not found";
  }
}

function getRandomLanguage(): string {
  return languages[Math.floor(Math.random() * languages.length)];
}

function sayGoodbye(name: string) {
  let goodbye = getGoodbyeInLanguage(getRandomLanguage());
  console.log(`${goodbye}, ${name}`);
}

function sayGoodbyeTimes(name: string, times: number) {
  for (let i = 0; i < times; i++) {
    sayGoodbye(name);
  }
}

sayGoodbyeTimes("Andie", 5);
```

Gebruik zo veel mogelijk de verkorte notatie waar mogelijk!

### **Oefening 2b: goodbye-functions (uitbreiding)**

**Deze oefening gaat gewoon verder op de vorige goodbye-functions oefening**

Maak een kopie van `goodbye_a.ts` en noem dit`goodbye_b.ts`

* Maak een interface voor alle functies en gebruik deze.
* **Indien je exceptions al gezien hebt:** Zorg ervoor dat je exceptions gebruikt voor de onbestaande taal op te vangen. Gebruik ook try catch om deze op te vangen.

### Oefening 3a: Movies

Maak een nieuwe folder **movies** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Maak een nieuw bestand `movies_a.ts`

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

### Oefening 3b: Movies

Maak een kopie van `movies_a.ts` en noem dit`movies_b.ts`

In deze oefening maken we 2 functies aan:

*   de functie `wasMovieMadeInThe90s`&#x20;

    * met de parameter `movie` van type `Movie`
    * met return waarde `true` or `false` (of de film in de jaren 90 is gemaakt of niet)
    * roep deze functie op met The Matrix en jouw favoriete film


*   de functie `averageMetaScore`&#x20;

    * met de parameter `movies` die een array van het type `Movie` bevat
    * met return waarde de gemiddelde score van alle films in die array&#x20;
    * print het gemiddelde van metascore van de 3 films adhv deze functie


* de functie `fakeMetaScore`
  * met de parameters
    * &#x20;`movie` van het type `Movie`&#x20;
    * `newscore` die een nieuwe score bevat
  * met return waarde een nieuw `Movie` object met de nieuwe score

### Oefening 3c: Movies

Maak een kopie van `movies_b.ts` en noem dit`movies_c.ts`

Maak 3 interfaces aan:

* een interface die de functie `wasMovieMadeInThe90s` omschrijft
* een interface die de functie `averageMetaScore` omschrijft
* een interface die de functie`fakeMetaScore`omschrijft

