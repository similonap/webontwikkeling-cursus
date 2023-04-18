# Labo 7

## myMovieDb

We bouwen in deze oefening een nieuwe **express** applicatie. Zorg ervoor dat deze in een aparte folder staat met dezelfde naam als de oefening. Je maakt het volledig labo in het bestand `index.ts`

Maak een Express applicatie aan die luistert op poort 3000 (zie syllabus).

### Header en footer

Maak een aparte header / footer template die een titel van jouw app, een logo en link naar een css file bevat

* het logo bevindt zich op jouw server. Gebruik dus geen externe urls om het logo te tonen
* gebruik css om jouw header en de andere paginas die we gaan maken te stylen. Hiervoor gebruik je een externe css file die je in jouw header linkt.

De invulling van deze header en footer mag je volledig zelf beslissen.&#x20;

### Landing page

Maak een welkom pagina die we kunnen oproepen via http://localhost:3000.&#x20;

* zorg dat je zeker de header en footer template importeert
* zorg dat de landingspagina wat info over jouw app bevat (wat tekst)

Het kan er als volgt uitzien:\


<figure><img src="../.gitbook/assets/Screenshot 2023-04-17 at 22.49.12.png" alt=""><figcaption></figcaption></figure>

### Movies

Maak een movies pagina die we kunnen oproepen via http://localhost:3000/movies

Maak een globale variabele aan movies zoals hieronder:

```typescript
let movies : Movie[] = [
    {name: "The Matrix", myScore: 90, image: "https://cdn.shopify.com/s/files/1/0057/3728/3618/products/9fcc8387e9d47ab5af4318d7183f6d2b_19f7e1e1-3941-4c27-bad1-1f6dd70f35e0_480x.progressive.jpg?v=1573587594", description: ""},
    {name: "Pulp Fiction", myScore: 100, image: "https://cdn.shopify.com/s/files/1/0057/3728/3618/products/pulpfiction.2436_500x749.jpg?v=1620048742", description: ""},
    {name: "Monster Hunter", myScore: 5, image: "https://cdn.shopify.com/s/files/1/0057/3728/3618/products/monsterhunter.styleb.ar_500x749.jpg?v=1608660576", description: ""},
    {name: "Blade Runner", myScore: 100, image:"https://cdn.shopify.com/s/files/1/0057/3728/3618/products/d9f6067d2406a7cfbf42a5fc4ae4cd9d_8174831c-db77-4608-9ae2-44aca8f2a6f5_500x749.jpg?v=1573585461", description:""}
];
```

* zorg dat je zeker de header / footer template importeert
* toon een lijst van de films van de movies variabel op deze pagina. Gebruik CSS om deze lijst wat stijl te geven.
* zorg dat de landing page naar deze pagina wijst (pas dus de landing page aan)
* zorg dat je via een link naar de landingpage kan

Dit kan er ongeveer als volgt uitzien:

<figure><img src="../.gitbook/assets/Screenshot 2023-04-17 at 22.49.56.png" alt=""><figcaption></figcaption></figure>

### Movie

Maak een movie pagina die we kunnen oproepen via http://localhost:3000/movies/X waar X een getal is.

* zorg dat je zeker de header/footer template importeert
* toon de film die zich op index X bevindt in de movies array
* zorg dat je bij elke movie op de movies pagina naar de movie pagina van die specifieke film kan gaan via een link.&#x20;
* zorg dat je via een link terug naar de movies pagina kunt
* Hoe rekening met het feit dat de gebruiker een index kan ingeven die hoger is dan het aantal elementen (voorzie een error page)

<figure><img src="../.gitbook/assets/Screenshot 2023-04-17 at 22.51.34.png" alt=""><figcaption></figcaption></figure>

### AddMovie

Maak een addmovie pagina aan die we kunnen oproepen via http://localhost:3000/addmovie .

* toon een form met 2 velden: Title en My Score
* dit form gebruikt de POST methode
* zorg dat de submit knop de data verstuurt en toevoegt aan de movies array
* Toon een bevestigingsbericht als de film is toegevoegd aan de array en laat terug de movies pagina zien.

{% hint style="info" %}
app.get('/addmovie',.. en app.post('/addmovie',.. zijn 2 verschillende routes. Gebruik de get route om het formulier te tonen. Gebruik de post route om de data te ontvangen. Beiden kunnen dezelfde EJS file als response terugsturen (zo ziet de gebruiker opnieuw het formulier na het de submitten)
{% endhint %}

<figure><img src="../.gitbook/assets/Screenshot 2023-04-17 at 22.52.46.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2023-04-17 at 22.57.41.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2023-04-17 at 23.00.33.png" alt=""><figcaption></figcaption></figure>



### Uitbreiding (PRO)

* Breidt de webapplicatie uit met een login systeem.
* De gebruiker kan aan de hand van een username en paswoord inloggen op het systeem.
* Alleen users die ingelogd zijn kunnen films toevoegen.
* Zorg dat de paswoorden gehashed (SHA-256) zijn in de database.
* Je kan de session middleware gebruiken voor bij te houden of de gebruiker is ingelogt of niet
  * [https://expressjs.com/en/resources/middleware/session.html](https://expressjs.com/en/resources/middleware/session.html)
* De gebruiker moet zichzelf kunnen uitloggen.
* Maak een signup page voor een gebruiker toe te voegen in de users array.
