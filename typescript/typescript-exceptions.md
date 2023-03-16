# TypeScript: Exceptions

Exceptions laten ons toe foutmeldingen door te geven op een eenvoudige manier. We gebruiken hiervoor throw, try, catch en finally.

## Throw

```typescript
let isFout = true;
if(isFout){
  throw 'Er is een fout'
}
```

Throw "gooit" de error. Indien deze in een functie wordt uitgevoerd, zal de functie stoppen. Er wordt geen return uitgevoerd. De functie stopt en geeft de exception mee als extra informatie die de omringende functie/code moet opvangen. Je kan eender wat "gooien":

```typescript
let isFout = true;
if(isFout){
  throw {waar:'Optellen', wat:'a is geen getal'}
}
```

## Try / Catch

Catch vangt de gegooide error op en plaats deze in de variabele "error". Deze kan kiezen de foutmelding te behandelen, of kan de foutmelding gewoon weer opnieuw door te gooien.&#x20;

```typescript
try{
  div(2,0);
}
catch(error)
{
  //do something with exception
}
```

In dit voorbeeld proberen we te delen door 0. Stel, div gooit een error wanneer 0 wordt meegegeven als 2e parameter. Om correct de error te behandelen, moet de functie in een try clausule gestoken worden. De opvolgende catch zal errors die eventueel gebeuren opvangen.

## Finally

```typescript
try{
  div(2,0);
}
catch(error)
{
  //do something with exception
}
finally {
  // this code always runs
}
```

Finally wordt altijd uitgevoerd. De code in try zal stoppen wanneer een fout zich voordoet. Catch zal de error behandelen. Of er nu een error gebeurt of niet, finally zal altijd uitgevoerd worden:

```typescript
try{
    let a = div(2,1);
    let b = div(3,0);
    console.log(b);
}
catch(error){
    console.log(error);
}
finally{
    console.log('This code must be reached no matter what');
}
```
