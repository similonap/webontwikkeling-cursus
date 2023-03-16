# TypeScript: Scope

Variabelen "leven" binnen een bepaalde scope. Buiten deze scope zijn ze niet toegankelijk.&#x20;

In onderstaand voorbeeld is n beschikbaar buiten en binnen de if structuur:

```typescript
let n: number = 1;
if(true){
  console.log(n); // === 1
}
console.log(n); // === 1
```

De scope van de variabele is dus inclusief alle structuren die zich in de scope bevinden:

```typescript
let n: number = 1;
if(true){
  if(true{
    console.log(n); // === 1
  }
}
console.log(n); // === 1
```

Ze is niet beschikbaar buiten haar scope. Dwz, buiten de { } waarbinnen de variabele gedefinieerd is:

```typescript
if(true){
  let n: number = 1;
  console.log(n); // === 1
}
console.log(n); // ERROR
```

Een andere if statement heeft ook geen toegang tot deze variabele:

```typescript
if(true){
  let n: number = 1;
  console.log(n); // === 1
}
console.log(n); // ERROR
if(true){
  console.log(n); // ERROR
}
```

De variabele is dus enkel beschikbaar binnen de { } waar ze gedefinieerd staat.

{% hint style="info" %}
Je zal misschien al opgemerkt hebben dat een variabele in een ander bestand soms een conflict geeft met jouw huidig bestand. Bv. oefening1.ts bevat de variabele i, oefening2.ts kan nu geen gebruik maken van die variabele.

Gebruik volgende statement om dit probleem te voorkomen (bv. op einde van jouw bestand)\
`exports {}`
{% endhint %}

{% hint style="danger" %}
Gebruik altijd let en const. Nooit var:
{% endhint %}

```typescript
var n: number = 1;
if(true){
  var n: number = 2;
  console.log(n); // === 2
}
console.log(n); // 2
if(true){
  console.log(n); // 2
}
```
