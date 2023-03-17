# Express Basics

**Frontend**

De frontend is wat de gebruiker ziet: met HTML, CSS en TypeScript (of JavaScript) zorg je voor een structuur waarin de gebruiker kan navigeren. CSS helpt je met layout en opmaak, en TypeScript zorgt voor interactie. Het proces bevindt zich volledig in de browser.&#x20;

Scripts gebruik je om interactie toe te laten door de gebruiker. Deze interactie kan lokale aanpassingen veroorzaken in de client, bv het veranderen van een kleur van een knop, het sorteren van een lijst etc. Maar scripts kunnen ook communiceren buiten het proces in de browser. Adhv API calls kan de client data ophalen van de backend, of data versturen naar de backend.

**Backend**

De backend zorgt voor de connectie met databases, het verwerken van data en het beschikbaar stellen van deze data via een API. Dit proces bevind zich op de server. Client applicaties kunnen deze server applicatie raadplegen om data op te halen of te verwerken.

**Express**

[Express](https://expressjs.com) is een populair Web Application Framework gemaakt op Node.js waarmee we web applicaties en APIs kunnen bouwen.&#x20;

![Express als backend genereert HTML, CSS, JavaScript/TypeScript](.gitbook/assets/les1\_fig1.png)

Aan de hand van Express kunnen we onze applicaties als een full TypeScript (of JavaScript) stack schrijven, m.a.w. onze code op de backend en de code in de client is allemaal TypeScript.

Dit type frameworks laat ons ook toe de client paginas dynamisch te genereren. Dit wil zeggen dat de finale HTML/CSS/TS pagina niet bestaat tot een gebruiker de server raadpleegt. Express zal deze pagina aanmaken met alle nodige data (bv. data uit de database).&#x20;

_Fictief voorbeeld:_  De gebruiker gaat naar http://webontwikkeling.ap/. Express herkent dat de gebruiker de root pagina wil. De ontwikkelaar heeft gezorgd dat Express hier een mooie hoofdpagina toont met de laatste 3 nieuwtjes (die uit een database komen) over Webontwikkeling. Onderdelen van deze pagina bestonden (bv. de CSS, wat HTML en een stukje client script) maar Express vult de ontbrekende data in en stuurt mooie volledige HTML/CSS/TS naar de client.

**Express hello world**

We starten met het installeren van Express.

```
npm install express
```

De Hello World applicatie:

```typescript
const express = require('express');
const app = express();
app.set('port', 3000);

app.get('/',(req:any,res:any)=>{
    res.type('text/html');
    res.send('Hello <strong>World</strong>')
});

app.listen(app.get('port'), 
    ()=>console.log( '[server] http://localhost:' + app.get('port')));
```

Start deze applicatie op met ts-node en surf via jouw browser naar localhost:3000. Nu zou je Hello World moeten zien!

Laten we elke lijn bekijken

```typescript
const express = require('express');
const app = express();
```

We importeren de express module en voeren express() uit. Het resultaat hiervan is een app object die de express applicatie voorstelt. We kunnen dit object gebruiken om een aantal settings aan te passen, te beslissen welke url welke data (html, json, etc) laadt en de applicatie te starten.

```typescript
app.set('port', 3000);
```

app.set laat ons toe bepaalde properties van onze Express applicatie aan te passen. Het is belangrijk om te definieren op welke poort onze webapplicatie gaat luisteren. Een typische keuze tijdens ontwikkeling is de poort 3000. Dit wil zeggen dat we lokaal naar http://localhost:3000 zullen moeten gaan.

Laten we nu eerst de laatste lijnen bekijken:

```typescript
app.listen(app.get('port'), 
    ()=>console.log( '[server] http://localhost:' + app.get('port')));
```

app.listen zorgt dat onze web applicatie start met luisteren op de meegegeven poort. Let op, we gebruiken in de eerste parameter app.get om de property die we daarnet een waarde hadden gegeven op te roepen. De tweede parameter is een callback die wordt uitgevoerd wanneer het luisteren succesvol is opgestart. Hier printen we gewoon de url + port uit op de console ter info.

**Express routes**

Web applicaties en websites bevatten meestal meer dan 1 "pagina". Tot nu toe zie je het path in een URL als een locatie op een webserver. Bv. localhost:3000/index.html zou de index.html zijn die zich bevindt in de root folder. localhost:3000/profile/addPicture.html zou een file addPicture.html zijn die zich in /profile/ bevindt.

Express laat ons toe zelf te bepalen welke data wordt teruggestuurd adhv het path dat gekozen wordt. In ons voorbeeld zal localhost:3000/ Hello World tonen:

```typescript
app.get('/',(req:any,res:any)=>{
    res.type('text/html');
    res.send('Hello <strong>World</strong>')
})
```

Express werkt met routes. Een route bepaalt welk path welke datat terugstuurt. Je doet dit adhv de methode app.get.

app.get heeft 2 parameters:

* het path
* een functie die de data terugstuurt naar de client

Het path hier is '/'. Dit komt overeen met localhost:3000**/**. Vervang je dit met bv '/helloworld' dan zal je naar lolalhost:3000/helloworld moeten gaan. localhost:3000 zal niet meer werken.

```typescript
app.get('/helloworld',(req:any,res:any)=>{
    res.type('text/html');
    res.send('Hello <strong>World</strong>')
})
```

De functie als tweede parameter verwacht zelf 2 parameters:

* het request object&#x20;
* het response object

Het request object bevat informatie over de vraag van de client (bv. data die de client stuurt, meer hierover later). Het response object laat ons toe een response te sturen naar de client. We gebruiken hier 2 functies:

```typescript
res.type('text/html');
```

type() laat ons toe het Content-type van de response te bepalen. Een volledige lijst van types vind je [hier](https://www.iana.org/assignments/media-types/media-types.xhtml). De belangrijkste die we gaan gebruiken zijn 'text/html' en 'application/json'.

```typescript
res.send('Hello <strong>World</strong>')
```

Om data terug te sturen gebruiken we de send() functie. Omdat we HTML willen terugsturen, vullen we de parameter met een string in HTML formaat.

**Multiple routes**

Verschillende routes toevoegen is makkelijk:

```typescript
app.get('/',(req:any,res:any)=>{
    res.type('text/html');
    res.send('Yet another hello world app...')
})
app.get('/helloworld',(req:any,res:any)=>{
    res.type('text/html');
    res.send('Hello World')
})
app.get('/goodbye',(req:any,res:any)=>{
    res.type('text/html');
    res.send('Later <strong>World</strong>')
})
```

Voor elke route roepen we app.get op met het path dat we willen instellen en de data die we willen terugsturen.

We kunnen ook verkeerde paths opvangen. Als de gebruiker naar een path gaat dat niet bestaat, kunnen we ze bv. een foutmelding geven.

```typescript
app.use((req:any, res:any) => {
    res.type('text/html');
    res.status(404);
    res.send('404 - Not Found');
    }
);
```

Merk op dat we een nieuwe lijn hebben toegevoegd:

```javascript
res.status(404);
```

Dit geeft een custom status code terug. 404 laat jouw browser weten dat de pagina niet gevonden werd. Standaard zal 200 worden teruggegeven, als alles ok is (en als je dus zelf geen status meegeeft).

{% hint style="danger" %}
Opgelet: De volgorde is hier belangrijk. Zet je deze app.use bovenaan in de applicatie, dan zal geen enkele route meer werken. Plaats die onderaan (maar boven app.listen).
{% endhint %}

**Een simpele API**

Tot nu toe stuurden we html terug. Maar we kunnen ook data terugsturen. Dit verandert onze web applicatie in een echte API.

```javascript
const express = require('express');
const app = express();
app.set('port', 3000);

const data = [
    {   
        name: 'george',
        age: 50
    },
    {   
        name: 'jane',
        age: 32
    },
    {   
        name: 'john',
        age: 42
    },
];

app.get('/getData',(req:any,res:any)=>{
    res.type('application/json');
    res.json(data);
})


app.listen(app.get('port'), ()=>console.log( '[server] http://localhost:' + app.get('port')));
```

We hebben een variabele data aangemaakt die een array van objecten bevat. Om deze data te sturen gebruiken we een ander type: application/json.

```javascript
res.type('application/json');
```

Dit zorgt ervoor dat de client weet dat het om json gaat. De Content-type in de header zal dan ook 'application/json' zijn.

```javascript
res.json(data);
```

Om de JSON data terug te sturen, gebruiken we res.json.&#x20;

{% hint style="info" %}
Eigenlijk moeten we het type hier niet definieren. res.json zal zelf de content-type van de header aanpassen naar 'application/json'.
{% endhint %}
