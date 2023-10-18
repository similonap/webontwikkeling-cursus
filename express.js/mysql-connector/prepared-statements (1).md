# prepared statements

#### Prepared statements

Als je een query uitvoert met een `WHERE` clause dan is het mogelijk dat je een SQL injection aanval krijgt. Dit is een aanval waarbij een gebruiker een query kan uitvoeren die niet de bedoeling is. Om dit te voorkomen kun je gebruik maken van prepared statements. Dit zijn statements waarbij je de variabelen in de query vervangt door een placeholder. Deze placeholders worden vervolgens vervangen door de variabelen die je meegeeft aan de `execute` functie.

```typescript
const [rows_user] = await connection.execute<User[]>('SELECT * FROM `users` WHERE `id` = ?', [1]);
```

In dit voorbeeld hebben we de `id` variabele vervangen door een `?` placeholder. Deze placeholder wordt vervangen door de eerste variabele in de array die we meegeven aan de `execute` functie. Gebruik je meerdere placeholders dan moet je meerdere variabelen meegeven aan de `execute` functie.

Gebruik altijd prepared statements als je een `WHERE` clause gebruikt. Dit voorkomt SQL injection aanvallen.

#### Insert

Als je een insert query wilt uitvoeren dan kun je de `execute` functie ook gebruiken. Je moet dan wel de `INSERT` query gebruiken.

```typescript
const [result] = await connection.execute<OkPacket>('INSERT INTO `users` (`name`, `email`) VALUES (?, ?)', ['Andie Similon', 'andie.similon@ap.be']);
console.log(result.insertId);
```

De `result` variabele is van het type `OkPacket`. Dit is een object dat de metadata van de query bevat. In dit geval bevat het object de `insertId` van de nieuwe rij. Je weet dan welke id de nieuwe rij heeft gekregen.

#### Update

Op dezelfde manier kun je ook een update query uitvoeren.

```typescript
const [result_update] = await connection.execute<OkPacket>('UPDATE `users` SET `name` = ? WHERE `id` = ?', ['Jon', 1]);
console.log(result_update.affectedRows);
```

Om te zien hoeveel rijen zijn aangepast kun je de `affectedRows` property gebruiken.

#### Delete

Een delete query werkt op dezelfde manier als een update query. Willen we bijvoorbeeld de gebruiker met de id 1 verwijderen dan kunnen we de volgende code gebruiken.

```typescript
const [result_delete] = await connection.execute<OkPacket>('DELETE FROM `users` WHERE `id` = ?', [1]);
console.log(result_delete.affectedRows);
```

#### Stored procedures

Als je een stored procedure wilt uitvoeren dan kun je de `execute` functie ook gebruiken. Je moet dan wel de `CALL` query gebruiken. Wil je hiervoor geen interface voor aanmaken kan je ook altijd de `RowDataPacket` gebruiken. Dit werkt ook voor andere queries.

```typescript
const [[rows_likes]] = await connection.execute<RowDataPacket[]>('CALL get_likes_for_post(?)', [1]);
console.log(rows_likes[0].likes);
```
