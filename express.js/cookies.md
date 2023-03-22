# Cookies

## Cookies

### HTTP is stateless

HTTP is een stateless protocol. Dit betekent dat de server in principe geen informatie over de client bijhoudt. Als je een webpagina bezoekt, zal de server niet weten of je daarvoor al eens op die pagina bent geweest. Dit is een groot probleem, want hoe kan de server dan bijhouden dat je ingelogd bent? Of dat je een bepaalde product in je winkelmandje hebt gelegd?

Om dit probleem op te lossen, gebruiken we cookies. Een cookie is een klein stukje informatie dat de server naar de client stuurt. De client slaat deze informatie op en stuurt deze informatie bij elke volgende request naar de server. Op die manier kan de server bijhouden welke client welke informatie heeft.

### Cookies in Express

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

### Cookie aanmaken

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

### Cookie verwijderen

Om een cookie te verwijderen, gebruiken we de `res.clearCookie()` functie. Deze functie heeft één parameter: de naam van de cookie die we willen verwijderen.

```typescript
res.clearCookie('name');
```

### Cookie opties

De `res.cookie()` functie heeft nog een aantal opties. Hier een overzicht van de belangrijkste opties die we later nog nodig zullen hebben:

* `maxAge`: de levensduur van de cookie in milliseconden. Als deze optie niet wordt meegegeven, dan wordt de cookie verwijderd wanneer de browser wordt afgesloten.
* `httpOnly`: als deze optie `true` is, dan kan de cookie niet worden gelezen door JavaScript. Dit is een veiligheidsmaatregel om cross-site scripting aanvallen te voorkomen.
