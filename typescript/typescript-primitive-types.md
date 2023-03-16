# TypeScript: Primitive Types

## Primitive types

Onder primitieve types vallen:

* number
* bigint
* string
* boolean

```typescript
let b: boolean = true; // boolean
let n: number = 3.4; // number
let i: bigint  = 3n; // big integer
let s: string = "hallo";
```

Let op: we gebruiken bijna altijd number ipv bigint (enkel voor zeer grote getallen).

Merk op het verschil met JavaScript: een variabel heeft altijd een bepaalde type. Die geef je mee door : _typename_ achter jouw variabel te plaatsen (enkel bij het definiëren van de variabel!)

```typescript
let b: boolean;
let n: number;
let i: bigint;
let s: string;
```

Strings kunnen op verschillende manieren een waarde krijgen:

```typescript
let naam: string = "Sven";
```

Hier gebruiken we de dubbele quotes om een waarde te geven.

```typescript
let familieNaam: string = 'Charleer';
```

Enkele quotes werken ook!

Maar we kunnen heel wat meer indien we **`` ` ``** (backtick) gebruiken. \
Let op, dit is niet een single quote**`'`**.

```typescript
let zin: string = `Hallo ik ben ${naam} ${familieNaam}.`;
```

Met behulp van de `` ` `` en `${naam.van.variabel}` kunnen we de waarden van andere variabelen in onze string gebruiken.&#x20;

Dit laat ons ook toe "breaks" in onze variabel te gebruiken:

```typescript
let zin2: string = `Hallo ik ben...

ik ben ${naam}.`;
```
