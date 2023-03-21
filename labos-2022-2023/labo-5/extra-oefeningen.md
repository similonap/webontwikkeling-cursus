# Extra oefeningen

## DadJoke

Schrijf een express server die de volgende routes ondersteund:

* /joke/json
* /joke/html

Deze routes moeten allebij een dadjoke ophalen van `https://icanhazdadjoke.com/` en deze teruggeven in de juiste content-type. Als de route /joke/json is, moet de dadjoke in JSON formaat teruggegeven worden. Als de route /joke/html is, moet de dadjoke in HTML formaat teruggegeven worden.

De applicatie moet op poort 3000 draaien.

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-21 at 23.09.17.png" alt=""><figcaption><p>/joke/html</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2023-03-21 at 23.10.11.png" alt=""><figcaption><p>/joke/json</p></figcaption></figure>

## ViewCounter

### Opdracht

Maak een webserver in express die telkens een pagina teruggeeft met het totaal aantal bezoeken (globaal) en het aantal bezoeken per pad.

Je moet dus een globale teller bijhouden en een teller per pad (bv door een object te gebruiken dat als key het pad heeft en als value het aantal views). Bij het herstarten van de server mogen de tellers opnieuw op 0 gezet worden.

{% hint style="info" %}
Voor een handler te schrijven voor alle paden kan je best eens kijken hoe we de 404 handler hebben geschreven in de theorie.&#x20;
{% endhint %}

### Voorbeeldinteractie

<figure><img src="../../.gitbook/assets/visits.gif" alt=""><figcaption></figcaption></figure>
