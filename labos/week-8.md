# Week 8



DAG studenten: Pushen naar Github VOOR vrijdag 23/4/2021 23:59\
AVOND studenten: Pushen naar Github VOOR zondag 25/4/2021 23:59

## Setup

Maak een folder `Labo7` in jouw webontwikkeling folder aan. Maak daar een bestand aan dat noemt `oefening1.ts`en commit/push die file, en **kijk na of je die ook op Github ziet staan!**

{% hint style="info" %}
**Belangrijk:** Na elk stukje code dat je schrijft, test je jouw code. Wanneer die werkt, commit je die code! Zo kan je altijd terugkeren naar een werkende versie, en kunnen wij ook jouw vooruitgang volgen.
{% endhint %}

{% hint style="info" %}
**Belangrijk**: We werken met **TypeScript**. Type dus ook alle variabelen en functies
{% endhint %}

{% hint style="info" %}
**Belangrijk:** Vergeet niet `tsc --init` en `npm install @types/node` te doen voor het project te initialiseren.
{% endhint %}

## Oefening 1: Promises

Deze oefening maak je in bestand `oefening1.ts`.

```typescript
const slowSum = (a: number, b: number) => {
    return new Promise<number>((resolve, reject) => {
        setTimeout(() => {
            resolve(a+b);
        },1000)
    });
}

const slowMult = (a: number, b: number) => {
    return new Promise<number>((resolve, reject) => {
        setTimeout(() => {
            resolve(a*b);
        },1500)
    });
}
```

Dit zijn 2 functies die een promise terug geven. Ze simuleren een trage som functie en een trage vermenigvuldigings functie.

1. Roep de `slowSum` functie aan met de getallen 1 en 5 en zorg dat ze het resultaat van deze functie op het scherm laat zien. (zie output)
2. Roep de `slowSum` functie opnieuw aan met de getallen 1 en 5 maar zorg deze keer dat na het optellen de vermenigvuldigings functie \``slowMult` wordt aangeroepen dat het resultaat vermenigvuldigd met 2 en dan op het scherm laat zien. (zie output)
3. Maak een eigen `slowDiv` functie dat een deling doet (laat deze 2000 milliseconden duren). Zorg ervoor dat als je een deling door nul doet dat je de promise afkeurt met de melding "You cannot divide by zero".
4. Roep deze functie aan met de getallen 6 en 3 en laat het resultaat op het scherm zien. (zie output)
5. Roep deze functie aan met de getallen 6 en 0 en laat de error op het scherm zien. (zie output)

**Verwachte output:**

```
➜  ts-node oefening1.ts
You cannot divide by zero
1 + 5 = 6
(6 / 3) = 2
(1 + 5) * 2 = 12
```

{% hint style="info" %}
Gebruik .then(...) om iets uit te voeren nadat de promise klaar is.
{% endhint %}

## **Oefening 2: Promises en fetch**

Deze oefening maak je in bestand `oefening2.ts`.&#x20;

Installeer de dependency node-fetch:

```
npm install node-fetch
```

Maak gebruik van `Promise.all` om de drie volgende cocktails via de cocktail api met de volgende ids in te lezen: **11000**, **11001**, **11002** en vervolgens de naam van de drie cocktails op het scherm te laten zien.

Je kan een cocktail via een id via de volgende api call binnenhalen:

```
https://www.thecocktaildb.com/api/json/v1/1/lookup.php?i=11000
```

**Verwachte output:**

```
Mojito
Old Fashioned
Long Island Tea
```

## Oefening 3: Async/await

Deze oefening maak je in bestand `oefening3.ts`.&#x20;

```
fetch('https://icanhazdadjoke.com/search?term=dog&limit=5&page=1', {
   headers: {
     'Accept': 'application/json'
   }
})
```

Gebruik de bovenstaande API call om alle moppen op het scherm te laten zien waar het woord 'dog' in voor komt. Je begint op de eerste pagina, en dan laad je de volgende in, en dan de volgende,... tot er geen moppen meer zijn.

**Opgelet:** In dit labo is het verplicht om de **async/await** werkwijze te gebruiken.&#x20;

**Verwachte output:**

```
Me: If humans lose the ability to hear high frequency volumes as they get older, can my 4 week old son hear a dog whistle?

Doctor: No, humans can never hear that high of a frequency no matter what age they are.

Me: Trick question... dogs can't whistle.
Why did the cowboy have a weiner dog? Somebody told him to get a long little doggy.
I adopted my dog from a blacksmith. As soon as we got home he made a bolt for the door.
“My Dog has no nose.” “How does he smell?” “Awful”
what do you call a dog that can do magic tricks? a labracadabrador
My dog used to chase people on a bike a lot. It got so bad I had to take his bike away.
What did the dog say to the two trees? Bark bark.
I went to the zoo the other day, there was only one dog in it. It was a shitzu.
What kind of dog lives in a particle accelerator? A Fermilabrador Retriever.
At the boxing match, the dad got into the popcorn line and the line for hot dogs, but he wanted to stay out of the punchline.
It was raining cats and dogs the other day. I almost stepped in a poodle.
What did the Zen Buddist say to the hotdog vendor? Make me one with everything.
```



Push en commit jouw folder naar Github
