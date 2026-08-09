# optimizacion-asignacion-tecnicos

Este es un proyecto académico sobre modelización matemática y optimización. Una empresa de protección contra incendios debe dividir sus instalaciones en 20 zonas, una por técnico. El objetivo es un reparto justo y eficiente bajo dos criterios: equilibrar el volumen de trabajo y asegurar la cercanía entre las instalaciones asignadas.

Para la resolución de este problema se han planteado tres modelos que posteriormente han sido resueltos con el software de optimización Gurobi.

## Una primera aproximación al problema

Como primera alternativa se ha planteado un modelo en el que se asigna cada uno de los 20 técnicos a una instalación "inicial" y posteriormente se van agregando el resto de instalaciones a cada una de estas instalaciones iniciales. Este modelo es muy pesado y tras varias horas de ejecución no se obtiene una solución óptima.

Como punto positivo cabe destacar que ha asignado las instalaciones siguiendo los criterios deseados. Aunque no se ha obtenido la solución óptima, sí se ha obtenido una solución aceptable.

## Segunda alternativa (Agrupación de instalaciones)

En este caso se plantea un modelo similar al primero, pero agrupando instalaciones y tratando estas agrupaciones como si fueran instalaciones en sí mismas. De esta forma se solventa el problema de tamaño del modelo y sí se puede llegar a una solución óptima. Con este enfoque se plantean dos cuestiones:

* Cómo agrupar las instalaciones: Las instalaciones se agrupan por distancias, considerando que las coordenadas de la agrupación se corresponden con el centroide del conjunto de instalaciones que agrupa. 

* Qué métrica utilizar para considerar la distancia entre agrupaciones: Si se toma la distancia entre las agrupaciones como si fueran instalaciones por separado, estaría dando por hecho que desplazarse hasta un grupo de instalaciones cuesta lo mismo que desplazarse a una sola. Según he podido comprobar, esto da muy malos resultados. Para solventarlo se ha considerado que la distancia de la agrupación A a la agrupación B es la distancia euclídea de A a B multiplicada el número de instalaciones en A.

## Tercera alternativa (Preasignar instalaciones iniciales)

Se han asignado previamente las instalaciones iniciales. En la optimización solo es necesario asignar el resto de instalaciones a estas instalaciones iniciales. Este enfoque ofrece un modelo muy ligero. Existen muchas formas de asignar las instalaciones iniciales. En este caso se ha optado por utilizar el método de agrupamiento de k-medias basándome en la posición de las instalaciones.

Dado un conjunto de $n$ observaciones, si se quieren obtener $k$ grupos, el algoritmo de k-medias tiene como objetivo obtener una partición del conjunto de $n$ datos de modo que cada observación pertenezca al grupo de observaciones cuyo centroide sea más cercano. He añadido la restricción de que cada grupo tenga aproximadamente el mismo número de instalaciones.

## Resultados

La mejor solución ha sido la obtenida con las agrupaciones en la segunda alternativa. No ha tardado demasiado tiempo en encontrar el óptimo global. Podrían incluso haberse hecho agrupaciones más pequeñas para mejorar el resultado.

<img width="854" height="574" alt="image" src="https://github.com/user-attachments/assets/43d1309e-558e-4557-9fb5-06694b7d3c0a" />

### Librerías utilizadas: pandas, folium, k-means-constrained, gurobipy, numpy, matplotlib, math

