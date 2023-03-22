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

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

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

### Voorbeelden

#### Visitor counter

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
