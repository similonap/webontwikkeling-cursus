# MySQL Connector

### MySql2

De MySQL2 library is een npm module die het mogelijk maakt om verbinding te maken met een MySQL database. Deze maakt het mogelijk om queries te gaan uitvoeren vanuit node.js code. We werken dus niet meer rechstreeks met een client zoals MySQL Workbench of phpMyAdmin. We gaan de queries uitvoeren vanuit node.js code.

#### Installatie

Om de MySQL2 module te installeren voeren we de volgende commando uit in de terminal:

```bash
npm install mysql2
```

#### Database connectie

Om een verbinding te maken met een database maken we gebruik van de `createConnection` functie. Deze functie heeft als argumenten een object met de volgende properties:

* `host`: De hostnaam van de database server.
* `user`: De gebruikers naam van de database.
* `password`: Het wachtwoord van de database.
* `database`: De naam van de database.

Je kan `mysql2` synchroon of asynchroon gebruiken. In het eerste geval gebruik je deze regel:

```typescript
import mysql2 from 'mysql';
```

Als we de asynchrone versie nemen, kunnen we gebruik maken van de `async/await` syntax.

```typescript
import mysql2 from 'mysql2/promise';
```

{% hint style="info" %}
Als je beide versies nodig hebt in dezelfde applicatie, kan je gewoonweg een andere naam gebruiken voor het woordje `from`. Bijvoorbeeld import `mysql2sync` en `import mysql2async`.
{% endhint %}

Omdat we hier willen gebruik maken van async/await moeten we de functie waar deze gebruikt wordt ook async maken. We maken hier een asynchrone functie aan met de naam `main` en roepen deze functie aan het einde van het bestand aan. Hier gaan we de database connectie maken.

```typescript
async function main() {
    try {
        const connection = await mysql2.createConnection({
            host: 'localhost',
            user: 'user',
            password: 'password',
            database: 'tutorial'});
        console.log("Connected!");
        connection.end();
    } catch (error) {
        console.log(error);
    }
}
main();
```

Merk hier op dat we de code in een `try/catch` blok zetten. Dit doen we omdat we hiermee de fouten kunnen opvangen die op kunnen treden. In het `catch` blok loggen we de error naar de console. Als je bijvoorbeeld geen verbinding kunt maken omdat je een foutieve gebruikersnaam of wachtwoord hebt ingevuld dan zal de error hier worden opgevangen.

Momenteel sluiten we direct de connectie na het maken van de connectie. Dit doen we omdat we nu nog geen queries uitvoeren. Als we queries uitvoeren dan willen we de connectie open houden totdat we klaar zijn met de query.

