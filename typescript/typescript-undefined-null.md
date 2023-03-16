# TypeScript: Undefined, null

Wanneer een variabel niet geinitialiseerd is, krijgt die de waarde undefined:

```typescript
let a: number;
let b: string;
let c: number[];
console.log(a); // undefined
console.log(b); // undefined
console.log(c); // undefined
```

Zorg dat je altijd een waarde geeft vooraleer je de variabel gebruikt:

```typescript
let a: number;
a++; // ERROR
let b: number;
b = 3;
b++; // OK
let c: number = 4;
c++; // OK
```

Je kan ook een variabel initialiseren met null. Dit wil zeggen dat de variabel geen waarde bevat:

```typescript
let a: number = null;
console.log(a); // null
```
