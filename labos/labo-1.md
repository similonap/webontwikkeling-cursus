# Week 1

## 1. Installeer Git

{% embed url="https://git-scm.com/downloads" %}

## 2. Visual Studio Code

**Stap 1:**\
Installeer Visual Studio Code indien je die nog niet hebt:

{% embed url="https://code.visualstudio.com/" %}

**Stap 2:**\
Configureer VS Code zodat Bash de default terminal wordt. Volg volgende instructies, de te kopieren lijn staat onder de afbeelding.

![](<../.gitbook/assets/image (4).png>)

```
"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"
```

{% hint style="info" %}
Opgelet: Indien je Git ergens anders geinstalleerd hebt, moet je dit aanpassen in de lijn hierboven.
{% endhint %}

Open een Terminal (menu Terminal -> New Terminal) in Visual Studio Code om te testen dat ie werkt.&#x20;

{% hint style="info" %}
We gaan de terminal niet uitgebreid gebruiken, maar als webontwikkelaar is het belangrijk dat je die onder de knie krijgt. Gebruik je liever Windows Powershell, dan kan dat. We weten echter uit ervaring dat dit minder vlot loopt dan wanneer je bash shell gebruikt. Bekijk zeker wat tutorials over het gebruik van de terminal, of lees dit artikel eens door: [https://medium.com/@grace.m.nolan/terminal-for-beginners-e492ba10902a](https://medium.com/@grace.m.nolan/terminal-for-beginners-e492ba10902a)
{% endhint %}

## 2. Maak een Github repository

**Stap 1:**\
Ga naar [Github](http://github.com), log in en maak een nieuwe repository aan met naam `WebOntwikkeling_2021_Naam_Voornaam`

bv:

![](<../.gitbook/assets/les1\_fig3 (1).png>)

Zorg dat jouw repository privaat staat:

![](../.gitbook/assets/les1\_fig4.png)

Geef toegang aan Andie en Sven: `svencharleer` en `similonap`

![](../.gitbook/assets/les1\_fig5.png)

**Stap 2:**\
Maak een folder aan op jouw laptop genaamd `Webontwikkeling_2021`. In deze folder zal je al jouw opdrachten maken tijdens dit semester.

**Stap 3:**

Open deze folder in VSCode. Open een terminal en voer het commande `pwd` uit. Dit toont je dat je je in de juiste folder bevindt.

**Stap 4:**

Volg de stappen op Github (info vind je op de Code tab in jouw repository) om vanuit deze folder een `README.md`bestand toe te voegen en te pushen naar jouw Webontwikkeling repository op Github.

## Node.js

Nu installeren we Node.js. Dit is een JavaScript runtime. Deze laat ons toe JavaScript code uit te voeren zonder browser. We kunnen hiermee applicaties schrijven, zoals bv. een server applicatie. Alle opdrachten die je in Webontwikkeling maakt, zullen worden uitgevoerd met Node.js.

{% embed url="https://nodejs.org/en/" %}

Om te testen of Node.js werkt, voer je het commande node uit in de terminal (je zal waarschijnlijk eerst eens moeten herstarten)

![](<../.gitbook/assets/image (2) (1).png>)

Hier kan je nu JavaScript code invoeren. Probeer de volgende lijnen eens uit:

```
let a = 2;
a = a + 3;
a = "hello";
```

Experimenteer gerust nog wat verder. Wanneer je klaar bent, druk je 2 maal `CTRL-C` om uit node te gaan.

{% hint style="info" %}
We zullen nooit rechtstreeks in Node lijnen code typen. We maken files uit en laten node deze uitvoeren. Hier komen we nog op terug.
{% endhint %}

{% hint style="info" %}
Zorg dat je altijd in de bash shell zit, en niet in node! Je kan geen bash shell commandos typen in node (zoals van folder veranderen, of node starten).\
Je herkent bash meestal aan het $ teken. Als je > ziet, zit je waarschijnlijk in Node.
{% endhint %}

## NPM

NPM is een package manager. Het laat je toe nieuwe packages toe te voegen aan jouw applicatie en zo gebruik te maken van bestaande oplossingen en tools die jouw leven gemakkelijker maken. Je vindt een grote library van packages op [https://www.npmjs.com/](https://www.npmjs.com/)

npm is beschikbaar op jouw laptop wanneer Node.js geinstalleerd is. Typ `npm` in jouw terminal en je zal wat help en versie info te zien krijgen.

**Stap 1:**

Het eerste package dat we moeten installeren is [https://www.npmjs.com/package/ts-node](https://www.npmjs.com/package/ts-node) . Dit laat ons toe TypeScript uit te voeren in Node.

{% hint style="info" %}
Bekijk zeker eens de pagina van dit NPM package. Elk package heeft een uitgebreide uitleg, over hoe je het installeert en gebruikt. Indien je iets niet weet, bekijk zeker altijd de pagina van het package eerst.
{% endhint %}

Voer volgende commandos uit in jouw terminal:

```
npm install -g typescript
npm install -g ts-node
```

De optie `install` zegt dat je een npm package wil installeren. Je kan een package terug verwijderen door uninstall te gebruiken. -g betekent dat je dit package "globally" installeert. Dit wil zeggen: het package is beschikbaar op jouw computer, niet alleen in jouw project.&#x20;

**Stap 2:**

Voer het commando ts-node uit. Probeer daar de vorige lijnen code die we in Node getest hebben (en dus met pure JavaScript) uit te voeren. Wat loopt er mis?

```
let a = 2;
a = a + 3;
a = "hello"
```

Gebruik weer CTRL-C x 2 om terug naar de terminal te gaan.

## TypeScript files

Maak eerst een `.gitignore` file aan en kopieer de inhoud van volgende file hierin: [https://www.toptal.com/developers/gitignore/api/node](https://www.toptal.com/developers/gitignore/api/node) \
Commit en push deze file.

Maak in jouw Webontwikkeling folder een folder `Labo1` aan. Hierin maak je een nieuw bestand `printNameAndAge.ts`. Push en commit jouw folder naar Github met boodschap "Labo 1 aangemaakt".

Schrijf nu een script in TypeScript dat&#x20;

* 3 variables initialiseert met jouw voornaam, jouw achternaam en jouw leeftijd
* 1 variable die de zin bevat \
  "Ik ben _voornaam achternaam_ en ik ben _leeftijd_ jaar oud"\
  **gebruik makend van de 3 vorige variables en waar voornaam/achternaam/leeftijd vervangen zijn door de waarden van de 3 variables**
* deze laatste variable print je naar je scherm met gebruik van console.log

{% hint style="info" %}
Om jouw code te testen, ga naar de Labo1 folder in jouw terminal en typ `ts-node printNameAndAge.ts.` Gebruik de error meldingen om jouw fouten te vinden en op te lossen.
{% endhint %}

{% hint style="info" %}
Kijk altijd na met `pwd` of je in de juiste folder staat met jouw terminal. Gebruik `cd Labo1` indien je nog in jouw Webontwikkeling folder zit.
{% endhint %}

Push en commit jouw folder naar Github met boodschap "Labo 1 gedaan".

