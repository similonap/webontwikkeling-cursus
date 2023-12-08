# Error handling middleware

### Niet-bestaande pagina's

Wanneer de gebruiker naar een route surft die niet gedefinieerd is, wordt normaal een 404 teruggestuurd. Een manier om meer controle te krijgen over dit gedrag is om **na alle routes** volgende code toe te voegen:

```typescript
app.use((req: Request, res: Response) => {
    res.status(404);
    res.send("Pagina kon niet gevonden worden.");
});
```

Dit is eigenlijk een "catch-all" handler. Hij werkt voor alles. Daarom mag hij pas na de andere handlers gedefinieerd worden, anders onderschept hij meteen elk request en krijg je altijd deze boodschap.

### Fouten (in asynchrone code)

Fouten in synchrone handlers worden door Express zelf afgehandeld. Je ziet een error stack in de terminal, maar de applicatie blijft gewoon actief. Je kan uiteraard nog steeds gebruik maken van `try` en `catch` om fouten te voorkomen, maar als er zich toch een probleem voordoet, blijft de applicatie overeind.

Bij fouten in asynchrone code (niet noodzakelijk met `async`, het kan ook dat je expliciet een `Promise` teruggeeft!) is dit anders. Deze kunnen de applicatie laten crashen. Je kan nog steeds gebruik maken van `catch` (zowel het block als de methode op `Promises`), maar je voegt best een vorm van error handling toe.

Dit kan als volgt. Zet achteraan in je code dit:

```typescript
app.use((err: Error, req: Request, res: Response, next: NextFunction) => {
    console.error(err);
    res.status(500).send({ errors: [{ message: "Something went wrong" }] });
});
```

Op zich is dit niet genoeg. Deze handler wordt niet vanzelf geactiveerd in geval van een fout. Voeg daarom ook volgende functie toe en wrap elke asynchrone handler hierin:

```typescript
function asyncHandler(fn: (req: Request, res: Response, next: NextFunction) => Promise<any>): RequestHandler {
    return (req, res, next) => {
        fn(req, res, next).catch(next);
    };
}
```

Dit werkt als volgt: `next` stelt de volgende handler voor die toegepast kan worden. `fn(req,res,next)` geeft (dit staat in de signatuur) een `Promise` terug. Op een `Promise` kunnen we `catch` oproepen om een eventuele fout af te handelen. De objecten voor de request en response zijn al "ingebouwd" in een `NextFunction`. We hoeven ze dus niet mee te geven. De 404-handler is geen error-handling middleware, dus die zal hier niet activeren.

{% hint style="info" %}
In Express 5 zal dit veranderen. Daar zal gelijkaardig gedrag vanzelf voorzien zijn.
{% endhint %}
