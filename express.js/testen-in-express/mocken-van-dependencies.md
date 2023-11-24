# Mocken van dependencies

Unit testen wordt vaak lastiger wanneer je code interageert met "de buitenwereld": filesystemen, databanken, invoer van de gebruiker, uitvoer naar de terminal, externe servers,...

Om deze reden wordt vaak gebruik gemaakt van "mocks": waarden die de plaats innemen van onderdelen die het moeilijk maken om unit testen te schrijven. Deze leveren vooraf vastgelegde data af eerder dan de echte handelingen uit te voeren. Achteraf kunnen we ook controleren dat deze gebruikt zijn zoals verwacht. Dit past binnen het black box principe dat gehanteerd wordt voor unit testen.

Hieronder bekijken we enkele voorbeelden:

### Mocken van het bestandensysteem

Stel, je hebt een Express-route die informatie leest van een bestand. Normaal gesproken zou je de `fs` module van Node.js gebruiken om het bestand te lezen. Voor testdoeleinden kun je echter de `fs` module mocken om consistente en gecontroleerde testresultaten te garanderen.

```typescript
// filenaam: fileController.ts
import { Request, Response } from 'express';
import fs from 'fs'; // onthoud deze import!

// we plaatsen dit niet meteen in app.get(...) en we benoemen de functie
export const readFile = (req: Request, res: Response) => {
  fs.readFile('/pad/naar/bestand.txt', 'utf8', (err, data) => {
    if (err) {
      res.status(500).send('Fout bij het lezen van het bestand');
    } else {
      res.status(200).send(data);
    }
  });
};

```

In een Jest-test kunnen we zorgen dat de oproep van fs.readFile vervangen wordt:

```typescript
// fileController.test.ts
import { readFile } from './fileController';
import fs from 'fs';
import { Request, Response } from 'express';

jest.mock('fs');

describe('readFile', () => {
  it('should read file content', () => {
    const mockReadFile = jest.spyOn(fs, 'readFile').mockImplementation((path, options, callback) => {
      callback(null, 'Mock bestandsinhoud');
    });

    // Partial is voor wanneer je dezelfde eigenschappen wil, maar allemaal optioneel
    let res: Partial<Response> = {
      send: jest.fn(),
      status: jest.fn().mockReturnThis(),
    };

    readFile({} as Request, res as Response);

    expect(res.send).toHaveBeenCalledWith('Mock bestandsinhoud');
    mockReadFile.mockRestore();
  });
});

```

### Mocken van databasetoegang

In dit voorbeeld maken we abstractie van de concrete database. Dat kan MongoDB zijn, MySQL,...

```typescript
// dbController.ts
import { Request, Response } from 'express';
import database from './database'; // Stel dat dit je database connectie module is

export const getDatabaseData = async (req: Request, res: Response) => {
  try {
    const data = await database.getData();
    res.status(200).json(data);
  } catch (err) {
    res.status(500).send('Databasefout');
  }
};

```

```typescript
// dbController.test.ts
import { getDatabaseData } from './dbController';
import database from './database';
import { Request, Response } from 'express';

jest.mock('./database'); // Mock de database module

describe('getDatabaseData', () => {
  it('should fetch data from the database', async () => {
    const mockData = [{ id: 1, naam: 'Testitem' }];
    database.getData = jest.fn().mockResolvedValue(mockData);

    let res: Partial<Response> = {
      json: jest.fn(),
      status: jest.fn().mockReturnThis(),
    };

    await getDatabaseData({} as Request, res as Response);

    expect(res.json).toHaveBeenCalledWith(mockData);
  });
});
```

### Mocken van een request

We gebruiken `fetch` om requests op externe services te doen. De eenvoudigste manier om dit te mocken is door gebruik te maken van `node-fetch:`

```typescript
// apiClient.ts
import fetch from 'node-fetch';

export const fetchDataFromAPI = async (url: string): Promise<any> => {
  try {
    const response = await fetch(url);
    const data = await response.json();
    return data;
  } catch (error) {
    throw new Error('Fout bij het ophalen van gegevens');
  }
};

```

```typescript
// apiClient.test.ts
import { fetchDataFromAPI } from './apiClient';
import fetch from 'node-fetch';

// Jest biedt een manier om modules te mocken
jest.mock('node-fetch', () => jest.fn());

describe('fetchDataFromAPI', () => {
  it('should fetch data from API', async () => {
    const mockResponse = { id: 1, naam: 'Testitem' };
    (fetch as jest.Mock).mockResolvedValueOnce({
      json: () => Promise.resolve(mockResponse),
    });

    const url = 'https://api.example.com/data';
    const data = await fetchDataFromAPI(url);

    expect(fetch).toHaveBeenCalledWith(url);
    expect(data).toEqual(mockResponse);
  });
});

```

{% hint style="warning" %}
Mocks maken het vaak gemakkelijker om snel een grote reeks unit tests uit te voeren, maar je wil jezelf er wel van verzekeren dat de _echte_, volledige applicatie ook werkt. Daarom gebruik je ze beter niet in end-to-end testen.
{% endhint %}
