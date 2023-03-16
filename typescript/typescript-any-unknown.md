# TypeScript: Any, unknown

Als je werkt met JavaScript modules, dan werk je met externe niet getypeerde variabelen. Het kan soms moeilijk zijn om een exact type te definieren in dat geval. TypeScript heeft daarom het type any:

```typescript
let a: any;
a = 1;
a = "hallo";
a = [1,2,3];
```

Aan variabelen van het type any mag je elk type van waarde geven.

{% hint style="info" %}
Gebruik any zo weinig mogelijk.&#x20;
{% endhint %}

Unknown is een ander type dat gelijkaardig is aan any. Echter, de compiler kan hier wat slimmer mee om:

```typescript
let a: unknown;
a = 1;
a = "hallo";
a = [1,2,3];
a = 5;
if(a === 5){
    a += 3;
}
```

Merk op dat a elke waarde mag hebben. Maar wanneer we nakijken of a bv. gelijk is aan 5, dan weet de compiler dat we over een number spreken. In die if statement, zal a bekeken worden als een variabel van het type number.

Je kan de compiler ook expliciet zeggen dat je weet over welk type het gaat:

```typescript
let a: unknown;
let b: number = (a as number);
let c: number = (<number>a);
```

De compiler vertrouwt jouw keuze en zal a accepteren als een number.
