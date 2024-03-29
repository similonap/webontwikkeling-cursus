# Testing

## Unit testen

### In een simpele applicatie

Breid de voorbeeldcode rond Jest uit. Voorzie een test om na te gaan dat je geen antwoord krijgt op een POST- request op de reeds voorziene route. Voorzie ook een test om na te gaan dat je geen route kan opvragen die niet bestaat.

### In de Pokémonapplicatie

{% hint style="info" %}
Omwille van onze applicatie-opbouw zijn de unit testen nog niet zo "unit" als ze zouden kunnen zijn. We hebben namelijk niet veel onderscheid gemaakt tussen de "controllers" en het "domein".
{% endhint %}

#### Voorbereiding

Splits je code eerst, zodat `app.listen` niet in dezelfde file gebeurt waarin je je routes definieert.&#x20;

Omdat we tijdens de Jest-tests de initialisatie niet meer doen, moet je je code aanpassen zodat de initiële lijst met spelers en met Pokémon door de tests ingesteld kan worden. Dit kan je doen op een gelijkaardige manier als in de uitleg over het mocken van de database, met functies `getPlayers`, `setPlayers`, `getAllPokemon` en `setAllPokemon`. Zet hierbij de lijsten met alle spelers / Pokémon samen in één file met deze getters en setters. Laat je leiden door de TypeScript compiler.

Pas ook je code voor app.listen aan zodat ze ook deze methodes gebruikt. Gebruik `beforeEach` om te zorgen dat je Jest-testen mogen veronderstellen dat er spelers en Pokémon zijn. Je hoeft niet alle 151 Pokémon te gebruiken, dat levert geen toegevoegde waarde. Let wel op dat de ingestelde spelers alleen Pokémon gebruiken die voorkomen in de beperkte lijst.

#### Weergave formulieren

Controleer dat de pagina `/players` inderdaad een formulier toont waarmee je kan inschrijven en een formulier waarmee je kan aanmelden.

#### Aanmaak spelers (eerste stap)

Controleer dat een oproep van createPlayer de nieuwe speler registreert in de lokale lijst met spelers. Hoe je een formulier invult, vind je terug[ in de supertest documentatie](https://www.npmjs.com/package/supertest).

#### Aanmaak spelers (tweede stap)

Controleer dat de nieuwe speler ook verschijnt in de database. Dit vereist dat je de database client mockt en nagaat dat `insertOne` is uitgevoerd met de juiste data.

#### Bewaren speler (JWT)

Test dat het bewaren van een speler zorgt voor de juiste oproep van `update` in MongoDB. Doe dit met de versie van je programma die de speler uit een JWT haalt. Je kan een JWT aanmaken via deze [website](https://jwt.io/).

#### Logout met ongeldig token

Test dat een eventueel opgeslagen JWT wordt geschrapt als het niet geverifieerd kan worden. Je kan bijvoorbeeld een JWT ondertekenen met een ander geheim dan hetgeen je voor de applicatie gebruikt.

#### Aanpassen team (JWT)

Test dat, als je een Pokémon toevoegt aan je team, deze ook zichtbaar is in je JWT. Test eveneens voor het verwijderen van een Pokémon.

Je zal hiervoor je JWT moeten decoderen. Dat kan je doen door `Buffer.from(base64Text,'base64').toString()` op te roepen. Hierbij vervang je `base64Text` door de tekst die je wil decoderen. Hier zal dat de payload van je JWT zijn. Je kan eventueel de resulterende tekst omzetten naar een object via `JSON.parse`.

## End-to-end testen

Schrijf een uitgebreide end-to-end test voor de Pokédex applicatie (na integratie van het loginsysteem) met Selenium. Dit doe in een aparte file, `end_to_end_test.ts`. Je moet ook eerst de applicatie op de normale manier opstarten (zodat `app.listen` plaatsvindt).

{% hint style="info" %}
Het maakt eigenlijk niet uit of je JWT of sessions gebruikt, de gebruiker doet in beide gevallen hetzelfde, dus een end-to-end test zou hier niet naar mogen kijken.
{% endhint %}

Hier zorg je eerst dat de database met spelers is leeggemaakt. Die met alle Pokémon mag blijven staan.

Daarna laat je een browser (naar keuze) starten en volgende stappen doorlopen:

* navigeren naar de indexpagina
* een nieuwe user aanmaken
* inloggen als die nieuwe user
* 8 Pokémon naar keuze aanklikken om in het team te plaatsen
* controleren dat de 6 recentste Pokémon er staan
* naar de SAVE knop in het menu gaan en er op klikken
* uitloggen (hiervoor dient de url `/forgetme`)
* terug inloggen
* controleren dat dezelfde 6 Pokémon er nog steeds staan
