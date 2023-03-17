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
