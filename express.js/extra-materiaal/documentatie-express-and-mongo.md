# Documentatie Express\&Mongo

## Basis Express Application

```typescript
import express from "express"; // importeer de express module

const app = express(); // maak een express applicatie aan

app.set("port", 3000); // definieer de poort
app.set('view engine', 'ejs');
app.set('views', `${__dirname}/views`);

app.use(express.static(`/public`));

app.listen(app.get("port"), () => // gebruik de poort en toon een boodschap als dit lukt
  console.log("[server] http://localhost:" + app.get("port"))
);
```

## MongoDB Connection

```typescript
import * as MongoClientModule from "mongodb";

const username = "MY_USERNAME";
const password = "MY_PASSWORD";

const uri = `mongodb+srv://${username}:${password}@MY_MONGODB_URL`;
const client = new MongoClientModule.MongoClient(uri);

const getData = async (req: any, res: any) => {
    client
        .db("WebOntwikkeling")
        .collection("MY_COLLECTION")
        .find({})
        .toArray()
        .then(data => {
            res
                .status(200)
                .json(data);
        });
}
```
