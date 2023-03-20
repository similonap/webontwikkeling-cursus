# Requests

Wanneer een gebruiker naar het domein van onze website surft, stuurt zijn browser een `GET`-request naar de route `/` van onze applicatie.

Die kunnen we bijvoorbeeld zo afhandelen:

```typescript
app.get('/',(req,res)=>{
    res.type("text/html")
    res.send("hello");
});
```

De gebruiker vraagt bijvoorbeeld naar `localhost:3030` en krijgt zo de tekst "hallo" te zien.

Wat als we de gebruiker wat meer controle willen geven over de request?

## **GET requests**

`GET`-requests zijn de "default". Express-applicaties bevatten vaak calls van de vorm `app.get` en deze dienen dus om aan te geven hoe een `GET`-request moet worden afgehandeld. Met andere woorden: wat moet gebeuren wanneer de gebruiker naar een bepaalde pagina surft. Om meer data mee te geven kunnen we gebruik maken van query strings, bijvoorbeeld:

```typescript
https://www.google.be/search?q=ap&client=safari
```

Dit is een `GET` request naar Google. De domeinnaam is `google.be`. Het pad is `/search`. Alles achter `?` is de query string: `q=ap&client=safari`

De query string bepaalt de velden en waarden die we naar de server willen sturen. In dit geval sturen we q met de waarde "ap" (de zoekterm) en client met de waarde "safari" (de gebruike web browser).

### **Query**

Om de waarden in een query string te raadplegen, maken we gebruik de property `query` van het request object.

{% hint style="info" %}
Het request object is de eerste parameter in de callback functie van `app.get`. Dit object bevat informatie van de request die de gebruiker/browser stuurt.
{% endhint %}

Veronderstel dat we een array met namen hebben. We willen een naam opzoeken door een index mee te geven.

```typescript
let people = ["Sven","Andie","George","Geoff"];

app.get("/person",(req,res)=>{
    res.type('text/html')
    let index_ = req.query.index;
    // TypeScript kan niet garanderen dat deze parameter een geldige waarde heeft gekregen
    // de if staat ons toe binnen dat block te veronderstellen dat string het type is
    if (typeof index_ === "string") {
      let index = parseInt(index_);
      res.send(people[index]);
    }
    else {
      res.send("Ongeldige parameterwaarde.");
    }
});
```

`req` is het Request object. De property `query` bevat alle query velden die meegestuurd worden.

{% hint style="info" %}
Probeer zelf eens een lijst van query velden toe te voegen aan de URL en print de inhoud van `req.query` naar de console.
{% endhint %}

{% hint style="danger" %}
Let op welke characters je gebruikt in een query string. Je kan bv. geen spaties gebruiken. Wil je in jouw client applicatie een random string meegeven als waarde, gebruik dan [URI Encode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/encodeURI) om deze om te zetten in een geldige string!
{% endhint %}

### **Route Parameters**

In plaats van query strings te gebruiken, kunnen we ook gestructureerde routes maken die parameters integreren in het pad zelf. Route parameters laten ons toe parameters te definiëren in onze route. Bijvoorbeeld:

```typescript
let people = ["Sven","Andie","George","Geoff"];
app.get('/person/:index',(req,res)=>{
    let index = parseInt(req.params.index);
    res.type('text/html')
    res.send(people[index]);
})
```

Parameters van een route starten met `:`. De gebruiker moet een waarde achter `/person/` plaatsen om de route aan te spreken.

Door `:index` bepaal je de naam van de property die de waarde van de parameter zal bevatten. Deze naam kan je dan gebruiken om de property terug te vinden in het object `params` van het request object.

Je kan ook meerdere parameters meegeven:

```typescript
let people = ["Sven","Andie","George","Geoff"];
app.get('/person/:index/replace/:newname',(req,res)=>{
    let index = parseInt(req.params.index);
    let oldName = people[index];
    people[index] = req.params.newname;
    res.type("text/html")
    res.send(`Old name was ${oldName}, new name is ${people[index]}`);
})
```

## POST Requests

`GET` requests zijn beperkt door de lengte van de url (meestal 2048). Dit wil zeggen dat je grote hoeveelheid data zoals bv lange paragrafen tekst, bestanden, grote JSON objecten, etc. niet kan doorsturen via een `GET` request. Ze brengen ook een veiligheidsrisico mee omdat hun inhoud in de URL staat. Je wil bijvoorbeeld niet dat je wachtwoord zomaar zichtbaar is in je browserbalk!

`GET` requests zijn ook niet geschikt voor operaties die een aanpassing teweegbrengen (zoals het versturen van een formulier). Dat komt onder meer omdat een paginarefresh zorgt dat het request opnieuw wordt uitgevoerd!

{% hint style="danger" %}
Let op. De inhoud van een `POST` request is ook leesbaar. Tenzij je gebruik maakt van encryptie, is de data niet veilig. Moderne browsers waarschuwen je automatisch wanneer je een website bezoekt die verkeer niet encrypteert.
{% endhint %}

Om `POST` requests makkelijk te behandelen voegen we volgende lijnen toe aan onze applicatie:

```typescript
app.use(express.json({ limit: '1mb' }));
app.use(express.urlencoded({ extended:true}))
```

De waarde voor `limit` kies je zelf. Dit is de maximale grootte van het request. De tweede lijn zorgt ervoor dat de inhoud van de `POST` omgezet wordt in een handig JSON object.

Om een `POST` request te behandelen gebruiken we `app.post` ipv `app.get`.

```typescript
app.post('/sendData',(req, res)=>{
    // code hier
});
```

Laten we een simpel formulier maken om gegevens naar deze route te sturen:

```html
<form action="/sendData" method="post">
    <div>
        <label for="fname">First name?</label>
        <input name="fname" id="fname" value="George">
      </div>
      <div>
        <label for="lname">Last Name?</label>
        <input name="lname" id="lname" value="Smith">
      </div>
      <div>
        <button type='submit'>Send!</button>
      </div>
</form>
```

Dit voorbeeld stuurt 2 velden: `fname` en `lname`. Omdat het attribuut `method` van het `form`-element op `post` staat, worden de gegevens verstuurd als een `POST` request. Om de data die gestuurd is op te vragen, gebruiken we het Request object. Hierin bevindt zich de property `body` die de velden bevat van het `POST` request:

```typescript
app.post('/sendData',(req, res)=>{
    let data = req.body;
    res.json(data);
})
```

De velden fname en lname bevinden zich in `req.body`:

```typescript
app.post('/sendData',(req, res)=>{
    let firstName = req.body.fname;
    let lastName = req.body.lname;
    res.type('text/html')
    res.send(`Hello ${firstName} ${lastName}`);
})
```

