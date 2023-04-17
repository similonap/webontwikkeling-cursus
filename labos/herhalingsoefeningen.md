# Herhalingsoefeningen

### **Lussen, interfaces en functies**

**1)** Maak een functie `zoekGetal` die in een getal zoekt in de volgende array. Deze functie geeft de index terug waar het getal zich bevindt. Als het getal niet gevonden wordt geef dan -1 terug. **Gebruik een for loop!**

```typescript
let getallen : number[] = [1,3,5,7,9,13];
```

de functie heeft de volgende interface

```javascript
interface ZoekGetal {
    (getallen: number[], getal: number): number
}
```

**2)** Maak nu een functie `zoekPersonenMetLeeftijd` die in de volgende array van personen gaat zoeken.  Deze  functie geeft de persoon terug (of meerdere) met een bepaalde leeftijd.

```javascript
interface Person {
    name: string,
    age: number
}
let personen: Person[] = [
    {
        name: 'Andie',
        age: 36
    },
    {
        name: 'Donald',
        age: 76
    },
    {
        name: 'Joe',
        age: 78
    },
    {
        name: 'Bompa',
        age: 75
    },
]
```

de functie heeft de volgende interface

```javascript
interface ZoekPersonenMetLeeftijd {
    (personen: Person[], leeftijd: number): Person[]
}
```

**3)** Maak een functie `berekenGemiddeldeLeeftijd` met de volgende interface

```javascript
interface BerekenGemiddeldeLeeftijd {
    (personen: Person[]): number
}
```

**Gebruik een for loop!**

4\) Maak een functie `zoekPersoonMetHoogsteLeeftijd` met de volgende interface

```javascript
interface ZoekPersoonMetHoogsteLeeftijd { 
    (personen: Person[]): Person
}
```

**Gebruik een for loop!**

### **Functies doorgeven en callbacks**

**1)** Maak een functie printAllePersonen met de volgende interface

```javascript
interface PrintAllePersonen {
    (personen: Person[]): void
}
```

zorg ervoor dat deze functie de personen afprint met **console.log** op de volgende manier

```
Andie 36
Donald 76
Joe 78
Bompa 75
```

**2)** Maak een functie printAllePersonen2 met dezelfde interface. Deze functie print de personen af op de volgende manier:

```
36 Andie
76 Donald
78 Joe
75 Bompa
```

**3)** Maak een functie printAllPersonen3 met dezelfde interface. Deze functie print de personen af op dezelfde manier als de eerste functie. **Het verschil is hier wel dat de leeftijd van de persoon in het rood moet afgebeeld worden als hij ouder dan 70 is.**

**4)** Maak nu een functie **printNaamDanLeeftijd**, **printLeeftijdDanNaam** en **printPersoonMetKleur** met de volgende interface

```javascript
interface PrintPersoon {
    (persoon: Person): void
}
```

Zorg ervoor dat deze op dezelfde manier als stap 1,2,3 deze persoon wordt afgeprint.

**5)** Verander nu de `printAllePersonen` functie zodat je ook een 2de parameter aanvaard. Deze parameter is een `PrintPersoon` functie. Vorm nu de `printAllPersonen` functie om zodat die deze `PrintPersoon` functie gebruikt om de personen af te printen. Zo kan je de 3 verschillende functies van 1,2 en 3 als 1 functie schrijven zonder dubbele code. De functie zal dan de volgende interface krijgen

```typescript
interface PrintAllePersonen {
    (personen: Person[], printPersoon: PrintPersoon): void
}
```

**6)** Schrijf nu deze 3 printPerson functies als een anonieme functies.

### **Map/Filter/Reduce/Sort**

**1)** Schrijf een functie om alle personen te sorteren met de volgende interface

```
interface SortPersonen {
    (personen: Person[]): Person[]
}
```

**2)** Pas `zoekGetal` aan zodat het gebruik maakt van filter.

**3)** Pas `zoekPersonenMetLeeftijd` aan zodat het gebruik maakt van filter

**4)** Pas berekenGemiddeldeLeeftijd aan zodat het gebruik maakt van reduce

**5)** Pas zoekPersoonMetHoogsteLeeftijd aan zodat het gebruik maakt van reduce



