# Env files

De eenvoudigste manier om de PORT variabele een waarde te geven, is door deze in je terminal tijdens de opstart van je server te declareren. Je geeft de naam van de variabele op, gevolgd door het gelijkteken en de waarde. Roep vervolgens je Node.js-app aan.

```
PORT=3000 node server.js
```

Normaliter zie je nu het volgende bericht: _"The value of PORT is: 3000"_.

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

