# Environment Variables

## Wat zijn Environment Variables?&#x20;

Letterlijk vertaald betekent het omgevingsvariabelen. Ze bieden informatie over de werkomgeving van een Node project.&#x20;

**Omgevingsvariabelen in Node worden gebruikt om:**

* Gevoelige gegevens op te slaan, zoals wachtwoorden, API-referenties en andere informatie die niet rechtstreeks in je code mag worden geschreven om beveiligingsrisico's te voorkomen.&#x20;
* Instellingen te configureren die kunnen verschillen tussen omgevingen. Denk maar aan poorten en verwijzingen naar databanken (development, staging, test of productie).

Je hebt out of the box toegang tot omgevingsvariabelen in Node.js. Wanneer je een Node server opstart, biedt het automatisch toegang tot alle bestaande omgevingsvariabelen door een `env`-object te maken binnen het globale `process` object.

Ga je gang en probeer het globale `process` object en daarvan de `env` eigenschap eens te loggen in je console. Maak een lege map met de naam **env-tryout.** Maak vervolgens een bestand met de naam **server.js** en voeg de onderstaande code eraan toe.

```javascript
// server.js
console.log(process.env);
```

Deze code retourneert alle omgevingsvariabelen die op het object `process.env` leven. Om toegang te krijgen tot een specifieke variabele, benader je deze zoals een eigenschap van een object:

```javascript
console.log('The value of PORT is:', process.env.PORT);
```

Wanneer je nu `node server.js` uitvoert, zou je een bericht moeten zien met de tekst _"The value of PORT is: undefined"_.

Je omgevingsvariabele is er niet omdat de eigenschap PORT geen standaard variabele is van het `process.env` object. We moeten deze zelf definiëren. Laten we eens kijken naar manieren waarop we dit kunnen oplossen.

* Met behulp van de **terminal**;
* Met behulp van een **.env-bestand**;

#### Terminal

De eenvoudigste manier om de PORT variabele een waarde te geven, is door deze in je terminal tijdens de opstart van je server te declareren. Je geeft de naam van de variabele op, gevolgd door het gelijkteken en de waarde. Roep vervolgens je Node.js-app aan.

```
PORT=3000 node server.js
```

Normaliter zie je nu het volgende bericht:  _"The value of PORT is: 3000"_.

Je kan dit patroon herhalen en ook andere variabelen toevoegen. Hier is een voorbeeld van het doorgeven van twee omgevingsvariabelen.

```
PORT=3000 NODE_ENV=development node server.js
```

#### Een .env-bestand

Als je er eenmaal een aantal hebt gedefinieerd, zal je snel merken dat het een onderhoudsnachtmerrie wordt. Stel je voor dat je een tiental omgevingsvariabelen gebruikt. Dit schaalt niet goed als je ze allemaal op één regel moet typen.

**Omgevingsvariabelen uitvoeren vanaf een terminal is zeker handig. Maar het heeft zijn nadelen:**

* Je kan de lijst met variabelen niet raadplegen;
* Het is veel te gemakkelijk om een typfout te maken;

Een populaire oplossing voor het organiseren en onderhouden van je omgevingsvariabelen is het gebruik van een `.env`-bestand. Het helpt ons om alle omgevingsvariabelen op één plek te definiëren en indien nodig te wijzigen.

Maak het `.env`-bestand ergens in de bestandenstructuur van je applicatie en voeg je variabelen en waarden eraan toe.

{% code title=".env" %}
```json
NODE_ENV=development
PORT=3000
# Zet je database/API connectie informatie hier
API_KEY=**************************
API_URL=**************************
```
{% endcode %}

#### Een .gitignore-bestand

Een .`env`-bestand is een geweldige manier om al je omgevingsvariabelen op één plek te verzamelen. Zorg er wel voor dat je het `.env`-bestand niet in een version control systeem zoals Git plaatst. Anders bevat je version control historiek referenties van je omgevingsvariabelen. Dit zou een beveiligingsrisico vormen aangezien er gevoelige informatie in je omgevingsvariabelen kan staan.

#### Gebruik in Docker
In een Docker Compose file kan je een of meerdere `.env`-bestanden inladen door middel van een key `env_file`. Je vindt hiervan een voorbeeld in de [Docker Compose reference](https://docs.docker.com/compose/compose-file/#env_file).

Wanneer deze zijn ingeladen, kunnen applicaties in de container de variabelen gebruiken. Een Node.js-applicatie kan bijvoorbeeld `process.env.MYVARIABLE` gebruiken. Ze kunnen ook gebruikt worden in zogenaamde Bash-instructies voor de container (zoals `postStartCommand`), maar daar moet je dan het formaat `$MYVARIABLE` gebruiken.

#### Resources

* [Wat zijn Omgevingsvariabelen en hoe maak je een .env file aan?](https://www.codementor.io/@parthibakumarmurugesan/what-is-env-how-to-set-up-and-run-a-env-file-in-node-1pnyxw9yxj)
