# TypeScript: Arrays

Arrays laten toe verschillende elementen te bewaren in een lijst. Een array heeft een lengte maar kan langer en korter worden.&#x20;

Een lege array initialiseren doe je zo:

```typescript
let score: number[] = [];
```

Dit initialiseert een array score met geen elementen. De lengte is dus 0. Het type number\[] bepaalt dat elementen enkel van het type number mogen zijn. Je kan dit ook zo schrijven:

```typescript
let score: Array<number> = [];
```

Bij initialisatie kan je ook elementen meegeven:

```typescript
let score: number[] = [19,14,20,13];
```

Nu heeft mijn array lengte 4. Je kan de lengte opvragen met:

```typescript
score.length
```

In TypeScript zijn we niet beperkt tot 1 type per array. Je kan bv. een array maken met verschillende types. Dan moet elk element voldoen aan 1 van de types die bepaald zijn:

```typescript
let a: Array<number | string> = [1,"hey",3]; 
let b: Array<number | string | boolean> = [true, 2, false, "test"];
```

Elementen opvragen van een array doe je adhv \[x] waar x de positie is in de array. Het eerste element bevindt zich op positie 0. Het laatste element op positie "array length - 1".

```typescript
const names: Array<string> = ["George","Geoffrey","John"];
console.log(names[0]); // George
console.log(names[1]); // Geoffrey
console.log(names[2]); // John
console.log(names[3]); // undefined - hier staat geen element! 
```

Zo kunnen we ook waarden aanpassen in onze array:

```typescript
const names: Array<string> = ["George","Geoffrey","John"];
console.log(names[0]); // George
names[0] = "Jane";
console.log(names[0]); // Jane
```

We kunnen ook items achteraan toevoegen aan de array:

```typescript
let a: Array<number> = [1,2,3];
a.push(4);
a.push(9);
console.log(a); // [1,2,3,4,9]
```

{% hint style="danger" %}
De lengte van een array past zich aan aan het aantal elementen die de array bevat. In dit voorbeeld is a.length 3. Maar na 2 pushes is a.length 5
{% endhint %}

We kunnen ook het achterste element verwijderen:

```typescript
let a: Array<number> = [1,2,3];
a.pop();
a.pop();
console.log(a); // [1]
```

{% hint style="info" %}
Ipv push en pop, kan je ook shift en unshift gebruiken. Shift verwijdert het eerste element. Unshift voegt een element vooraan toe.&#x20;
{% endhint %}

