# TypeScript: Tuples

Tuples laten ons toe verschillende elementen aan 1 variabel toe te wijzen. Het lijkt erg op een array, maar heeft een vaste lengte en volgorde van types.

```typescript
let a: [number, string] = [1, "Sven"];
let b: [boolean, string, boolean] = [true, "Hallo", false];
let c: [number, string] = ["Sven", 1]; // ERROR
let d: [number, boolean] = [1, false, 1]; // ERROR
```

{% hint style="info" %}
Arrays kunnen ook verschillende types bevatten. Het aantal van die types en volgorde is niet bepaald. Bij tuples moet je exact volgen wat er tussen \[] staat.&#x20;

Bv. \[number, string] zegt dat het eerste element een number moet zijn. Het tweede element moet een string zijn.
{% endhint %}

