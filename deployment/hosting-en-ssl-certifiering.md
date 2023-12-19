# Hosting en SSL-certifiëring

Hosting houdt in dat je je applicatie online beschikbaar maakt. Hier zijn verschillende mogelijkheden voor. Tegenwoordig zijn er veel gespecialiseerde diensten voor. Wij zullen [https://render.com/](https://render.com/) gebruiken.

SSL-certificering (Secure Sockets Layer) is een beveiligingsprotocol dat ervoor zorgt dat alle gegevens die tussen een webserver en een browser worden uitgewisseld, privé blijven en integraal zijn. Dit wordt bereikt door het versleutelen van de gegevens die worden verstuurd, waardoor ze niet leesbaar zijn voor derden die ze zouden kunnen onderscheppen.

Render voorziet zelf een SSL-certificaat voor je website. Dit betekent dat je website over HTTPS wordt aangeboden (de "S" staat voor "SSL").



## Stap 1: je code op Github plaatsen

Maak een repository voor het project dat je wil hosten. Push de code naar **Github** (niet Gitlab!). Zorg dat de repository de root folder van je applicatie is.

{% hint style="warning" %}
Indien je nog geen gebruik hebt gemaakt van Github, moet je vermoedelijk eerst een SSH-sleutelpaar aanmaken. Kort samengevat: voer het commando `ssh-keygen -t rsa` uit. Ga op Github naar je settings en zoek het onderdeel over SSH sleutels. Kies om een nieuwe toe te voegen, met een naam naar keuze. Ga dan op je PC naar de map `.ssh` die vermeld wordt na dat commando. Kopieer de inhoud van de file met de extensie `.pub` naar het tekstvak voor je sleutel op Github.&#x20;
{% endhint %}

## Stap 2: een Render account aanmaken en connecteren met Github

Maak een gratis account aan. Verbind hem met je Github account.

## Stap 3: "web service" aanmaken

Een "Web service" hoeft hier geen "API endpoint" te zijn. Het kan een gewone Express applicatie zijn. Je build commando is `npm i`. Je deploy commando is `ts-node index.ts`. Stel je applicatie zo in dat een push naar Github meteen een nieuwe deploy tot gevolg heeft.

## Stap 4: code aanpassen

Render veronderstelt dat je applicatie op poort 10000 draait. Je kan dit wel aanpassen door het in de .env file te specifiëren, maar er is geen reden om dit niet te doen.

Zorg ook dat `ts-node` lokaal geïnstalleerd is indien nodig. Mogelijk is het momenteel globaal geïnstalleerd. Je mag dit als development dependency installeren.

Zorg ook dat je cookies,... de `secure` vlag op true hebben staan wanneer je code op Render draait, maar niet wanneer ze lokaal draait. Ook dit kan je bereiken via omgevingsvariabelen.

Doe na je aanpassingen opnieuw een push. Render zal automatisch de applicatie updaten.

## Stap 5: uittesten

Ga in het dashboard naar het overzicht van je applicatie. Als deployment gelukt is, staat er een groen wolkje in het overzicht. Via de getoonde URL zou je de applicatie moeten kunnen bereiken.
