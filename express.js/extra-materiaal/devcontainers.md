---
description: met MongoDB voorbeeld
---

# DevContainers

## DevContainers

### Intro

Dit project zal gebruik maken van Node, Typescript, Express en MongoDB.

* Node: de basis om onze applicatie te ontwikkelen
* Typescript: de taal die we gebruiken om te ontwikkelen binnen Node
* Express: back-end framework
* MongoDB: NoSQL database omgeving

Hoewel het mogelijk is om deze systemen te installeren op onze computer, gaan we gebruik maken van **Docker** containers. Dit heeft enkele voordelen:

* Samenwerking: door de container-setup te delen met anderen (bv. via git) verzekeren we dat iedereen werkt met exact dezelfde versie van Node, Angular, Express en PostgreSQL.
* Deployment: we kunnen de server opzetten zodat deze Docker containers kan draaien. Hierdoor wordt deployment van onze app een heel stuk gemakkelijker.
* Setup: moet je werken op een ander apparaat? Wil je verder werken via een online codespace? Heb je je eigen apparaat moeten herinstalleren? Met één command ga je terug aan de slag.

Om te kunnen ontwikkelen in deze Docker omgeving gaan we gebruik maken van een **DevContainer**. Een DevContainer laat ons toe om een Docker container als development omgeving te gebruiken. VS Code heeft (via het [remote development extension pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack)) de mogelijkheid om een devcontainer op te starten die je hebt opgeslagen op een git repository.

### Overzicht

#### Software

_Installeer deze software voor je begint aan de rest van de guide. Je hebt alles nodig dat hieronder staat opgelijst._

* [WSL](https://learn.microsoft.com/en-us/windows/wsl/install): nodig om Docker te draaien.
  1. Open Powershell als administrator
  2.  Gebruik het volgende commando en volg de installatie procedure.

      ```
      WSL --install
      ```
* [Docker Desktop](https://www.docker.com/products/docker-desktop/): Docker Desktop installeert meteen ook de cli van Docker. Docker heb je nodig om een container op te starten.
* [Visual Studio Code](https://code.visualstudio.com/): De IDE waar we van gebruik maken in deze guide.
* [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack): De extensions die vereist zijn om in VS Code te werken met DevContainers.

### Opstart Repository

In deze guide maak ik gebruik van GitLab. Github werkt even goed, net als andere git repositories.

In Gitlab:

1. Maak een nieuw project aan.
2. Kies voor een 'blank project'.
3. Vul de gegevens in van je project:
   * project naam
   * slug
   * vink de optie UIT om een readme aan te maken.

Eens je project is aangemaakt hebben we de HTTPS URL nodig van je git project. Deze URL vind je terug onder de knop 'Clone'.

<img src="../../.gitbook/assets/image (5).png" alt="" data-size="original">

### Opstart DevContainer

#### Stap 1: opstart Docker en VSCode

* Start Docker op en zorg dat het venster van Docker Desktop openstaat.
* Open Visual Studio Code (VS Code). Kijk na of je het Remote Development Extension Pack geinstalleerd hebt. Het maakt niet uit welk bestand of project momenteel geopend is, want VS Code zal voor dit project zelf een nieuw venster openen.

#### Stap 2: van Repository naar Devcontainer

* Open het Command Palette (`Ctrl+Shift+P`) en zoek naar het commando\
  `Dev Containers: Clone Repository in Container Volume`.
* Druk op Enter om het commando te bevestigen.
* Er wordt nu om een Git URL gevraagd. Dit is de HTTPS URL van je git repository.

> ⚠️ Er is een tweede commando dat er sterk op lijkt (`Dev Containers: Clone Repository in Named Container Volume`). Let dus op dat je voor het juiste kiest!

#### Stap 3: DevContainer Configuratie

* Je wordt gevraagd om een Dev Container Configuration te kiezen. Zoek naar de optie '`Node.js & Typescript`'.
* Bij de volgende opties mag je de default waardes kiezen

De container wordt nu gedownload en opgestart. Dit kan even duren. Zeker wanneer je dit voor het eerst doet, zal het downloaden wat tijd kosten.

## Voorbeeld Project

### Folder Setup

Maak een nieuwe folder genaamd `app` aan. Open de terminal in deze folder.

Creëer ook 2 bestanden:

* `index.ts`
* `queries.ts`

Gebruik vervolgens de terminal om `Node`, `Typescript` en `Express` te initialiseren.

```bash
npm init -y && tsc --init && npm i -D @types/node
npm i ejs && npm i -D @types/ejs
npm i express && npm i -D @types/express
```

Het resultaat is de volgende bestandsstructuur:

```bash
└── app/
    ├── node_modules/
    |    └── ...
    ├── index.ts
    ├── package-lock.json
    ├── package.json
    ├── queries.ts
    └── tsconfig.json
```

### Setup Express Server

{% code title="index.ts" %}
```typescript
import express from 'express';
import * as db from './queries';

// create express app
const app = express();
const port = 3000;

// init middleware
app.use(express.json());
app.use(
    express.urlencoded({
        extended: true,
    })
);

// listen to port
app.listen(port, () => console.log(`App running on port ${port}.`));

// API express routes
const apiUrl = '/api';
app.get(`${apiUrl}/status`, (req: any, res: any) => res.json({ info: 'Node.js, Express, and MongoDb API' }));
app.get(`${apiUrl}/movies`, db.getMovies);
app.get(`${apiUrl}/movies/:name`, db.getMovieByName);
```
{% endcode %}

### Setup Database Queries

{% code title="queries.ts" %}
```typescript
import * as MongoClientModule from 'mongodb';

const username = "JOUW_DATABASE_GEBRUIKERSNAAM";
const password = "JOUW_DATABASE_WACHTWOORD";

const uri = `mongodb+srv://${username}:${password}@teacher-svb.42wgsrf.mongodb.net/?retryWrites=true&w=majority`;
const client = new MongoClientModule.MongoClient(uri);

const getMovies = async (request: any, response: any) => {
    client.db("WebOntwikkeling")
        .collection("Movies")
        .find({})
        .toArray()
        .then(vals => {
            response.status(200).json(
                vals
            );
        });
}

const getMovieByName = (request: any, response: any) => {
    const name = request.params.name;
    console.log(name);

    client.db("WebOntwikkeling")
        .collection("Movies")
        .findOne({ name: name })
        .then(val => {
            response.status(200).json(
                val
            );
        });
}

export { getMovies, getMovieByName }
```
{% endcode %}
