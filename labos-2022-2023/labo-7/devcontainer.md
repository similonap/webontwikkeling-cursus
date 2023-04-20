# Devcontainer

{% hint style="info" %}
## Theorie

_Bekijk eerst de theorie voor je aan de oefeningen begint!_

* [DevContainers](../../express.js/extra-materiaal/devcontainers.md)
{% endhint %}

## Oefeningen

### Oefening 1: maak een DevContainer Repository

* [ ] Maak een nieuwe GitLab repository
* [ ] Gebruik VS Code om een DevContainer in die repository te maken
  * [ ] Kies voor een `Node & TypeScript` project
  * [ ] De andere opties mag je laten staan op hun default waardes
* [ ] Voeg een [.gitignore](https://www.toptal.com/developers/gitignore/api/node) file toe
* [ ] installeer ts-node globaal\
  `npm i -g ts-node`
* [ ] installeer nodemon globaal\
  `npm i -g -D nodemon`
* [ ] Maak een nieuwe folder genaamd `app` & Open de `app` folder in de terminal
*   [ ] Gebruik vervolgens de terminal om `Node`, `Typescript`, `Express` te installeren via NPM in de `app` folder

    ```
    npm init -y && tsc --init && npm i -D @types/node
    npm i ejs && npm i -D @types/ejs
    npm i express && npm i -D @types/express
    ```
* [ ] Gebruik `git` om je wijzigingen te pushen naar Gitlab