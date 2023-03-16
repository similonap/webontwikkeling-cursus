# Labo 6

### Maaltafels

Maak een nieuwe folder **maaltafels** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Installeer alle nodige libraries voor te werken met express en ejs.

Maak een nieuw bestand `index.ts` aan met de volgende inhoud:

```typescript
const express = require("express");
const app = express();

app.set("port",3000);
app.set("view engine", "ejs");

app.get("/", (req:any,res:any) => {
    res.render("maaltafels");
})

app.listen(app.get("port"), () => {
    console.log(`Web application started at http://localhost:${app.get("port")}`)
})
```

Maak nu een nieuwe ejs file aan die de maaltafels van 1 tot en met 10 toont in je browser als je surft naar http://localhost:3000&#x20;

Je mag geen aanpassingen maken in de `index.ts` file. Het opbouwen van de tabel moet volledig gebeuren in het ejs bestand.

**De output in de browser moet er als volgt uitzien:**

![](<../.gitbook/assets/Screenshot 2022-03-21 at 15.27.43.png>)

### Mathservice

Maak een nieuwe folder **mathservice** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Installeer alle nodige libraries voor te werken met express en ejs.

Maak een nieuwe express applicatie in een `index.ts` bestand. We gaan een web applicatie maken die de volgende wiskundige operatoren kan uitvoeren: **add, min, mult en div**&#x20;

Zorg voor 1 GET-route die urls in de volgende vorm kan afhandelen:

```
http://localhost:3000/add?a=3&b=5
http://localhost:3000/min?a=3&b=5
http://localhost:3000/mult?a=3&b=5
http://localhost:3000/div?a=3&b=5
```

**Je moet dus query parameters (voor a en b) EN route parameters (voor de operatoren) gebruiken**

Je krijgt dan een output in de volgende vorm (json):

```
{
    "result": 8
}
```

Als 1 van de twee parameters (a en b) niet zijn opgegeven krijg je het volgende json object terug:

```
{
    "error": "Both query parameters (a,b) have to be specified."
}
```

### Catstatic

Maak een nieuwe folder **catstatic** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Installeer alle nodige libraries voor te werken met express en ejs.

Maak een nieuwe express applicatie in een `index.ts` bestand. Zorg voor een GET route op `/cats/images` &#x20;

Zorg ervoor dat de volgende images getoond worden als je naar `http://localhost:8888/cats/images` surft. **We maken gebruik van ejs en niet van een statische html bestand.**

{% file src="../.gitbook/assets/cats.zip" %}

Zorg voor een **extern css bestand** waar je een eigen style geeft aan de pagina.&#x20;

![](<../.gitbook/assets/Screenshot 2022-03-21 at 20.53.05.png>)

### Contact

Maak een nieuwe folder **contact** waarin je jouw bronbestanden voor deze oefening kan plaatsen.

Installeer alle nodige libraries voor te werken met express en ejs.

Maak een nieuwe express applicatie in een `index.ts` bestand.&#x20;

Voorzie een route `/contact` met een apart ejs bestand waar je het volgende contact formulier op laat zien:

![](<../.gitbook/assets/Screenshot 2022-03-21 at 21.01.23.png>)



Als de gebruiker alles invult (dit moet niet nagekeken worden) en op submit drukt moet er een POST request gedaan worden naar dezelfde route (maar met een post). Deze route gebruikt een ander ejs bestand. De volgende tekst moet getoond worden. Hier moet uiteraard de naam, email en bericht vervangen worden met het doorgestuurde bericht:

![](<../.gitbook/assets/Screenshot 2022-03-21 at 21.00.28.png>)

**Uitbreiding:**

Gebruik het include keyword in ejs om het contact formulier terug te importeren onderaan de bevestiging pagina:

![](<../.gitbook/assets/Screenshot 2022-03-21 at 21.09.28.png>)

**PRO: Contact Uitbreiding**

Zorg ervoor dat alle toevoegingen via het contact formulier worden opgeslagen in een json bestand `emails.json`.&#x20;

Dit json bestand wordt bij het opstarten van de applicatie ingelezen en bij elke  nieuwe toevoegen wordt deze terug opgeslagen.&#x20;

Zorg voor een extra veld in de form die toestaat om een file mee te sturen bij het contact formulier.

![](<../.gitbook/assets/Screenshot 2022-03-28 at 11.28.15.png>)

Gebruik de npm package [https://www.npmjs.com/package/express-fileupload](https://www.npmjs.com/package/express-fileupload) om deze af te handelen. Zorg ervoor dat de bestanden worden opgeslagen in een files directory en dat het pad naar dit bestand mee in de `emails.json` file worden opgeslagen.
