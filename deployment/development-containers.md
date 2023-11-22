# Development containers

#### Gebruik van omgevingsvariabelen in Docker

In een Docker Compose file kan je een of meerdere `.env`-bestanden inladen door middel van een key `env_file`. Je vindt hiervan een voorbeeld in de [Docker Compose reference](https://docs.docker.com/compose/compose-file/#env\_file).

Wanneer deze zijn ingeladen, kunnen applicaties in de container de variabelen gebruiken. Een Node.js-applicatie kan bijvoorbeeld `process.env.MYVARIABLE` gebruiken. Ze kunnen ook gebruikt worden in zogenaamde Bash-instructies voor de container (zoals `postStartCommand`), maar daar moet je dan het formaat `$MYVARIABLE` gebruiken.
