# TypeScript: Objecten

We kunnen verschillende waarden groeperen door gebruik van objecten. Objecten bestaan uit properties waarbij elke property een waarde kan bevatten van een bepaald/ander type:

```typescript
let student = {
  name: "George",
  age: 13,
  siblings: ["Jane","Geoff"],
  alive: true
}
```

Dit object bevat 4 properties: name (een string), age (een number), siblings (een array van strings) en alive (een boolean).

In TypeScript moeten we elke variabel voorzien van een type .Omdat we geen type hebben voor dit specifiek object, moeten we zelf een type voorzien. Hiervoor gebruiken we een interface. Voor objecten definieren we de interface als volgt:

```typescript
interface Student {
  name: string;
  age: number;
  siblings: string[];
  alive: boolean
}
```

{% hint style="info" %}
Een interface voor een object start met het keyword `interface` en dan een naam. Daarna plaatsen we tussen { }  de verschillende properties en hun types.
{% endhint %}

Nu kunnen we bovenstaand object een type geven:

```typescript
let student: Student = {
  name: "George",
  age: 13,
  siblings: ["Jane","Geoff"],
  alive: true
}
```

{% hint style="danger" %}
* Een object van het type Student moet alle properties bevatten die gedefinieerd staan in het interface!
* Een object van het type Student mag geen andere properties bevatten!
{% endhint %}

De volgorde van de properties is onbelangrijk. Bv. dit student object is ook geldig:

```typescript
let student2: Student = {
  alive: true,
  age: 14,
  name: "Jane",
  siblings: ["George","Geoff"],
}
```

## Properties aanspreken

We kunnen elke property individueel aanspreken:

```typescript
let student: Student = {
  name: "George",
  age: 13,
  siblings: ["Jane","Geoff"],
  alive: true
} 
console.log(student.name); // print George
student.age = 15; // verandert de age naar 15
student.siblings.push("Joan"); // voegt een nieuwe sibling "Joan" toe aan de array
```

Elke property kan je dus gebruiken zoals je een variabel aanspreekt/gebruikt.

Omdat een property gewoon data bevat (een string, een number,...), kan een property ook een functie bevatten:

```typescript
let student = {
  name: "George",
  age: 13,
  siblings: ["Jane","Geoff"],
  alive: true,
  showIntroduction: () => {
    console.log("Hello my name is George");
    }
}
student.showIntroduction();
```

De property showIntroduction bevat een functie. Je kan die dus uitvoeren zoals elke andere functie.

{% hint style="info" %}
Let op: de interface komt niet meer overeen met dit object. Je zal de interface moeten aanpassen om de property function te bevatten. Hiervoor heb je een interface nodig die de functie beschrijft. Dit wordt uitgelegd in [TypeScript: Functions](typescript-functions.md#functies-en-types)
{% endhint %}

## Optionele properties

Normaal zijn alle properties verplicht aanwezig:

```typescript
interface Student {
  name: string,
  age: number
}

let student1: Student = {name: "George", age:3}; // OK
let student2: Student = { age:4, name: "Geoff"}; // OK
let student3: Student = { age:5, name: "Jane", location: "Antwerp"}; // ERROR
let student4: Student = {age: 6, location: "Bruges"}; // ERROR
```

Je kan properties optioneel maken door een `?` achter de naam van de property te plaatsen:

```typescript
interface Student {
  name?: string,
  age?: number
}

let student1: Student = {name: "George", age:3}; // OK
let student2: Student = { }; // OK
let student3: Student = { age:5, location: "Antwerp"}; // OK
if(student2.age){
  console.log("hier geraken we niet); // student 2 bevat geen age
}
console.log(student.ag); // ERROR, ag bestaat niet
```

## Readonly properties

Net zoals const een variabel onveranderbaar maakt, kan je zorgen dat een property niet aangepast mag worden. Hiervoor gebruik je het keyword `readonly`

```typescript
interface Student {
  readonly name: string,
  readonly age: number
}
let student1: Student = {name: "George", age:3};
student1.age = 4; // ERROR
```

Je kan dus enkel waarden meegeven bij intialisatie van het object!

## Objecten en functies

Objecten kunnen net zoals elk ander type meegegeven worden als parameters of teruggegeven worden als return waarde.

halloStudent vraagt een parameter van het type Student. Omdat de parameter dat type bevat, kan je ook de properties aanspreken in de functie:

```typescript
interface Student {
  name: string
}

const halloStudent = (student:Student) => {
  console.log("hallo " + student.name); 
}

let student1: Student = {name: "George"};
halloStudent(student1);
```

giveMeGeorge maakt zelf een nieuw object aan dat ie teruggeeft als return waarde:

```typescript
interface Student {
  name: string,
  age: number
}

const giveMeGeorge = ():Student => {
  return {name:"George", age:3};
}

let student1: Student = giveMeGeorge();
console.log(student.name);
console.log(student.age);
```

De return waarde bevat dus een geldig Student object.

## JSON

Wanneer we data via APIs doorsturen of in bestanden opslaan, dan gebruiken we meestal JSON. JSON lijkt er op een JavaScript object, maar de schrijfwijze is een beetje anders.

Dit is een JavaScript object. Die steek je meestal in bv. een variabel:

```typescript
let student = {
  name: "George",
  age: 13,
  siblings: ["Jane","Geoff"],
  alive: true,
  showIntroduction: () => {
    console.log("Hello my name is George");
    }
}
```

JSON steek je meestal in een .json bestand. Bv:&#x20;

```typescript
{
  "name": "George",
  "age": 13,
  "siblings": ["Jane","Geoff"],
  "alive": true
}
```

{% hint style="danger" %}
Merk op:

* in het JSON bestand kan je geen variabelen gebruiken. Je schrijft dus niet let student = ...
* properties hebben quotes nodig rond hun namen. Het is dus `"name"` en niet `name`
* je kan geen functies plaatsen in een JSON bestand. showIntroduction kan dus niet bestaan in het bestand
{% endhint %}
