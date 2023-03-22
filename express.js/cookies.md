# Cookies

## HTTP is stateless

HTTP is een stateless protocol. Dit betekent dat de server in principe geen informatie over de client bijhoudt. Als je een webpagina bezoekt, zal de server niet weten of je daarvoor al eens op die pagina bent geweest. Dit is een groot probleem, want hoe kan de server dan bijhouden dat je ingelogd bent? Of dat je een bepaalde product in je winkelmandje hebt gelegd?

Om dit probleem op te lossen, gebruiken we cookies. Een cookie is een klein stukje informatie dat de server naar de client stuurt. De client slaat deze informatie op en stuurt deze informatie bij elke volgende request naar de server. Op die manier kan de server bijhouden welke client welke informatie heeft.

## Cookies in Express

Als we willen dat Express cookies kan gebruiken, moeten we eerst de cookie-parser middleware installeren:

```bash
npm install cookie-parser
```

Deze library heeft geen built-in typescript types, dus we moeten de types van de `cookie-parser` library installeren:

```bash
npm install --save-dev @types/cookie-parser
```

We kunnen de cookie-parser middleware dan toevoegen aan onze applicatie:

```typescript
import express from 'express';
import cookieParser from 'cookie-parser';

app.use(cookieParser());
```

## Cookie aanmaken

Om een cookie aan te maken, gebruiken we de `res.cookie()` functie. Deze functie heeft twee parameters: de naam van de cookie en de waarde van de cookie.

```typescript
res.cookie('name', 'value'});
```

Als we bijvoorbeeld willen bijhouden hoeveel keer een gebruiker een pagina heeft bezocht, kunnen we een cookie aanmaken met de naam `visitCount` en de waarde `1`. Als de gebruiker de pagina opnieuw bezoekt, kunnen we de waarde van de cookie met 1 verhogen.

```typescript
app.get('/', (req, res) => {
  let currentCount;
  if (req.cookies.visitCount) {
    currentCount = parseInt(req.cookies.visitCount) + 1
  } else {
    currentCount = 1;
  }
  res.cookie('visitCount', currentCount)
  res.send('You have visited this page ' + currentCount + ' times.');
});
```

Hoewel dat cookies zeer belangrijk zijn voor authenticatie, is het niet veilig om de waarde van een cookie te vertrouwen. Een gebruiker kan namelijk de waarde van een cookie veranderen in de browser. We zien later nog hoe we dit probleem kunnen oplossen.

## Cookie verwijderen

Om een cookie te verwijderen, gebruiken we de `res.clearCookie()` functie. Deze functie heeft één parameter: de naam van de cookie die we willen verwijderen.

```typescript
res.clearCookie('name');
```

## Cookie opties

De `res.cookie()` functie heeft nog een aantal opties. Hier een overzicht van de belangrijkste opties die we later nog nodig zullen hebben:

* `maxAge`: de levensduur van de cookie in milliseconden. Als deze optie niet wordt meegegeven, dan wordt de cookie verwijderd wanneer de browser wordt afgesloten.
* `httpOnly`: als deze optie `true` is, dan kan de cookie niet worden gelezen door JavaScript. Dit is een veiligheidsmaatregel om cross-site scripting aanvallen te voorkomen.
* `secure`: als deze optie `true` is, dan wordt de cookie alleen verstuurd via een beveiligde verbinding (HTTPS). Dit is een veiligheidsmaatregel om cross-site scripting aanvallen te voorkomen.

Je kan deze opties meegeven als een object als tweede parameter van de `res.cookie()` functie:

```typescript
res.cookie('name', 'value', { maxAge: 900000, httpOnly: true });
```

## Andere datatypes

De waarde van een cookie moet een string zijn. Als je een andere datatype wil opslaan in een cookie, dan moet je deze eerst omzetten naar een string. Dit kan je doen met de `JSON.stringify()` functie:

```typescript
const data = { name: 'John', age: 30 };

res.cookie('data', JSON.stringify(data));
```

Om deze data weer terug te krijgen, moet je de `JSON.parse()` functie gebruiken:

```typescript
const data = JSON.parse(req.cookies.data);
```

## Cookies in de browser

Als we een cookie aanmaken, dan wordt deze opgeslagen in de browser. We kunnen de cookies bekijken door naar de developer tools te gaan en naar de `Application` tab te gaan. Daar kunnen we de cookies bekijken die de browser heeft opgeslagen.

<figure><img src="../.gitbook/assets/Screenshot 2023-03-22 at 11.19.38.png" alt=""><figcaption></figcaption></figure>

In deze tab kan je ook je cookies aanpassen en verwijderen. Als je de waarde van een cookie aanpast, dan zal de server de nieuwe waarde zien wanneer je de pagina opnieuw laadt. Dit is een groot probleem, want de server kan niet vertrouwen op de waarde van een cookie. Plaats dus nooit gevoelige data in een cookie.

