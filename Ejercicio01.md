# Ejercicio 1 (Muy básico: 1 jugador, 3 dientes, 1 dañado)

## Enunciado

1. Crea un array `dientes` con **3** elementos, todos `0`.  
2. Selecciona una posición al azar para poner un `1` (diente dañado).  
3. Crea un array `visibles` de 3 `"🦷"`.  
4. Un solo jugador elige índices (0, 1, 2).  
   - Si descubre el diente dañado, pon `"💥"` y termina el juego con **"¡El cocodrilo mordió!"**.  
   - Si descubre un diente sano, cámbialo a `"✅"`.  
5. Si el jugador presiona los **2** dientes sanos sin tocar el dañado, **gana**.

## Código (JavaScript)

```html
<script>
    // 1. Array con 3 dientes sanos
    const dientes = [0, 0, 0];

    // 2. Posición aleatoria para el diente dañado
    const posicionDaniada = Math.floor(Math.random() * 3);
    dientes[posicionDaniada] = 1;

    // 3. Array visible
    const visibles = ["🦷", "🦷", "🦷"];

    let juegoTerminado = false;
    let dientesSanosDescubiertos = 0; 
    // Hay 2 dientes sanos (3 - 1)

    while (!juegoTerminado) {
        console.log("Estado visible: " + visibles);

        let seleccion = prompt("Elige un diente (0, 1 o 2):");
        seleccion = Number(seleccion);

        if (visibles[seleccion] !== "🦷") {
            console.log("Ese diente ya fue presionado. Elige otro.");
        } else {
            // ¿Es dañado?
            if (dientes[seleccion] === 1) {
                visibles[seleccion] = "💥";
                console.log("¡El cocodrilo mordió! Has perdido.");
                juegoTerminado = true;
            } else {
                // Diente sano
                visibles[seleccion] = "✅";
                dientesSanosDescubiertos++;

                if (dientesSanosDescubiertos === 2) {
                    console.log("¡Has descubierto todos los dientes sanos! ¡Ganaste!");
                    juegoTerminado = true;
                }
            }
        }
    }

    console.log("Estado final: " + visibles);
</script>
```

# Ejercicio 2 (Un poco mayor: 1 jugador, 4 dientes, 1 dañado)

## Enunciado
1. Crea un array `dientes` de **4** elementos (todos `0`).  
2. Selecciona al azar **1** posición para el diente dañado (`1`).  
3. Crea un array `visibles` de 4 `"🦷"`.  
4. Un único jugador elige índices (0 a 3).  
   - Si encuentra el diente dañado, se muestra `"💥"` y termina el juego con **"¡El cocodrilo mordió!"**.  
   - Si es sano, se pone `"✅"`.  
5. Gana si descubre los **3** dientes sanos.

## Código (JavaScript)

```html
<script>
    // 1. Array de 4 dientes sanos
    const dientes = [0, 0, 0, 0];

    // 2. Posición aleatoria para el diente dañado
    const posicionDaniada = Math.floor(Math.random() * 4);
    dientes[posicionDaniada] = 1;

    // 3. Array visible
    const visibles = ["🦷", "🦷", "🦷", "🦷"];

    let juegoTerminado = false;
    let dientesSanosDescubiertos = 0;
    const totalSanos = 3; // 4 - 1

    while (!juegoTerminado) {
        console.log("Estado visible: " + visibles);

        let seleccion = prompt("Elige un diente (0 a 3):");
        seleccion = Number(seleccion);

        if (visibles[seleccion] !== "🦷") {
            console.log("Ese diente ya fue presionado. Elige otro.");
        } else {
            if (dientes[seleccion] === 1) {
                visibles[seleccion] = "💥";
                console.log("¡El cocodrilo mordió! Has perdido.");
                juegoTerminado = true;
            } else {
                visibles[seleccion] = "✅";
                dientesSanosDescubiertos++;

                if (dientesSanosDescubiertos === totalSanos) {
                    console.log("¡Has descubierto todos los dientes sanos! Ganaste.");
                    juegoTerminado = true;
                }
            }
        }
    }

    console.log("Estado final: " + visibles);
</script>
```

# Ejercicio 3 (1 jugador, 5 dientes, entre 1 y 2 dañados)

## Enunciado
1. Crea un array `dientes` de **5** elementos (todos `0`).  
2. Escoge entre **1 y 2** dientes para dañar, de manera aleatoria, y colócalos con un bucle `while` que ponga `1` en posiciones distintas del array.  
3. Genera el array `visibles` de 5 `"🦷"`.  
4. Un solo jugador intenta descubrir todos los sanos:
   - Si presiona un diente dañado, aparece `"💥"` y **pierde** inmediatamente.  
   - Si logra presionarlos todos sin tocar un dañado, **gana**.

## Código (JavaScript)

