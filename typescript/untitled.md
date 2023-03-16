# TypeScript: Conditional Statements en Loops

## If/else

```typescript
if(true){
  console.log("true!");
}

if(false){
  //hier komen we nooit
}
else if(true){
  console.log("niet false, wel true!");
}
else{
  //hier komen we ook niet!
}
```

Een if statement kan alleen gebruikt worden. Wil je iets doen als if niet waar is, gebruik dan else.&#x20;

Je kan achter een else statement ook terug een if plaatsen.

### Ternary operator

We kunnen if/else statements ook op een verkorte manier schrijven. Stel de volgende if/else statement:

```typescript
let a: number = 10;
let b: number = 20;
if(a < b){ 
  console.log("a is kleiner"); 
}
else{
  console.log("a is groter");
}
```

Dit kunnen we verkorten met een ternary operator:

```typescript
let a: number = 10;
let b: number = 20;
a < b ? console.log("a is kleiner") : console.log("a is groter");
```

Het voordeel van een ternary operator is dat we deze ook in de parameter van bv. console.log kunnen verwerken. Net zoals bv. een functie, geeft de ternary operator gewoon een waarde terug. Indien waar, de waarde achter ?, indien niet waar, de waarde achter de :

We kunnen dit dus ook schrijven als:

```typescript
let a: number = 10;
let b: number = 20;
console.log(a < b ? "a is kleiner" : "a is groter");
```

## While

```typescript
let a: number = 10;
while(a< 20){
  console.log(a);
  a++;
}
```

While loopt totdat de conditie tussen de haakjes is voldaan. Hierboven zal de loop stoppen wanneer a de waarde 20 heeft. Merk op, de test gebeurt eerst. Dan wordt de loop uitgevoerd.

## Do While

```typescript
let a: number = 10;
do{
  console.log(a);
  a++;
} while(a<20)
```

Do/while lijkt erg op while. Het grootste verschil zit zich in wanneer de conditie wordt nagekeken. De loop wordt altijd 1 maal uitgevoerd, ongeacht de waarde van bv. a.

## Switch

```typescript
let animal: string = "dog";
switch(animal) {
  case "cat":
    console.log("it's a cat!");
    break;
  case "dog":
    console.log("it's a dog!");
    break;
  default:
    console.log("it's neither!");
    break;
}
```

Indien we een variabele moeten vergelijken met verschillende waarden, en elke waarde (of meerdere waarden) vragen dat je iets anders uitvoert, dan kan je best een switch statement gebruiken.

{% hint style="info" %}
Let op: de break conditie stopt de switch van het verder uitvoeren van de code. Indien je geen break plaatst, wordt alle code tot de volgende break, of het einde van de switch statement, uitgevoerd.
{% endhint %}

In het onderstaande voorbeeld combineren we verschillende waarden.&#x20;

```typescript
let animal: string = "dog";
switch(animal) {
  case "cat":
    console.log("it's a cat!");
    break;
  case "dog":
  case "pug":
  case "labrador":
    console.log("it's a dog!");
    break;
  default:
    console.log("it's neither!");
    break;
}
```

## For

### for(let i...)

Indien je wilt loopen over bepaalde waarden of elementen, is een for loop meestal de beste oplossing. Je hebt een start waarde nodig, een einde conditie, en een bewerking op die startwaarde.

Bv. ik wil alle getallen tussen 0 en 10 afprinten:

```typescript
for(let i=0;i<10;i++){
  console.log(i) // start bij 0
}
```

Ik hoef niet te beginnen met een startwaarde van 0. Ik kan beginnen bij bv. 5

```typescript
for(let i=5;i<10;i++){
  console.log(i) // start bij 5
}
```

Ik hoef ook niet op te tellen. Elke bewerking is mogelijk, zolang we altijd zeker zijn dat de eindconditie kan behaald worden:

```typescript
for(let i=5;i>=0;i--){
  console.log(i) // start bij 5
}
```

{% hint style="danger" %}
Let op: de eindconditie is belangrijk. Trek je bv. 2 getallen af elke loop (i-=2), dan stop de loop hierboven ook, omdat je i>=0 checkt. Maar zou je i === 0 nagaan, dan stopt die nooit. Dit zijn de waarden van i:

5 - 3 - 1 - (-1) - (-3)

i === 0 wordt nooit bereikt. Let dus ook op nooit i === array.length te gebruiken, maar altijd i < array.length
{% endhint %}

### for ... of

Loopen over een array kan met een simpele for statement. Bv.

```typescript
let numbers: Array<number> = [1,3,5];
for(let i=0;i<numbers.length;i++){
  console.log(numbers[i]);
}
```

Dankzij de for..of statement kan dit makkelijker!

```typescript
let numbers: Array<number> = [1,3,5];
for(let el of numbers){
  console.log(el);
}
```

Dit werkt ook met strings!

```typescript
let name: string = "Sven";
for(let el of name){
  console.log(el);
}
```

### for ... in

Soms heb je niet alleen de elementen nodig, maar ook de index. Waar het element zich bevindt. Dit kan je doen met for..in

```typescript
let numbers: Array<number> = [1,3,5];
for(let el in numbers){
  console.log(el); // print de index
  console.log(numbers[el]); //print het element
}
```

## Break

Break kan ook gebruikt worden bij andere statements, zoals de while en for loops:

```typescript
let numbers: Array<number> = [111,12,13,114,115];
for(let n of numbers){
  if(n === 12){
    break;
  }
  console.log(n);
}
```

Wanneer n === 12 zal de for loop stoppen. De code na de break wordt niet meer uitgevoerd. De loop zal ook niet verder itereren over de andere elementen.

## Continue

Continue onderbreekt de loop maar start de volgende iteratie. Ipv de loop volledig te stoppen, wordt de rest van de code in de loop niet meer uitgevoerd voor deze iteratie. Je "skipt" dus de rest van de code en gaat verder naar de volgende iteratie.

```typescript
let numbers: Array<number> = [111,12,13,114,115];
for(let n of numbers){
  if(n === 12){
    continue;
  }
  console.log(n);
}
```

Wanneer n === 12 wordt console.log(n) voor 12 niet uitgevoerd. We gaan wel verder naar element 13, 114, 115.
