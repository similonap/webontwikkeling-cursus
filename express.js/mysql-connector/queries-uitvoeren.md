# Queries uitvoeren

Om queries uit te voeren maken we gebruik van het `connection` object. We maken hier gebruik van de `execute` functie waar we de query meegeven als argument. Deze functie geeft een array terug met twee elementen. Het eerste element is een array met de resultaten van de query. Het tweede element is een array met metadata over de query. We gaan hier alleen gebruik maken van het eerste element.

### Select met meerdere resultaten

Als je bijvoorbeeld een query uitvoeren om alle gebruikers van een `Users` tabel op te halen dan zou je de volgende code kunnen gebruiken:

```typescript
const [rows_users] = await connection.execute('SELECT * FROM `users`');

console.log(rows_users);
// [
//   { id: 1, name: 'Jon', email: 'john@example.com' },
//   { id: 2, name: 'Paul', email: 'paul@example.com' },
//   { id: 3, name: 'Mary', email: 'mary@example.com' }
// ]
```

Je krijgt hier een array terug met resultaten van de query. Dit object is van het type `RowDataPacket`. Wil je voor dit object autocomplete functionaliteit hebben en static typing dan moet je voor het resultaten object een interface aanmaken die `RowDataPacket` specialiseert.

```typescript
interface User extends RowDataPacket {
    id: number;
    name: string;
    email: string;
}
```

Je gebruikt dan de Diamond Operator om aan te geven dat je een array wilt met objecten van het type `User`. Het resultaat zal dan het type `User[]` hebben.

```typescript
// Query all rows from the users table
const [rows_users] = await connection.execute<User[]>('SELECT * FROM `users`');

console.log(rows_users);
```

Wil je een specifieke gebruiker opvragen dan kun je een `WHERE` clause gebruiken. In dit voorbeeld gaan we de gebruiker opvragen met de id 1.

```typescript
const [rows_user] = await connection.execute<User[]>('SELECT * FROM `users` WHERE `id` = 1');
```

Ook al krijg je hier maar 1 rij terug zal het resultaat een array zijn. Dit komt omdat de `execute` functie altijd een array terug geeft. Je zal dus zelf de eerste rij uit de array moeten halen omdat hij niet op voorhand weet of je 1 of meerdere rijen terug krijgt.

```typescript
const [rows_user] = await connection.execute<User[]>('SELECT * FROM `users` WHERE `id` = 1');
const user = rows_user[0]
```
