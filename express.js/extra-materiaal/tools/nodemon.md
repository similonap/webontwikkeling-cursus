# Nodemon

Tot nu toe hebben we altijd de server handmatig moeten herstarten als we een wijziging aanbrengen in onze code. Dit is niet erg handig tijdens de ontwikkeling van een applicatie. Gelukkig is er een tool die dit voor ons doet. Deze tool heet `nodemon`. Deze tool monitored onze code en herstart de server elke keer als er een wijziging is.

## Installatie

Om `nodemon` te installeren voeren we het volgende commando uit:

```bash
npm install --save-dev nodemon
```

## Gebruik

Om `nodemon` te gebruiken voeren we het volgende commando uit:

```bash
nodemon index.ts
```

nodemon heeft ingebouwde ondersteuning voor TypeScript. Dit betekent dat we geen aparte `ts-node` commando hoeven uit te voeren. `nodemon` zal automatisch de juiste TypeScript compiler gebruiken. 