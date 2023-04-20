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

Eén van de gemakkelijkste manieren waarmee een DevContainer kan gestart worden is een Git repository aanmaken. Binnen die Git repository wordt vervolgens een folder `.devcontainer` gemaakt, met daarin een `devcontainer.json` bestand. Dit bestand bepaalt welke systemen beschikbaar zullen zijn in de DevContainer. VS Code heeft een handige extension die dit bestand voor jou creëert.

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

<img src="../../.gitbook/assets/image (1).png" alt="" data-size="original">

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

<details>

<summary>devcontainer.json</summary>

Dit is het devcontainer.json bestand dat gemaakt werd.

{% code title="devcontainer.json" %}
```json
// For format details, see https://aka.ms/devcontainer.json. For config options, see the
// README at: https://github.com/devcontainers/templates/tree/main/src/typescript-node
{
	"name": "Node.js & TypeScript",
	// Or use a Dockerfile or Docker Compose file. More info: https://containers.dev/guide/dockerfile
	"image": "mcr.microsoft.com/devcontainers/typescript-node:0-18"

	// Features to add to the dev container. More info: https://containers.dev/features.
	// "features": {},

	// Use 'forwardPorts' to make a list of ports inside the container available locally.
	// "forwardPorts": [],

	// Use 'postCreateCommand' to run commands after the container is created.
	// "postCreateCommand": "yarn install",

	// Configure tool-specific properties.
	// "customizations": {},

	// Uncomment to connect as root instead. More info: https://aka.ms/dev-containers-non-root.
	// "remoteUser": "root"
}

```
{% endcode %}

</details>
