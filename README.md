# JavaScript Calculator 

Este es un proyecto de la plataforma **FreeCodeCamp** del curso **Front-End Development Libraries** para la certificación del programa.




**Objetivo**: Construir una aplicación que sea funcionalmente similar a esta: https://javascript-calculator.freecodecamp.rocks/.

**Requisitos**: Los requisitos para construir la apliación se pueden encontrar en: https://www.freecodecamp.org/espanol/learn/front-end-development-libraries/front-end-development-libraries-projects/build-a-javascript-calculator:
 <br><br>
-------------
### Funcionamiento

La primera constante, `isOperator`, es una función que recibe un parámetro `symbol` de tipo string. Esta función comprueba si el symbol dado es un operador matemático, es decir, si es uno de los siguientes caracteres: `*`, `/`, `+` o `-`. Para hacer esta comprobación, utiliza una expresión regular **/[*/+-]/**, que busca cualquiera de estos caracteres en la cadena symbol. Luego, utiliza el método `.test(symbol)` para verificar si el symbol coincide con la expresión regular. Si coincide, la función devuelve **true**, lo que indica que el symbol es un operador; de lo contrario, devuelve **false**

```javascript
 const isOperator = (symbol: string) =>{
  return /[*/+-]/.test(symbol);
  }
```
<br><br>

La función `buttonPress` maneja el evento de presionar un botón en una calculadora. 
```javascript
  const buttonPress=(symbol:string) =>{

    /*Este caso se activa cuando se presiona el botón "clear" en la calculadora. 
    Dentro de este caso, se establece la respuesta (answer) como una cadena vacía 
    y la expresión (expression) como "0", lo que reinicia la calculadora */
    if(symbol === "clear"){
      setAnswer("");
      setExpression("0");
    }

    /*Este caso se activa cuando se presiona el botón "negative". 
    Verifica si la respuesta es una cadena vacía. Si no lo es, cambia el signo del 
    número en la respuesta. Si el primer carácter de la respuesta es un signo negativo, 
    se elimina; de lo contrario, se agrega un signo negativo delante del número. */
    else if (symbol=== "negative"){
      if(answer==="") return;
      setAnswer(
        answer.toString().charAt(0)=== "-" ? answer.slice(1) : "-" + answer);
    }

    /* Este caso se activa cuando el symbol es un operador (por ejemplo, "+", "-", "*", "/").
     Dentro de este caso, actualiza la expresión (expression) agregando el operador al final de la 
     expresión actual.*/
    else if(symbol==="percent"){
      if(answer==="") return;
      setAnswer((parseFloat(answer)/100).toString());
    }

    /*Este caso se activa cuando se presiona el botón "=" en la calculadora. 
    Invoca la función calculate() para calcular el resultado de la expresión actual.*/
    else if(isOperator(symbol)){
      setExpression(et + " " + symbol + " ")
    }

    /*Este caso se activa cuando se presiona el botón "0". Verifica si el primer carácter 
    de la expresión no es "0". Si no lo es, agrega "0" al final de la expresión actual. */
    else if(symbol === "="){
      calculate();
    }

    /*Este caso se activa cuando se presiona el botón "0". 
    Verifica si el primer carácter de la expresión no es "0". 
    Si no lo es, agrega "0" al final de la expresión actua */
    else if(symbol === "0"){
      if(expression.charAt(0) !== "0"){
        setExpression(expression + symbol);
      }

     /*Este caso se activa cuando se presiona el botón "." (punto decimal). 
     Extrae el último número de la expresión actual y verifica si ya contiene un punto decimal. 
     Si no contiene un punto decimal, agrega un punto decimal al final de la expresión actual */
    }else if(symbol === "."){
      const lastNumber = expression.split(/[-+/*]/g).pop();
      if(!lastNumber) return;

      if(lastNumber?.includes("."))return;
      setExpression(expression + symbol);
      /* Este caso se activa para todos los demás símbolos, es decir, los dígitos del 1 al 9. 
      Verifica si el primer carácter de la expresión es "0". Si lo es, elimina el primer carácter 
      y luego agrega el dígito presionado. Si no es "0", simplemente agrega el dígito presionado 
      al final de la expresión */
    } else{
      if(expression.charAt(0)=== "0"){
        setExpression(expression.slice(1)+symbol);
      }else{
        setExpression(expression + symbol)
      }
    }
    }
```
<br><br>

Por ultimo la funcion `calculate` se compone de 3 partes esenciales

Este if, que comprueba si el último carácter de la expresión (et) es un operador matemático. Si lo es, la función calculate finaliza su ejecución. Luego, divide la expresión en partes individuales, separadas por espacios, y crea un nuevo array vacío (newParts) para almacenar las partes reorganizadas de la expresión.

```javascript
 if(isOperator(et.charAt(et.length - 1))) return;
      const parts = et.split(" ");
      const newParts=[];
```
Este bucle recorre las partes de la expresión en orden inverso. 
Si encuentra un operador `(*, /, +)` seguido por otro operador, reorganiza las partes de la expresión para garantizar el orden correcto de precedencia de las operaciones matemáticas. Esto implica mover los operadores a la parte delantera del array y ajustar el índice del bucle en consecuencia.
```javascript
for(let i =parts.length-1; i>=0; i--){
        if(["*","/","+",].includes(parts[i])&& isOperator(parts[i-1])){
          newParts.unshift(parts[i]);
          let j=0;
          let k= i-1
          while(isOperator(parts[k])){
            k--;
            j++;
          }
          i-=j;
        } else{
          newParts.unshift(parts[i])
        }
      }
```
Aquí, se reconstruye la expresión reorganizada (newExpression) uniendo las partes del array con un espacio en blanco entre cada una. Luego, se evalúa esta expresión utilizando la función eval de JavaScript para calcular el resultado.

```javascript
const newExpression = newParts.join(" ");
      if(isOperator(newExpression.charAt(0))){
        setAnswer(eval(answer + newExpression) as string);
      }else{
        setAnswer(eval(newExpression) as string);
      }
      setExpression("")
```
<br><br>
Link del proyecto desarrollado:
`https://exquisite-bienenstitch-dc984d.netlify.app/`
