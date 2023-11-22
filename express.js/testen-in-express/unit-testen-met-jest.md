# Unit testen met Jest

Unit testen in Express-applicaties met Jest biedt een krachtige manier om de betrouwbaarheid en stabiliteit van je applicatie te garanderen. Jest is een populair JavaScript testing framework dat zich onderscheidt door zijn eenvoudige configuratie en rijke functionaliteiten. Bij het schrijven van unit tests voor Express-applicaties in TypeScript, is het belangrijk om je te focussen op het isoleren van individuele functies of componenten van de applicatie, waarbij het gebruik van mocks tot een minimum wordt beperkt. Hieronder vind je een basisvoorbeeld van hoe je kunt beginnen met het testen van een Express-route in TypeScript met Jest.

Installeer eerst Jest en Supertest (om HTTP requests te doen): `npm i --save-dev jest supertest @types/supertest`

{% hint style="info" %}
Dit zijn development dependencies, want de applicatie die aan de gebruiker wordt aangeboden heeft ze niet nodig. Ze zijn alleen nodig voor de ontwikkelaar.
{% endhint %}

Veronderstel dat je deze app met één route hebt:

```typescript
// app.ts
import express, { Express, Request, Response } from 'express';

const app: Express = express();

app.get('/hello', (req: Request, res: Response) => {
  res.status(200).send('Hallo Wereld');
});

export default app;

```

Dan kan je een Jest-test schrijven als volgt:

```typescript
// app.test.ts
import request from 'supertest';
import app from './app';

describe('GET /hello', () => {
  it('should return Hallo Wereld', async () => {
    const response = await request(app).get('/hello');
    expect(response.status).toBe(200);
    expect(response.text).toBe('Hallo Wereld');
  });
});

```
