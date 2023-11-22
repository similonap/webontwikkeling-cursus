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

**Neem op dit punt een backup van je code, want in de volgende oefening moet je terug naar hier.**

Zorg dat de login bijgehouden wordt in een sessie. Zorg er ook voor dat alle routes die enkel voor een specifieke trainer bedoeld zijn een 403-fout opleveren wanneer iemand niet (met het juiste ID) is ingelogd.

{% hint style="danger" %}
Omdat de technieken rond veilige opslag van wachtwoorden in een ander vak aan bod komen, investeren we daar geen tijd in. Denk er echter aan dat je in een productieomgeving **nooit** wachtwoorden als plain text opslaat.
{% endhint %}

{% hint style="info" %}
Test achteraf uit wat gebeurt als je je applicatie herstart!
{% endhint %}

## Login met JWT

{% hint style="info" %}
Dit is een eerder grote vraag. Hou je applicatie goed in de gaten met `console.debug` en test na elke tussenstap.
{% endhint %}

Start terug van je backup en voorzie dezelfde functionaliteit, maar gebruik een JWT-token in plaats van een sessie.

{% hint style="info" %}
Test achteraf uit wat gebeurt als je je applicatie herstart!
{% endhint %}
