# TypeScript: Enum

Een enum (enumerator) gebruik je indien je een aantal vaste waarden wil gebruiken in jouw code. Enums kunnen in vele gevallen nuttig zijn. Een veel gebruikte situatie is status: bv. de status van een gebruiker in een chat programma (online, away, brb) of een speler (alive, dead) etc.

Een enum definieer je als volgt:

```typescript
enum Color {
  Red,
  Green,
  Blue,
}
```

Color is de naam van jouw enum. Red, Green en Blue zijn alle mogelijke waarden.

Je gebruikt jouw enum zoals andere types:

```typescript
let myFavoriteColor: Color;
```

Om jouw variabel van het type Color een waarde te geven, doe je:

```typescript
let myFavoriteColor: Color = Color.Red;
myFavoriteColor = Color.Blue;
```

In de achtergrond houdt TypeScript een getal bij voor elke enum. De eerste waarde zal altijd gelijk zijn aan 0, de tweede 1, enz.

```typescript
Color.Red === 0;
Color.Green === 1;
Color.Blue === 2;
```

We kunnen echter de waarden hiervan aanpassen bij het definiëren van die enum

```typescript
enum Color {
  Red = 5,
  Green,
  Blue,
}
```

Nu start de enum bij 5:

```typescript
Color.Red === 5;
Color.Green === 6;
Color.Blue === 7;
```

We kunnen ook elke enum een aparte waarde geven:

```typescript
enum Color {
  Red = 5,
  Green = 10,
  Blue = 200,
}
```

Soms wil je de string waarde van een enum tonen. Je kan hiervoor de naam van de enum + \[] gebruiken:

```typescript
enum Color {
  Red,
  Green,
  Blue,
}
console.log(Color[0]); // toont Red
console.log(Color[1]); // toont Green
```
