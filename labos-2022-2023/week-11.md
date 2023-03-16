# Labo 8



## MongoDB opzetten

#### 1. Maak een account aan

Ga naar [https://cloud.mongodb.com/](https://cloud.mongodb.com/) en maak een account aan. Na het maken van een account log in via je nieuwe account. Maak vervolgens een nieuwe **Shared Cluster** (is volledig gratis) aan**.**  Kies **AWS**, kies dan als regio: **eu-west-1** in ireland of **eu-central-1** in frankfurt en geef je cluster een naam. Klik vervolgens op **Create Cluster**

**Het aanmaken van je cluster kan tot 5 minuten duren! Hou hier rekening mee**

#### 2. Stel je security settings in

Ga terug naar het overzicht van de clusters en klik op **connect** en bij **Whitelist a connection IP address** kies je Add different ip address. Geef daar `0.0.0.0` in.&#x20;

Als je dit niet vindt, ga links naar **Network Access** en voeg 0.0.0.0 toe als IP adres.

#### 3. Maak een MongoDB gebruiker aan

Vervolgens maak je een nieuwe mongodb gebruiker aan in **Create a MongoDB User.** Zorg ervoor dat het paswoord kan gedeeld worden met ons zodat we ook toegang tot de database hebben.&#x20;

Als je dit niet vindt, ga links naar **Database Access** en voeg een user toe.

#### 4. Haal jouw connection string op

Ga dan verder door op **Choose a connection method** te klikken en klik op Connect your application en kies dan Node.js met versie 3.0 or later

Kopieer de **connection string** en hou deze zeker bij. \
(**tip**: plaats deze in een constante variabele in je index.js bestand, je gaat deze nog nodig hebben)

### **5**. Maak een nieuwe collection aan

Klik op Collections en vervolgens op Add my own data. Maak een nieuwe database aan met de naam **WebOntwikkeling** en als Collection Name: **Movies**

Als je al een database in je account hebt kan je gewoon ook op 'Add Database' drukken.

## Opgave

### 1. Test jouw MongoDB

Zorg ervoor dat je in jouw applicatie connecteert op de database en de lijst van databases in jouw console logt.&#x20;

* zorg dat je  de connectie opent naar jouw database
* zorg dat je de connectie verbreekt als de applicatie eindigt/crasht
* zorg dat in jouw lijst de naam van jouw nieuwe database Webontwikkeling getoond wordt&#x20;

### 2. Insert movies

* Maak volgende variabel aan:

```typescript
let movies = [
    {name: "The Matrix", myScore: 90, timesViewed: 10},
    {name: "Pulp Fuction", myScore: 100, timesViewed: 100},
    {name: "Monster Hunter", myScore: 5, timesViewed:1},
    {name: "Blade Runner", myScore: 100, timesViewed:30},
    {name: "Austin Powers", myScore: 80, timesViewed:10},
    {name: "Jurasic Park 2", myScore: 40, timesViewed:1},
    {name: "Ichi the Killer", myScore: 80, timesViewed:1}
];
```

* Maak een interface aan die overeenkomt met de objecten in movies.&#x20;
* Geef movies het juiste type
* Zorg dat deze films in jouw collection Movies in MongoDB terechtkomen.
* Test door via de website te kijken of je de items ziet staan.

### 3. Find movies

* Zet de de code die de insert doet in de database in commentaar
* Zet de variabel movies in commentaar

{% hint style="info" %}
Gebruik een aparte console.log die een titel toont voor elk van de outputs zodat je ze beter kan onderscheiden. Bv. voor het eerst volgende punt toon je "FIRST MOVIE" en dan pas de eerste film
{% endhint %}

* Doe een query op de database en toon de eerste film op de console
* Doe een  query op de database en&#x20;
  * toon een lijst van alle scores van alle films
  * een totaal van het aantal keren dat deze films bekeken zijn (dus de som van alle timesViewed)
* Toon een lijst van alle films met een score tussen 30 en 85
* Toon een lijst van alle films met een score tussen 30 en 85 OF die maar 1 keer bekeken zijn.