```html
<script>
    // 1. Array de 5 dientes sanos
    const dientes = [0, 0, 0, 0, 0];

    // 2. Número aleatorio de dientes dañados entre 1 y 2
    let cantidadDaniados = Math.floor(Math.random() * 2) + 1;
    let daniadosColocados = 0;

    while (daniadosColocados < cantidadDaniados) {
        let pos = Math.floor(Math.random() * dientes.length);
        if (dientes[pos] === 0) {
            dientes[pos] = 1;
            daniadosColocados++;
        }
    }

    // 3. Array visible
    const visibles = ["🦷", "🦷", "🦷", "🦷", "🦷"];

    let juegoTerminado = false;
    let sanosPresionados = 0;
    const totalSanos = dientes.length - cantidadDaniados; // 5 - (1 ó 2)

    while (!juegoTerminado) {
        console.log("Estado visible: " + visibles);

        let seleccion = prompt("Elige un diente (0 a 4):");
        seleccion = Number(seleccion);

        if (visibles[seleccion] !== "🦷") {
            console.log("Ese diente ya fue presionado. Elige otro.");
        } else {
            if (dientes[seleccion] === 1) {
                visibles[seleccion] = "💥";
                console.log("¡El cocodrilo mordió! Perdiste.");
                juegoTerminado = true;
            } else {
                visibles[seleccion] = "✅";
                sanosPresionados++;

                if (sanosPresionados === totalSanos) {
                    console.log("¡Has descubierto todos los dientes sanos! Ganaste.");
                    juegoTerminado = true;
                }
            }
        }
    }

    console.log("Estado final: " + visibles);
</script>
```

# Ejercicio 4 (2 jugadores, 3 dientes, 1 dañado)

## Enunciado
1. Hay **2 jugadores** y **3 dientes**.  
2. Exactamente **1** diente se daña (posición aleatoria en el array).  
3. Los jugadores alternan turnos (jugador 1, luego jugador 2, etc.).  
4. Si un jugador presiona el diente dañado, sale `"💥"` y ese jugador pierde de inmediato.  
5. Si consiguen descubrir los **2** dientes sanos, ambos ganan.

## Código (JavaScript)

```html
<script>
    // 1. Array de 3 (todos 0)
    const dientes = [0, 0, 0];

    // 2. Posición aleatoria para el diente dañado
    const posicionDaniada = Math.floor(Math.random() * 3);
    dientes[posicionDaniada] = 1;

    // 3. Array visible
    const visibles = ["🦷", "🦷", "🦷"];

    let jugadorActual = 1;
    let juegoTerminado = false;
    let sanosPresionados = 0; // hay 2 sanos

    while (!juegoTerminado) {
        console.log("Estado visible: " + visibles);
        console.log("Turno del jugador " + jugadorActual);

        let seleccion = prompt("Jugador " + jugadorActual + ", elige (0, 1 o 2):");
        seleccion = Number(seleccion);

        if (visibles[seleccion] !== "🦷") {
            console.log("Ese diente ya fue presionado. Elige otro.");
        } else {
            if (dientes[seleccion] === 1) {
                visibles[seleccion] = "💥";
                console.log("¡El cocodrilo mordió! Jugador " + jugadorActual + " pierde.");
                juegoTerminado = true;
            } else {
                visibles[seleccion] = "✅";
                sanosPresionados++;

                if (sanosPresionados === 2) {
                    console.log("¡Han descubierto todos los dientes sanos! Ambos jugadores ganan.");
                    juegoTerminado = true;
                }
            }

            // Cambiar turno si el juego sigue
            if (!juegoTerminado) {
                if (jugadorActual === 1) {
                    jugadorActual = 2;
                } else {
                    jugadorActual = 1;
                }
            }
        }
    }

    console.log("Estado final: " + visibles);
</script>
```

# Ejercicio 5 (2 jugadores, 5 dientes, entre 1 y 2 dañados)

## Enunciado
1. **2 jugadores** y **5 dientes**.  
2. Entre **1 y 2** de esos dientes estarán dañados, colocados de forma aleatoria.  
3. Cada turno, un jugador elige un índice (0 a 4).  
   - Si elige un diente dañado, se muestra `"💥"` y ese jugador pierde; fin del juego.  
   - Si es un diente sano, se cambia a `"✅"`.  
4. Si logran presionar todos los dientes sanos, ambos ganan.

## Código (JavaScript)

```html
<script>
    // 1. Array de 5 dientes
    const dientes = [0, 0, 0, 0, 0];

    // 2. Elige 1 ó 2 dientes dañados
    let cantidadDaniados = Math.floor(Math.random() * 2) + 1;
    let daniadosColocados = 0;

    while (daniadosColocados < cantidadDaniados) {
        let pos = Math.floor(Math.random() * dientes.length);
        if (dientes[pos] === 0) {
            dientes[pos] = 1;
            daniadosColocados++;
        }
    }

    // 3. Array visible
    const visibles = ["🦷", "🦷", "🦷", "🦷", "🦷"];

    let jugadorActual = 1;
    let juegoTerminado = false;

    const totalSanos = 5 - cantidadDaniados;
    let sanosPresionados = 0;

    while (!juegoTerminado) {
        console.log("Estado visible: " + visibles);
        console.log("Turno del jugador " + jugadorActual);

        let seleccion = prompt("Jugador " + jugadorActual + ", elige un diente (0 a 4):");
        seleccion = Number(seleccion);

        if (visibles[seleccion] !== "🦷") {
            console.log("Ese diente ya fue presionado. Elige otro.");
        } else {
            if (dientes[seleccion] === 1) {
                visibles[seleccion] = "💥";
                console.log("¡El cocodrilo mordió! Jugador " + jugadorActual + " pierde.");
                juegoTerminado = true;
            } else {
                visibles[seleccion] = "✅";
                sanosPresionados++;

                if (sanosPresionados === totalSanos) {
                    console.log("¡Todos los dientes sanos han sido presionados! Ambos jugadores ganan.");
                    juegoTerminado = true;
                }
            }

            // Cambiar turno si no ha terminado
            if (!juegoTerminado) {
                if (jugadorActual === 1) {
                    jugadorActual = 2;
                } else {
                    jugadorActual = 1;
                }
            }
        }
    }

    console.log("Estado final: " + visibles);
</script>

