# Express

## Connectie opzetten

Er zijn twee strategieën om de connectie met de database op te zetten en af te sluiten:

* Je kan de connectie opzetten bij het opstarten van de applicatie en deze open laten staan tot de applicatie afgesloten wordt.
* Je kan de connectie opzetten bij het uitvoeren van een request en deze afsluiten wanneer de request afgehandeld is.

Beide hebben hun voor- en nadelen. Bij de eerste strategie is de connectie altijd open en kan je deze dus altijd gebruiken. Bij de tweede strategie is de connectie enkel open wanneer je deze nodig hebt. Dit is beter voor de performantie van je applicatie, maar je moet wel telkens de connectie opzetten en afsluiten.

### Connectie openen bij het opstarten van de applicatie

In dit voorbeeld maken we gebruik van de eerste strategie. We maken een connectie met de database bij het opstarten van de applicatie en sluiten deze pas af wanneer de applicatie afgesloten wordt.

```typescript
const connect = async () => {
    try {
        await client.connect();
        console.log('Connected to database');
    } catch (error) {
        console.error(error);
    }
}

app.listen(3000, async () => {
    await connect();
    console.log('Server started');
});
```

We moeten nu enkel nog de connectie afsluiten wanneer de applicatie afgesloten wordt. Dit doen we met de volgende code:

```typescript
const exit = async () => {
    try {
        await client.close();
        console.log('Disconnected from database');
    } catch (error) {
        console.error(error);
    }
    process.exit(0);
}

const connect = async () => {
    try {
        await client.connect();
        console.log('Connected to database');
        process.on('SIGINT', exit);
    } catch (error) {
        console.error(error);
    }
}


```

Deze code zorgt ervoor dat wanneer de applicatie afgesloten wordt, de connectie met de database ook afgesloten wordt. Dit is belangrijk omdat je anders een connectie open laat staan die niet meer gebruikt wordt. Dit kan voor problemen zorgen.

### Connectie openen bij het uitvoeren van een request

In dit voorbeeld maken we gebruik van de tweede strategie. We maken een connectie met de database wanneer we een request uitvoeren en sluiten deze af wanneer de request afgehandeld is.

```typescript
app.get('/pokemon', async (req, res) => {
    try {
        await client.connect();
        const cursor = client.db('Les').collection('pokemon').find<Pokemon>({});
        const result = await cursor.toArray();
        res.json(result);
    } catch (error) {
        console.error(error);
    } finally {
        await client.close();
    }
});
```
