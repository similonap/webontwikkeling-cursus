# Extra oefeningen

## Oefening: Unieke waarden

Je begint met de volgende code:

```
let food : string[] = ["icecream", "cheese","icecream","apple","pear","chocolate","milk"];
```

* Gebruik `filter` om uit deze array de dubbele waarden uit te halen.
* Gebruik `reduce` om uit deze array de dubbele waarden uit te halen.
* Gebruik in plaats van `filter` de `reduce` functie om alle food elementen met lengte 4 te filteren.
* Gebruik `reduce` om het aantal keer een bepaalde waarde voorkomt in de array te tellen. De output moet er zo uit zien:

```
{ icecream: 2, cheese: 1, apple: 1, pear: 1, chocolate: 1, milk: 1 }
```

* Maak gebruik van de reduce functie (of meerdere) om de alle gebruikte letters uit de food array te tonen op het scherm.\
  \
  Wat voorbeelden:

```
// let food : string[] = ["icecream", "cheese","icecream","apple","pear","chocolate","milk"];
acehiklmoprst

//let food : string[] = ["pas","sap"];
aps

//let food : string[] = ["pas","sap","bar","rap","paas"];
abprs
```

## Oefening: Muziekanalyse

In deze oefening ga je werken met een dataset van liedjes. Je gaat verschillende bewerkingen uitvoeren om inzicht te krijgen in de gegevens van deze dataset. Gebruik de gegeven `Song` interface en `songs` array om de volgende taken uit te voeren:

```javascript
export interface Song {
  id: number;
  name: string;
  album: string;
  duration: number;
  artist: string;
  genre: string;
  image: string;
}
```

Je kan het volgende json bestand gebruiken voor voorbeeld data:

{% file src="../../.gitbook/assets/songs.json" %}

Voor sommige opdrachten heb je extra interfaces nodig. Hier zijn de interfaces die je nodig hebt:

```javascript
interface SongByGenre {
  genre: string;
  songs: string[];
}

interface SongsPerArtist {
  [key: string]: number;
}
```

1. **Korte liedjes**: Filter de liedjes met een duur van 200 seconden of korter en log ze in de console. Gebruik hiervoor de `filter` functie.
2. **Unieke genres**: Geef een lijst van unieke genres in de dataset en log ze in de console. Maak gebruik van de `map` en `filter` functies om dit te bereiken.
3. **Unieke albums**: Geef een lijst van unieke albums in de dataset en log ze in de console. Pas de `map` en `filter` functies toe om dit doel te bereiken.
4. **Unieke artiesten**: Geef een lijst van unieke artiesten in de dataset en log ze in de console. Gebruik de `map` en `filter` functies om dit resultaat te verkrijgen.
5. **Totale duur**: Bereken de totale duur van alle liedjes in de dataset en log het resultaat in de console. De `reduce` functie kan je hierbij helpen.
6. **Liedjes per genre**: Groepeer de liedjes per genre en log het resultaat in de console. Om dit te doen, kun je de `map` en `filter` functies toepassen.
7. **Liedjes per genre (met reduce)**: Gebruik de `reduce` functie om de liedjes per genre te groeperen en log het resultaat in de console. Begin met een geschikt startobject in de `reduce` functie. Maak gebruik van de `SongByGenre` interface.
8. **Aantal liedjes per artiest**: Bereken het aantal liedjes per artiest en log het resultaat in de console. Maak hiervoor gebruik van de `reduce` functie en de `SongsPerArtist` interface.
9. **Gemiddelde liedjeslengte**: Bereken de gemiddelde lengte van alle liedjes in de dataset en log het afgeronde resultaat in de console. Gebruik de `reduce` functie om de totale lengte te berekenen en deel het resultaat door het aantal liedjes.
10. **Liedjes gesorteerd op lengte**: Sorteer de liedjes op lengte, van kortste naar langste, en log het resultaat in de console. Dit kan worden bereikt met de `sort` functie.
11. **Artiesten gesorteerd op aantal liedjes**: Sorteer de artiesten op het aantal liedjes, in aflopende volgorde, en log het resultaat in de console. Gebruik de `sort` functie en maak gebruik van de eerder berekende data.

## Oefening: Music Search

Deze applicatie gebruikt dezelfde dataset als de `Muziekanalyse` oefening.

Bij deze applicatie begin je met een bestaande express applicatie. Zorg eerst goed dat je de applicatie begrijpt.&#x20;

{% file src="../../.gitbook/assets/search.zip" %}



De applicatie bestaat uit een zoekveld en een lijst van songs. De songs worden opgehaald uit een json bestand. De applicatie is nog niet volledig functioneel. De bedoeling is dat je de applicatie verder afwerkt.

De GET route `/` aanvaard drie query parameters:

* `q`: de zoekstring. Als deze parameter niet aanwezig is, dan worden alle songs getoond. Als de parameter wel aanwezig is, dan worden enkel de songs getoond waarvan de naam, artiest, album of genre de zoekstring bevat.
* `sortDirection`: de sorteerrichting. Als deze parameter niet aanwezig is, dan worden de songs gesorteerd op naam in oplopende richting. Als de parameter wel aanwezig is, dan worden de songs gesorteerd op het veld dat gespecifieerd is in de `sortField` parameter. De sorteerrichting wordt bepaald door deze parameter. De mogelijke waarden zijn `asc` en `desc`.
* `sortField`: het veld waarop gesorteerd wordt. Als deze parameter niet aanwezig is, dan worden de songs gesorteerd op naam. Als de parameter wel aanwezig is, dan worden de songs gesorteerd op het veld dat gespecifieerd is in deze parameter. De mogelijke waarden zijn `name` en `duration`.

Je mag in deze opgave geen gebruik maken van for loops. Je moet dus gebruik maken van de array methodes `filter`, `indexOf`, `map`, `reduce` en `sort`.

Bij het opstarten van de express applicatie zal je het volgende zien:

![](<../../.gitbook/assets/Screenshot 2023-05-06 at 17.22.19.png>)

Uiteindelijk zal de applicatie er als volgt uitzien:

<figure><img src="../../.gitbook/assets/Screenshot 2023-05-06 at 17.25.47.png" alt=""><figcaption></figcaption></figure>

