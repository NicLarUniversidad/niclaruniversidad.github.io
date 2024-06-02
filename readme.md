# Cálculo del número PI con el método de Montecarlos

## Método

Se puede calcular el número PI, con una hoja de papel y granos arroz.
Primero, se dibuja un cuadrado en la hoja, y un círculo en el centro del cuadrado, con un diámetro igual a la mitad de los lados del cuadrado.
Luego, se arrojan granos de arroz sobre la hoja y se cuentan cuántos granos cayeron sobre el círculo (Ci) y cuántos sobre el cuadrado (Cu).
Finalmente, se calcula el número PI calculado 

    Cu/Ci * 4

donde Ci son los granos que cayeron sobre el círculo y Cu son los granos que cayeron en el cuadrado (incluyen a los del círculo). 

## Pasos de la simulación

### Paso 0


Se diseñó un modelo donde se representa la hoja de papel con un sistema de coordenadas cartesianas. Se calcula la posición del cuadrado, círculo y de cada arroz en los ejes X e Y. Con el fin de simplificar el modelo los centros del cuadrado/círculo están en el punto (0,0). Y por criterio arbitrario, los vértices del cuadrado están en los puntos (-125,125), (-125,-125), (125,-125) y (125, 125). Mientras que el círculo tiene un radio=125.

### Paso 1


Se calcularon dos números aleatorios para determinar la posición de cada grano de arroz, uno para el eje X y otro para el eje Y. 

### Paso 2


Se transformó el número aleatorio en valores de entrada válidos para el modelo. A cada número aleatorio se lo multiplica por 250 y se le resta 125:


    const randomX = Math.random();
    const randomY = Math.random();
    riceGrainValues.push([randomX, randomY, (randomX * 250) - 125, (randomY * 250) - 125]);

Por cada grano de arroz se guardan dos números aleatorios y las posiciones de los ejes X e Y.
Luego de calcular ambos valores, se calculó el ángulo del punto con respecto al punto (0, 0).


    let theta = Math.atan2(y - 0, x - 0) * (180 / Math.PI); 

Y de acuerdo al ángulo del punto del grano, se calcula el punto de la circunferencia del círculo en ese mismo ángulo.

    
    const radius = 125
    const circleX = Math.cos(theta)*radius;
    const circleY = Math.sin(theta)*radius; // Punto de la circunferencia del círculo en el ángulo theta

Luego, de acuerdo en qué cuadrante estén los dos puntos (del grano y de la circunferencia), se calcula si el grano está dentro o fuera de la circunferencia.


    let xSigne = 1;
    let ySigne = 1;
    if (x < 0) { xSigne = -1; }
    if (y < 0) { ySigne = -1; }
    if (x > circleX * xSigne && y > circleY * ySigne) {
        result = 0; // Está fuera de la circunferencia
    } // Si no, está dentro de la circunferencia

### Paso 3


Se itera las veces que el usuario indique en la caja de texto antes de simular.
Cada iteración representa un grano de arroz.

### Paso 4

Al final de la simulación se realiza el cálculo del número PI, analizando y contabilizando los resultados.

