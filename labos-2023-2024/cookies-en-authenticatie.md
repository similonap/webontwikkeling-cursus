# Cookies en authenticatie

## Client-side teller

Maak een kleine Express-applicatie die op de homepagina een knop "teller ophogen" toont. Bij deze knop staat hoe vaak de gebruiker er al op geklikt heeft. Dit aantal moet geldig blijven, ook wanneer je de applicatie stopt en herstart. Gebruik een cookie om dit te verwezenlijken.

## Onthouden trainernaam

Breid de Pokédex-applicatie uit. Wanneer de gebruiker zijn/haar naam aanklikt in de lijst met trainers, wordt het ID onthouden. Op deze manier moet het mogelijk zijn om naar `/` te surfen en automatisch op de juiste pagina terecht te komen. Doe dit ook via een cookie. Voorzie daarnaast ook een pagina `/forgetme`, zodat we eventueel als een andere trainer kunnen inloggen.

Maak een backup van deze code, want in de volgende oefening zal je ze moeten herwerken.

## Login via sessie

{% hint style="info" %}
Dit is een eerder grote vraag. Hou je applicatie goed in de gaten met `console.debug` en test na elke tussenstap.
{% endhint %}

Breid de applicatie uit met een loginsysteem. Dit vereist dat je de lijst met trainers bijhoudt in een database en dat je elke trainer een wachtwoord geeft.

Dit vereist een paar aanpassingen. Je zal moeten zorgen dat een nieuwe trainer ook een wachtwoord moet meegeven (gebruik `<input type="password">`). Je zal ook moeten zorgen dat de lijst met links vervangen wordt door een loginformulier met een veld voor de trainernaam en voor het wachtwoord.

Zorg dat de `Player` bijgehouden wordt in een sessie. Pas alle URL's aan zodat het ID van de speler geen deel uitmaakt van de URL (want die data zit toch in de sessie). Zorg er ook voor dat alle routes die enkel voor een specifieke trainer bedoeld zijn een 403-fout opleveren wanneer iemand niet is ingelogd.

{% hint style="danger" %}
Omdat de technieken rond veilige opslag van wachtwoorden in een ander vak aan bod komen, investeren we daar geen tijd in. Denk er echter aan dat je in een productieomgeving **nooit** wachtwoorden als plain text opslaat.
{% endhint %}

{% hint style="info" %}
Test achteraf uit wat gebeurt als je je applicatie herstart!
{% endhint %}

## Persistente session store

Gebruik het NPM package [connect-mongo](https://www.npmjs.com/package/connect-mongo) om je sessies te bewaren.

{% hint style="info" %}
Test achteraf uit wat gebeurt als je je applicatie herstart!
{% endhint %}

{% hint style="warning" %}
We gebruiken hier MongoDB omdat dat eenvoudig is en het principe aantoont. Het is niet vanzelf zo dat het opslagmechanisme voor je applicatiedata ook het ideale opslagmechanisme voor je sessies is. Daarvoor is een uitgebreidere analyse nodig.
{% endhint %}

## Login met JWT

{% hint style="info" %}
Dit is een eerder grote vraag. Hou je applicatie goed in de gaten met `console.debug` en test na elke tussenstap.
{% endhint %}

Gebruik een JWT-token in plaats van een sessie om dezelfde taak te vervullen. Om dit vlot te laten gaan, neem je best een backup van de versie met sessies en verwijder je dan de uitbreiding van de interface voor je sessie. Op die manier kan TypeScript je wijzen op alle plaatsen waar de sessie gebruikt werd en kan je die code vervangen door code op basis van JWT's.

Controleer daarna verder gebruik van de session (via Ctrl-f). Om na te gaan dat je JWT de juiste data bevat, kan je een base64 decoder gebruiken op de payload. Je vindt er makkelijk een met een zoekmachine.

{% hint style="info" %}
Test achteraf uit wat gebeurt als je je applicatie herstart!
{% endhint %}
