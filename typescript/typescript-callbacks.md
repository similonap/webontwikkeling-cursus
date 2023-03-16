# TypeScript: Callbacks

Functies kan je oproepen in andere functies:

```typescript
let printOutput = (output:number):void => {
	console.log(output)
};

let add = (a:number,b:number):void => {
	printOutput(a + b);
}

add(1,2);
```

De functie printOutput is beschikbaar in de global scope en ook binnen de scope van de functie `add`.

De functie add is wel volledig afhankelijk van printOutput. Via callbacks kunnen we die logica loskoppelen en toch nog gebruik maken van printOutput zonder dat add die rechtstreeks aanspreekt:

```typescript
interface ResultHandler {
    (output:number):void
}
 
let printOutput: ResultHandler = (output:number):void => {
	console.log(output)
};

let add = (a:number, b:number, handleResult: ResultHandler):void => {
	let c:number = a+b;
        handleResult(c);
}

add(1,2,printOutput);
```

Merk op:

* \[lijn 1] we hebben een interface ResultHandler aangemaakt voor printOutput. Deze interface zegt dat een functie van dit type 1 parameter (type number) nodig heeft, en niets teruggeeft (void).
* \[lijn 9] dit laat ons toe een 3e parameter toe te voegen aan add van het type ResultHandler
* \[lijn 9] deze 3e parameter verwacht dus een functie. Welke functie? Een functie zoals bv. printOutput
* \[lijn 11] de 3e parameter bevat een functie van het type ResultHandler. Je kan die functie dus oproepen door handleResult(...) op te roepen
* \[lijn 14] printOutput wordt meegegeven als 3e parameter. Die bevat dus printOutput.
* \[lijn 11] handleResult bevat dus printOutput. handleResult(..) voert dus printOutput(...) uit!

Nu kan add gebruik maken van elke functie die overeenkomt met deze interface. De code is onafhankelijk! Andere ontwikkelaars kunnen makkelijk de functionaliteit van add aanpassen door gewoon een andere callback functie mee te geven.

Je kan ook de functie direct in de functie call definiëren:

```typescript
interface ResultHandler {
    (output:number):void
}
 
let add = (a:number, b:number, handleResult: ResultHandler):void => {
	let c:number = a+b;
    handleResult(c);
}

add(1,2,(output)=>{console.log(output)});
```

We hadden hier dus geen nood aan een aparte variabele printOutput. De inhoud van deze functie werd gewoon direct meegegeven aan add.

## Functies als return waarde

We kunnen ook functies teruggeven als return waarde van een functie. Let op, we hebben hier ook een interface voor nodig:

```typescript
interface Calculation {
    (a:number, b:number):number
};
let multiplyOrDivide = (action:string):Calculation => {
	if(action === 'multiply'){
		return (a,b) => {return a*b;};
	}
	else if(action === 'divide'){
		return (a,b) => {return a/b;};
	}
    return (a,b) => {return -1};
}

let multiply: Calculation = multiplyOrDivide('multiply');
let divide: Calculation = multiplyOrDivide('divide');
let a: number = multiply(2,2);
let b: number = divide(2,2);
```

De functie multiplyOrDivide heeft als return type het type Calculation: dit is een functie met 2 parameters en 1 return waarde. Deze functie geeft dus een functie terug.

Op lijn 6, 9 en 11 zie je voorbeelden van deze return waarde:&#x20;

* lijn 6 geeft (a,b) => {return a\*b}
* lijn 9 geeft (a,b) => {return a/b} terug
* lijn 6 geeft (a,b) => {return -1} terug

Wanneer je de functie multiplyOrDivide uitvoert, dan krijg je dus 1 van de bovenstaande functies terug. De variabelen multiply en divide bevatten dus functies die je kan uitvoeren (zie lijn 16 en 17).
