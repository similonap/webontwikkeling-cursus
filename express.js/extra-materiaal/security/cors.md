# CORS

## CORS

### Wat is CORS?

CORS staat voor Cross-Origin Resource Sharing. Het is een mechanisme dat gebruikt wordt om toegang te geven tot resources op een andere domein. Dit is een veiligheidsmechanisme dat ervoor zorgt dat een website niet zomaar toegang krijgt tot resources op een andere website. Dit is een belangrijk mechanisme om te begrijpen als je met API's gaat werken. Dit concept noemen we ook wel de `Same Origin Policy`.

Bijvoorbeeld: je hebt een website op `www.example.com`. Je wil een API oproepen op `www.api.com`. Je kan dit niet zomaar doen. Je moet eerst toestemming vragen aan de server van `www.api.com`. Dit doe je door een speciale header mee te sturen met je request. De server van `www.api.com` zal dan bepalen of je toegang krijgt tot de resource.

Heb je deze toegang niet gekregen, dan zal de server een foutmelding terugsturen. Dit is een zogenaamde `CORS error`.

### Wat wordt er bedoeld met origin?

Een origin is een combinatie van een protocol, domein en poort. Dus probeer je een request te doen van `http://localhost:3000` naar `http://localhost:3001`, dan is dit een andere origin en zal ook dit een CORS error geven. Voor te voldoen aan de `Same Origin Policy` moet je dus dezelfde protocol, domein en poort gebruiken.

### Een voorbeeld

Stel je hebt de volgende express backend lopen op poort 3000:

```typescript
import express from "express";

const app = express();

app.set("port", 3000);

app.get("/", (req, res) => {
  res.type("text/html");
  res.send("Hello <strong>World</strong>");
});

app.listen(app.get("port"), () =>
  console.log("[server] http://localhost:" + app.get("port"))
);
```

En je hebt een frontend applicatie op poort 3001. Je kan hiervoor een simpele express server opzetten met static files:

```typescript
import express from "express";

const app = express();

app.set("port", 3001);

app.use(express.static("public"));

app.listen(app.get("port"), () =>
  console.log("[client] http://localhost:" + app.get("port"))
);
```

Je kan nu een HTML pagina maken in de `public` folder:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CORS</title>
  </head>
  <body>
    <h1>CORS</h1>
    <button id="btn">Load data</button>
    <div id="data"></div>
    <script>
      const btn = document.getElementById("btn");
      const data = document.getElementById("data");

      btn.addEventListener("click", () => {
        fetch("http://localhost:3000")
          .then((response) => response.text())
          .then((text) => (data.innerHTML = text));
      });
    </script>
  </body>
</html>
```

Deze code zal een request doen naar de backend op poort 3000. Als je nu op de knop klikt, zal je een CORS error krijgen:

<figure><img src="../../../.gitbook/assets/Screenshot%202023-03-08%20at%2013.35.35.png" alt=""><figcaption></figcaption></figure>

Er zal dus een aanpassing nodig zijn in de backend om dit toch te laten werken.

### CORS in Express

Om CORS te gebruiken in Express, moeten we een middleware toevoegen. Dit is een functie die wordt uitgevoerd voor elke request die binnenkomt. Hier kunnen we er voor zorgen dat de juiste headers worden toegevoegd aan de response.

We moeten deze eerst installeren:

```typescript
npm install cors
```

We kunnen deze dan toevoegen aan onze applicatie:

```typescript
import cors from "cors";

app.use(cors());
```

Als je nu opnieuw op de knop klikt, zal je de data van de backend zien verschijnen. Als je in detail gaat kijken naar het netwerkverkeer, zal je zien dat er een extra header is toegevoegd aan de response:

```
Access-Control-Allow-Origin: *
```

<figure><img src="../../../.gitbook/assets/Screenshot%202023-03-08%20at%2013.43.32.png" alt=""><figcaption></figcaption></figure>

Als je gewoon `cors()` aanroept zonder parameters, zal elke request van eender welke website toegang krijgen tot je API. Dit is niet altijd de bedoeling. Je kan ook een lijst van domeinen meegeven die toegang krijgen tot je API.

```typescript
app.use(cors({
    origin: ["http://localhost:3000", "http://localhost:3001"]
}));
```

Nu zal je enkel toegang krijgen tot je API als je vanaf een van deze domeinen een request doet. De header zal er dan als volgt uitzien:

```
Access-Control-Allow-Origin: http://localhost:3001
```

### CORS Proxy

Soms komt het voor dat je een API wil oproepen van een andere website, maar dat je geen controle hebt over de backend. In dat geval kan je een zogenaamde CORS proxy gebruiken. Dit is een server die de request doorstuurt naar de API en de response terugstuurt naar de client. Deze server heb je zelf in de hand, dus je kan zelf bepalen welke headers er worden toegevoegd aan de response.

Je zou zelf een dergelijke CORS proxy kunnen schrijven in express die gewoon de request doorstuurt naar de API en de response terugstuurt naar de client.

```typescript
app.get("/api", (req, res) => {
  fetch("https://api.example.com")
    .then((response) => response.text())
    .then((text) => res.send(text));
});
```

Er bestaan ook al bestaande CORS proxies die je kan gebruiken. Een bekende is [CORS Anywhere](https://github.com/Rob--W/cors-anywhere)
