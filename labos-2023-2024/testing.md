# Testing

### Unit testen



### Uitgebreide test flow

Schrijf een uitgebreide end-to-end test voor de Pokédex applicatie (na integratie van het loginsysteem) met Selenium. Dit doe je niet in dezelfde file, maar in een aparte file, end\_to\_end\_test.ts.

Hier zorg je eerst dat de database met spelers is leeggemaakt. Die met alle Pokémon mag blijven staan.

Daarna laat je een browser (naar keuze) starten en volgende stappen doorlopen:

* navigeren naar de indexpagina
* een nieuwe user aanmaken
* inloggen als die nieuwe user
* 8 Pokémon naar keuze aanklikken om in het team te plaatsen
* controleren dat de 6 recentste Pokémon er staan
* uitloggen
* terug inloggen
* controleren dat dezelfde 6 Pokémon er nog steeds staan