# Sessions

## Wat is een session?

Een session is een stukje informatie die de server bijhoudt over een client. Een session wordt opgeslagen op de server en wordt geïdentificeerd door een unieke sessie ID. Deze sessie ID wordt opgeslagen in een cookie op de client. Op die manier kan de server bijhouden welke client welke informatie heeft.

Het voordeel van een session is dat de server meer informatie over de client kan bijhouden. Een cookie is veel beperkter in de hoeveelheid data er kan bij gehouden worden dan een session. Nog een voordeel van een session is dat dit veiliger is dan cookies. Cookies kan je namelijk makkelijk aanpassen in de browser. De data die in een session wordt opgeslagen, kan je niet aanpassen in de browser.

## Hoe werkt een session?

Een session werkt als volgt:

* De client stuurt een request naar de server, bijvoorbeeld tijdens het inloggen.
* De server genereert een unieke sessie ID en slaat deze op in een database (of in het geheugen).
* De server stuurt een cookie naar de client met de sessie ID. Bijvoorbeeld: `connect.sid=1234567890`.
* De client stuurt de cookie (`connect.sid=1234567890`) bij elke volgende request naar de server.
* De server gebruikt de sessie ID om de juiste informatie op te halen uit de database.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

## Express sessions

### Installatie

Het is perfect mogelijk om zelf een session systeem te bouwen, maar dit is een tijdrovende klus. Gelukkig zijn er al veel libraries die dit voor ons doen. We gaan gebruik maken van de `express-session` library. We kunnen deze library installeren met de volgende commando:

```bash
npm install express-session
```

Deze library heeft geen built-in typescript types, dus we moeten de types van de `express-session` library installeren:

```bash
npm install --save-dev @types/express-session
```

### Session middleware

We kunnen de `express-session` middleware dan toevoegen aan onze applicatie:

```typescript
import express from 'express';

app.use(session({
  secret: 'keyboard cat'
}));
```

De `secret` parameter is de enige verplichte parameter. Deze parameter wordt gebruikt om de sessie ID te versleutelen. Zo kan niemand de werkelijke sessie ID achterhalen of eventueel zelf een sessie ID genereren. Deze secret moet ten alle tijden geheim blijven. De secret kan je bijvoorbeeld meegeven via een omgevingsvariabelen. 

By default zal de sessie opgeslagen worden in het geheugen. Dit is niet ideaal, want als de server herstart, dan worden alle sessies verwijderd. Dit gaan we voorlopig negeren, in een productie omgeving moet je dit wel oplossen door bijvoorbeeld de sessies op te slaan in een database. Dit doe je aan de hand van de `store` parameter.

### Session object

De `express-session` middleware voegt een `session` object toe aan de `Request` object. Dit object bevat alle informatie over de sessie. Vooraleer we de sessie kunnen gebruiken, moeten we een interface toevoegen aan het `express-session` module. Dit doen we door een `declare module` statement toe te voegen aan onze `index.ts` file:

```typescript
declare module "express-session" {
    interface Session {
      key1: string;
      key2: number;
    }
}
```

We kunnen nu de sessie gebruiken in onze applicatie:

```typescript
app.get("/", (req, res) => {
    req.session.key1 = "value1";
    req.session.key2 = 2;
    res.send("Hello world");
});
```

en we kunnen deze uitlezen in een andere route:

```typescript
app.get("/test", (req, res) => {
    res.send(req.session.key1 + " " + req.session.key2);
});
```

### Visitor counter

We hernemen nu het voorbeeld van de visitor counter. We gaan nu een session gebruiken om bij te houden hoeveel keer een gebruiker een pagina heeft bezocht. 

```typescript
import express from "express";
import cookieParser from 'cookie-parser';
import session  from 'express-session';

const app = express();
app.set("port", 3000);

app.use(session({ secret: 'keyboard cat' }))

declare module "express-session" {
    interface Session {
      visitCount: string;
    }
}

app.get("/", (req, res) => {
    let currentCount;
    if (req.session.visitCount) {
        currentCount = req.session.visitCount + 1;
    } else {
        currentCount = 1;
    }
    req.session.visitCount = currentCount;
    res.send("You have visited this page " + currentCount + " times.");
});

app.listen(app.get("port"), () => {
    console.log("Server started on port " + app.get("port"));
});
```

Deze code is bijna identiek aan de code van de visitor counter. Het enige verschil is dat we nu de sessie gebruiken om bij te houden hoe vaak een gebruiker een pagina heeft bezocht.

Als je nu gaat kijken in de developer tools zie je dat er geen cookie meer wordt opgeslagen met de `visitCount` waarde. Dit komt omdat de `visitCount` waarde niet in de cookie wordt opgeslagen, maar in de session. Je zal wel een cookie zien met de sessie ID.

