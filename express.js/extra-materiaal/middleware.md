# Middleware

Middleware is een functie die toegang heeft tot de request en response objecten. Middleware kan de request en response objecten aanpassen, of de request doorsturen naar de volgende middleware functie in de stack. Je kan dus bijvoorbeeld een functie schrijven die wordt uitgevoerd voordat de request naar de route wordt gestuurd. 

Je hebt al een aantal keer middleware gebruikt. Telkens je de `app.use()` functie gebruikt, voeg je middleware toe aan de stack. Je hebt bijvoorbeeld de `express.static()` functie gebruikt om statische bestanden te serveren. Deze functie is een middleware functie.

## Eigen middleware functie
### Logging voorbeeld

Wil je bijvoorbeeld een functie schrijven die een request logt voor elke request die binnenkomt? Dan kan je de volgende functie schrijven:

```typescript
app.use((req, res, next) => {
    console.log(`${req.method} ${req.path}`);
    next();
});

app.get("/", (req, res) => {
    res.render("index");
})
```

Vergeet niet om de `next()` functie aan te roepen. Anders zal de request niet naar de volgende middleware functie in de stack gaan en zal deze request ook niet naar de route gaan.

### Locals voorbeeld

Soms is het handig om bepaalde variabelen beschikbaar te maken in alle views. Je kan deze variabelen toevoegen aan de `res.locals` object. Deze variabelen zijn dan beschikbaar in alle views. Zo moet je niet elke keer dezelfde variabelen doorgeven aan de `render()` functie. Je moet deze dan wel toevoegen aan de `res.locals` object in een middleware functie.

```typescript
app.use((req, res, next) => {
    res.locals.title = "My website";
    next();
});

app.get("/", (req, res) => {
    res.render("index");
})
```

Je kan nu in de `index.ejs` view de `title` variabele gebruiken zonder deze mee te geven aan de render functie.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><%= title %></title>
</head>
<body>
    <h1><%= title %></h1>
</body>
</html>
```

Je zou eventueel ook een `user` object kunnen toevoegen aan de `res.locals` object. Zo kan je in alle views de `user` variabele gebruiken. Je kan deze variabele dan bijvoorbeeld gebruiken om te bepalen of de gebruiker is ingelogd of niet.

