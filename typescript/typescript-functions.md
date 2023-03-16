# TypeScript: Functions

Een functie kan op 2 manieren geschreven worden:

```typescript
function add(a,b,c){
  return a+b+c;
}
```

Dit is een "named function". De functie heeft de naam add.

of

```typescript
const add = (a,b,c) => {
  return a+b+c;
}
```

Dit is een "anonymous function". De functie heeft geen naam maar wordt toegekend aan de variabele add.

In beide gevallen heeft de functie hier 3 parameters: a, b en c.

De functie geeft ook een waarde terug: a+b+c. Hiervoor gebruik je `return`

{% hint style="danger" %}
We gebruiken altijd anonymous functions. Vanaf nu mag je de schrijfwijze met het keyword function vergeten.
{% endhint %}

Functies roep je op adhv de naam van de variabele waar de functie zich in bevindt plus haakjes () en de nodige parameters:

```typescript
const hallo = () => {
  console.log("hallo");
}
hallo();
```

Hierboven hebben we een functie met 0 parameters. We roepen ze dus op met `hallo()`

```typescript
const add = (a,b) => {
  return a+b;
}
let total: number = add(1,2);
```

Deze functie heeft 2 parameters: a en b. Deze functie heeft ook een return waarde. We kunnen de uitkomst van deze functie dus toekennen aan een variabele.

{% hint style="danger" %}
Let op: return stopt de uitvoering van een functie. De console log in de code hieronder zal dus nooit uitgevoerd worden. De functie stop bij lijn 2:
{% endhint %}

```typescript
const add = (a,b) => {
  return a+b;
  console.log("dit wordt niet uitgevoerd");
}
let total: number = add(1,2);
```

## Functies en types

In TypeScript heeft alles een type nodig. Dit doen we bij functies als volgt:

```typescript
const add = (a: number,b: number):number => {
  return a+b;
}
let total: number = add(1,2);
```

Achter elke parameter plaats je het type. a is van het type number, b is van het type number. Achter de haakjes van de parameters staat het return type, het type dat uiteindelijk door de functie wordt teruggegeven. Hierboven is dit een number. Hieronder een string:

```typescript
const sumToText = (a: number,b: number):string => {
  return `The sum is ${a+b}`;
}
let totalText: string = sumToText(1,2);
```

In TypeScript moet je je ook houden aan de exacte beschrijving van de functie:

```typescript
const add = (a: number,b: number):number => {
  return a+b;
}
let total: number = add(1); // ERROR
let total2: number = add(1,2,3); // ERROR
```

add verwacht 2 parameters. Lijn 4 en 5 zijn dus fout.

### Optionele parameters

Je kan ook bepalen dat sommige parameters optioneel zijn. Dan hoef je ze niet altijd mee te geven aan jouw functie.&#x20;

```typescript
const add = (a: number,b?: number):number => {
  if(b){
    return a+b;
  }
  else return a;
}
let total: number = add(1); // werkt
let total2: number = add(1,2,3); // ERROR
```

Hierboven is b optioneel. Dit wil zeggen dat ik b niet moet meegeven worden: add(1) is dus ok.

{% hint style="danger" %}
Let wel op: nu moet je nakijken of b bestaat. In jouw functie mag je niet meer veronderstellen dat die een waarde zal bevatten
{% endhint %}

{% hint style="danger" %}
Opgelet: een optionele parameter kan niet gevolgd worden door een niet-optionele parameters:
{% endhint %}

```typescript
const add = (a?: number,b: number):number => {
  /// kan niet!
```

### Default parameters

Je kan ook default waarden meegeven aan jouw parameters. Dit wil zeggen dat wanneer de parameter niet zou worden meegegeven, een default waarde verondersteld wordt:

```typescript
const add = (a: number,b = 2):number => {
    return a+b;
}
let total: number = add(1); // werkt
let total2: number = add(1,2); // werkt
let total3: number = add(1,2,3); // ERROR
```

In het voorbeeld hierboven krijgt b een default waarde 2. Wanneer je dus geen tweede parameter meegeeft, zal b de waarde 2 bevatten.

```typescript
const hello = (name = "Class"):void => {
    console.log(`Hello ${name}`);
}
hello(); // Hello Class
hello("George"); // Hello George
```

Default waarden hoeven niet achteraan te staan:

```typescript
const add = (a=2,b: number):number => {
    return a+b;
}
let total: number = add(1); // ERROR
let total2: number = add(1,2); // werkt
let total3: number = add(undefined,2); // werkt
```

Merk op op lijn 6: als je niets wilt meegeven voor parameter a, dan geef je `undefined` mee.

## Interfaces

Wanneer we een functie definiëren, geven we die meestal mee aan een variabele:

```typescript
const hello = () => {console.log("hello");
```

Maar wat is het type van hello?

We kunnen een type definiëren die een functie beschrijft adhv interfaces. Met een interface kunnen we beschrijven hoeveel parameters een functie moet hebben, wat de types zijn van de parameters en het type van de return waarde:

```typescript
interface Hello {
    ():void
}
```

Voor de functie hello worden geen parameters verwacht. Het heeft ook geen return waarde (dus void). Nu kan je de variabele een type geven:

```typescript
const hello: Hello = () => {console.log("hello");
```

Je kan ook bv. een array van dit type maken:

```typescript
let helloFunctions: Hello [] = [];
```

Let op: in deze array mag ik enkel functies steken die overeenkomen met de interface: een functie met 0 parameters die geen return waarde heeft:

```typescript
helloFunctions.push(() => {console.log("hello"));
helloFunctions.push(() => {console.log("hi));
helloFunctions.push(() => {
    let a: number = 1;
    a++;
    //merk op, geen return waarde
});
```

Voor een functie met meer parameters en bv. een return waarde:

```typescript
interface AddFunction {
  (a:number, b:number):number;
}
let add:AddFunction= (a,b) =>{
  return a+b;
}
let c:number = add(1,2);
```

{% hint style="info" %}
Let op: het Addfunction type impliceert de types van de parameters en return waarden. Je hoeft die dus niet uit te schrijven
{% endhint %}

## Verkorte notatie

Wanneer je maar 1 lijn code hebt staan in jouw functie, kan je jouw schrijfwijze verkorten:

```typescript
let hello = () => { console.log("hello"); };
```

```typescript
let hello = () => console.log("hello");
```

Wanneer jouw lijn code een return doet, hoef je zelfs return niet meer te vermelden:

```typescript
interface Calculation {
    (a:number, b:number):number
};
let add: Calculation = (a,b) => { return a + b };
```

```typescript
let add: Calculation = (a,b) => a + b ;
```

Wanneer je maar 1 parameter hebt, kan je zelfs de haakjes rond de parameter weglaten:

```typescript
interface Calculation {
    (a:number):number
};
let double: Calculation = (a) => { return 2*a };
```

```typescript
let double: Calculation = (a) =>  2*a;
```

```typescript
let double: Calculation = a =>  2*a;
```

