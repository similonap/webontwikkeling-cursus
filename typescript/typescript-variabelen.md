# TypeScript: Variabelen

## Benaming van variabelen

Variables zijn hoofdletter gevoelig. In het onderstaande voorbeeld zijn `amount` en `Amount` niet dezelfde variables

```typescript
let amount: number = 5;
let total: number = Amount + 5; // ERROR
```

Kies altijd voor duidelijke benamingen van jouw variabelen. Let wel op, gebruik enkel letters, cijfers en underscores (\_). Je kan een variabel niet starten met een cijfer.

```typescript
let amount1: number = 3;
let amount_2: number = 5;
let 3amount: number = 7; // ERROR
```

Soms wil je een variabel die niet mag veranderd worden, bv. indien je nood hebt aan een maximum of minimum waarde.

```typescript
let myAge: number = 13;
myAge = 14;

const minimumDrinkingAge: number = 16;
minimumDrinkingAge = 10; // ERROR
```

Let wel op bij het gebruik van arrays. Const zorgt dat je geen nieuwe array aan die variabel kan geven. Maar de inhoud kan wel veranderen.

```typescript
const a: Array<number> = [1,2,3];
a[0] = 3; // OK
a = [2,3,4]; // ERROR
```

