# In een Express applicatie

We kunnen met de kennis die we nu hebben van de mysql2 en de express library nu een API gaan bouwen. We gaan een API maken die gebruikers kan aanmaken, posts kan aanmaken en likes kan geven aan posts.

```typescript
import express from 'express';
import mysql2, { OkPacket } from 'mysql2/promise';
import { User } from './types';

const app = express();
const port = 3000;

let connection: mysql2.Connection;

app.use(express.json());

app.listen(port, async () => {
    connection = await mysql2.createConnection({
        host: 'localhost',
        user: 'root',
        password: 'root',
        database: 'tutorial'
    });
    console.log(`Example app listening at http://localhost:${port}`);
});
```

Het eerste wat we doen is een express app aanmaken. We maken ook een connectie met de database. Deze connectie gebruiken we later om queries uit te voeren. Dit doen we in de `listen` functie. We doen dit omdat we willen wachten tot de app is gestart voordat we de connectie maken.

#### Get users

We gaan nu een route maken om alle gebruikers op te halen. We maken hiervoor een `GET` request naar de `/users` route.

```typescript
app.get('/users', async (req, res) => {
    const [rows] = await connection.execute<User[]>('SELECT * FROM `users`');
    res.json(rows);
});
```

Om ook een gebruiker te kunnen ophalen aan de hand van zijn id maken we een `GET` request naar de `/users/:id` route. We maken hier gebruik van een prepared statement omdat we willen voorkomen dat iemand een SQL injection aanval kan uitvoeren.

```typescript
app.get('/users/:id', async (req, res) => {
    const [rows] = await connection.execute<User[]>('SELECT * FROM `users` WHERE `id` = ?', [req.params.id]);
    res.json(rows);
});
```

#### Create user

We gaan nu een route maken om een gebruiker aan te maken. We maken hiervoor een `POST` request naar de `/users` route.

```typescript
app.post('/users', async (req, res) => {
    const [result] = await connection.execute<OkPacket>('INSERT INTO `users` (`name`, `email`) VALUES (?, ?)', [req.body.name, req.body.email]);
    const [rows] = await connection.execute<User[]>('SELECT * FROM `users` WHERE `id` = ?', [result.insertId]);
    res.json(rows[0]);
});
```

Na het aanmaken van de gebruiker willen we ook de gebruiker terugsturen. We doen dit door de gebruiker op te halen aan de hand van de `insertId` die we terugkrijgen van de `execute` functie.

#### Update user

We gaan nu een route maken om een gebruiker aan te passen. We maken hiervoor een `PUT` request naar de `/users/:id` route.

```typescript
app.put('/users/:id', async (req, res) => {
    const [result] = await connection.execute<OkPacket>('UPDATE `users` SET `name` = ? WHERE `id` = ?', [req.body.name, req.params.id]);
    if (result.affectedRows === 1) {
        const [rows] = await connection.execute<User[]>('SELECT * FROM `users` WHERE `id` = ?', [req.params.id]);
        return res.json(rows[0]);
    }
    return res.status(404).json({ message: 'User not found' });
});
```

We kijken of de gebruiker is aangepast door te kijken of er 1 rij is aangepast. We vragen vervolgens de gebruiker op aan de hand van het id. Als de gebruiker niet is gevonden sturen we een 404 terug.

#### Delete user

We gaan nu een route maken om een gebruiker te verwijderen. We maken hiervoor een `DELETE` request naar de `/users/:id` route.

```typescript
app.delete('/users/:id', async (req, res) => {
    const [result] = await connection.execute<OkPacket>('DELETE FROM `users` WHERE `id` = ?', [req.params.id]);
    if (result.affectedRows === 1) {
        return res.status(200).json({ message: 'User deleted' });
    }
    return res.status(404).json({ message: 'User not found' });
});
```

Dit is precies hetzelfde als bij het aanpassen van een gebruiker. We kijken of de gebruiker is verwijderd door te kijken of er 1 rij is verwijderd. Als dit niet het geval is dan sturen we een 404 terug. Uiteraard kunnen we de gebruiker hier niet meer ophalen omdat deze is verwijderd.

### SQL Script

Het SQL init script dat voor de code hierboven hebben gebruikt is als volgt:

```sql
CREATE DATABASE IF NOT EXISTS tutorial;
USE tutorial;

CREATE TABLE IF NOT EXISTS users (
  id INT NOT NULL AUTO_INCREMENT,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  PRIMARY KEY (id)
);

CREATE TABLE IF NOT EXISTS posts (
  id INT NOT NULL AUTO_INCREMENT,
  title VARCHAR(255) NOT NULL,
  body TEXT NOT NULL,
  user_id INT NOT NULL,
  PRIMARY KEY (id),
  FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE IF NOT EXISTS likes (
  id INT NOT NULL AUTO_INCREMENT,
  post_id INT NOT NULL,
  user_id INT NOT NULL,
  PRIMARY KEY (id),
  FOREIGN KEY (post_id) REFERENCES posts(id),
  FOREIGN KEY (user_id) REFERENCES users(id)
);

DELIMITER $$
CREATE PROCEDURE get_likes_for_post(IN post_id INT)
BEGIN
  SELECT COUNT(*) AS likes FROM likes WHERE post_id = post_id;
END$$
DELIMITER ;

INSERT INTO users (name, email) VALUES ('John', 'john@example.com');
INSERT INTO users (name, email) VALUES ('Paul', 'paul@example.com');
INSERT INTO users (name, email) VALUES ('Mary', 'mary@example.com');

INSERT INTO posts (title, body, user_id) VALUES ('John\'s Post', 'This is John\'s post', 1);
INSERT INTO posts (title, body, user_id) VALUES ('Paul\'s Post', 'This is Paul\'s post', 2);
INSERT INTO posts (title, body, user_id) VALUES ('Mary\'s Post', 'This is Mary\'s post', 3);
INSERT INTO posts (title, body, user_id) VALUES ('John\'s Second Post', 'This is John\'s second post', 1);

INSERT INTO likes (post_id, user_id) VALUES (1, 2);
INSERT INTO likes (post_id, user_id) VALUES (2, 1);
INSERT INTO likes (post_id, user_id) VALUES (3, 2);
INSERT INTO likes (post_id, user_id) VALUES (4, 3);
```
