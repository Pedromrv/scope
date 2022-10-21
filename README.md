# Scope

Si le pides a la empleada de la tienda de teléfonos un modelo de teléfono que no tiene en su tienda, no podrá venderte el teléfono que quieres. Sólo tiene acceso a los teléfonos del inventario de su tienda. Tendrás que probar en otra tienda para ver si puedes encontrar el teléfono que buscas.

La programación tiene un término para este concepto: scope (técnicamente llamado ámbito léxico). En JavaScript, cada función tiene su propio ámbito(scope). El ámbito es básicamente una colección de variables, así como las reglas para el acceso a esas variables por nombre. Sólo el código dentro de esa función puede acceder a las variables de alcance de esa función.
El nombre de una variable tiene que ser único dentro del mismo ámbito, no puede haber dos variables a diferentes una al lado de la otra. Pero el mismo nombre de variable a puede aparecer en diferentes ámbitos:

```javascript
function one() {  
// this `a` only belongs to the `one()` function 
let a = 1;  
console.log( a );

}

function two() {  
// this `a` only belongs to the `two()` function 
let a = 2;  
console.log( a );

}  
one(); // 1

two(); // 2
```

Además, un scope puede estar anidado dentro de otro scope, al igual que si un payaso en una fiesta de cumpleaños infla un globo dentro de otro globo. Si un scope está anidado dentro de otro, el código dentro del ámbito más interno puede acceder a las variables de cualquier ámbito.

Considere:
```javascript
function outer() { 

	let a = 1;

	function inner() { 
	
		let b = 2;

	    // we can access both `a` and `b` here

		console.log( a + b ); // 3 
	}

	inner();

    // we can only access `a` here

	console.log( a ); // 1 
}

outer();
```

Las reglas de ámbito léxico dicen que el código de un scope puede acceder a variables de ya sea ese scope o cualquier scope fuera de él.
Por lo tanto, el código dentro de la función inner() tiene acceso a ambas variables a y b, pero el código sólo en outer() tiene acceso sólo a a-no puede acceder a b porque esa variable sólo está dentro de inner().

Recuerda este fragmento de código de antes:
```javascript
const TAX_RATE = 0.08;

function calculateFinalPurchaseAmount(amt) { 
	// calculate the new amount with the tax 
	amt = amt + (amt * TAX_RATE);

    // return the new amount
	return amt; 
}
```

La TAX_RATE  constant es accesible desde dentro de la función 
calculateFinalPurchaseAmount(..), aunque no la hayamos pasado, debido al ámbito léxico.

## Práctica

No hay absolutamente ningún sustituto para la práctica en el aprendizaje de la programación. Ninguna cantidad de escritos elocuentes de mi parte va a convertirte en un programador.
Teniendo esto en cuenta, vamos a intentar practicar algunos de los conceptos que hemos aprendido en este capítulo. Yo daré los "requisitos" y tú lo intentarás primero. Luego consulta el listado de código de abajo para ver cómo lo he enfocado:
- Escribe un programa que calcule el precio total de tu compra de teléfonos. Seguirás comprando teléfonos (pista: ¡bucle!) hasta que te quedes sin dinero en tu cuenta bancaria. También comprará accesorios para cada teléfono siempre que el importe de la compra esté por debajo de su umbral de gasto mental.
- Una vez calculado el importe de la compra, añada los impuestos y, a continuación, imprima el importe de la compra calculado, debidamente forrado.
- Por último, comprueba el importe con el saldo de tu cuenta bancaria para ver si te lo puedes permitir o no.
- Deberá establecer algunas constantes para el "tipo impositivo", el "precio del teléfono", el "precio de los accesorios" y el "umbral de gasto", así como una variable para el "saldo de su cuenta bancaria".
- Debe definir funciones para calcular el impuesto y para formar el precio con un "$" y redondear a dos decimales.


- Desafío adicional: Intenta incorporar la entrada de datos en este programa, quizás con el prompt(..) cubierto en "Entrada de datos" en la página 6. Por ejemplo, puede pedirle al usuario el saldo de su cuenta bancaria. Diviértase y sea creativo.

Bien, adelante. Pruébalo. No mires mi solución hasta que lo hayas probado tu mismo.

SOLUCIÓN:
```javascript
const SPENDING_THRESHOLD = 200; 
const TAX_RATE = 0.08;  
const PHONE_PRICE = 99.99; 
const ACCESSORY_PRICE = 9.99;

let bank_balance = 303.91; 
let amount = 0;

function calculateTax(amount) { 
	return amount * TAX_RATE;
}

function formatAmount(amount) { 
	return "$" + amount.toFixed( 2 );
}

// keep buying phones while you still have money

while (amount < bank_balance) { 
	// buy a new phone!  
	amount = amount + PHONE_PRICE;
	
	// can we afford the accessory?
	if (amount < SPENDING_THRESHOLD) { 
	amount = amount + ACCESSORY_PRICE;
	}
}

// don't forget to pay the government, too
amount = amount + calculateTax( amount );

console.log(
        "Your purchase: " + formatAmount( amount )

);
// Your purchase: $334.76

// can you actually afford this purchase?

if (amount > bank_balance) { 
	console.log(
		"You can't afford this purchase. :("

	); 
}

    // You can't afford this purchase. :(
    ```

## Review

Aprender a programar no tiene por qué ser un proceso complejo y abrumador. Sólo hay unos cuantos conceptos básicos que debes entender.
Estos actúan como bloques de construcción. Para construir una torre alta, primero se empieza poniendo bloque sobre bloque sobre bloque. Lo mismo ocurre con la programación. Estos son algunos de los bloques de construcción esenciales de la programación:
- Necesitas operadores para realizar acciones.
- Necesitas valores y tipos para realizar diferentes tipos de acciones como las matemáticas en los números o la salida con cadenas.
- Necesitas variables para almacenar datos (estado) durante la ejecución de tu programa.
- Necesitas condicionales como las sentencias if para tomar decisiones.
- Necesita bucles para repetir tareas hasta que una condición deje de ser verdadera.
- Necesitas funciones para organizar tu código en trozos lógicos y reutilizables.

Los comentarios en el código son una forma eficaz de escribir un código más legible, lo que hace que su programa sea más fácil de entender, mantener y arreglar más tarde si hay problemas.
Por último, no descuides el poder de la práctica. La mejor manera de aprender a escribir código es escribiendo código.

Me alegro de que estéis en camino de aprender a codificar. Seguid así. No olvidéis consultar otros recursos de programación para principiantes (libros, blogs, formación online, etc.). 
