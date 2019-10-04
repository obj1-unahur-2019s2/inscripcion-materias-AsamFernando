# Inscripción a materias

Queremos implementar un sistema que permita realizar la inscripción a materias de una Universidad. Ojo, prestar bien atención a las reglas del dominio, que pueden no ser exactamente iguales a las de tu universidad.

En esta universidad de cada materia hay un único curso y sólo vamos a manejar  información de la inscripción actual, no nos interesan inscripciones anteriores. 
En cambio, sí debemos conocer el historial de materias aprobadas de un estudiante. 
De cada materia aprobada hay que saber qué materia aprobó y con qué nota.

Cada materia pertenece a una única carrera. Pero, un estudiante puede estar cursando distintas carreras. En esta universidad, cada materia otorga una cantidad de _créditos_, que es un número. 

En los ejemplos incluiremos tres carreras: _Programación_, _Medicina_ y _Derecho_.
- Programación incluye, entre otras, estas materias: Elementos de Programación, Matemática 1, Objetos 1, Objetos 2, Objetos 3, Trabajo Final, Bases de Datos. 
- Medicina incluye Química, Biología 1, Biología 2, Anatomía General.
- Derecho incluye Latín, Derecho Romano, Historia del Derecho Argentino, Derecho Penal 1, Derecho Penal 2.

_Roque_ es un estudiante muy inquieto, que está cursando programación y medicina. De programación, tiene aprobadas Matemática 1 y Objetos 1. 

> **Tip**:   
La nota con la que un estudiante aprobó una materia, no puede ser atributo del estudiante (porque un estudiante tiene muchas notas) ni de la materia (porque una materia tiene muchos estudiantes y cada uno tiene su nota). Entonces se necesita un objeto que represente "Juan Pérez aprobó Objetos 1 con 7", que es distinto tanto al objeto que representa a Juán Pérez como al objeto que representa a la materia Objetos 1.

Implementar un modelo que permita resolver los siguientes **requerimientos**. 

1. Registrar una materia aprobada por un estudiante indicando la nota obtenida. Si el estudiante ya tiene registrada la aprobación de la materia, se debe lanzar un error. 

1. Saber para un estudiante: si tiene o no aprobada una materia, la cantidad de materias aprobadas, el promedio.

1. Saber para un estudiante: la colección de materias de **todas** las carreras a las que está inscripto. P.ej. para Roque debe incluir todas las de programación y también todas las de medicina.  
_Sugerencia_: mirar el método `flatten`, p.ej. probar `[[3,4],[6,8,2]].flatten()`. 

1. Determinar si un estudiante puede inscribirse a una materia. Para esto se deben cumplir cuatro condiciones: 
    - la materia debe corresponder a alguna de las carreras que esté cursando el estudiante, 
    - el estudiante no puede haber aprobado la materia previamente, 
    - el estudiante no debe estar estar ya inscripto en esa materia,
    - el estudiante debe tener aprobadas todas las materias que se declaran como _requisitos_ de la materia a la que se quiere inscribir.  
    P.ej., para que un estudiante pueda inscribirse a Objetos 2, es necesario tener aprobadas Objetos 1 y Matemática 1.

1. Inscribir un estudiante a una materia, verificando las condiciones de inscripción de la materia. Si no se cumplen las condiciones, lanzar un error.  
Además, cada materia tiene un “cupo”, es decir, una cantidad máxima de estudiantes que se pueden inscribir. Para manejar el exceso en los cupos, las materias tienen una lista de espera, de estudiantes que quisieran cursar pero no tienen lugar 
(ver punto 5).
O sea, como resultado de la inscripción, el estudiante puede, o bien quedar confirmado, o bien quedar en lista de espera.  
No se requiere que el sistema conteste nada con respecto al resultado de la inscripción. 

1. Dar de baja un estudiante de una materia. En caso de haber estudiantes en lista de espera, el primer estudiante de la lista debe obtener su lugar en la materia.

1. Brindar resultados de inscripción, específicamente:
    * Los estudiantes inscriptos a una materia dada.
    * Los estudiantes en lista de espera para una materia dada.

1. Brindar información útil para une estudiante, específicamente: las materias en las que está inscripto, las materias en las que quedó en lista de espera. Para esto, usar la lista de todas las materias de las carreras que cursa, resuelto en un punto anterior.

1. Más información sobre une estudiante: dada una carrera, conocer todas las materias de esa carrera a las que se puede inscribir. Sólo vale si el estudiante está cursando esa carrera.  




# Tests 
Suponiendo que
* los requisitos de Objetos 2 son Objetos 1 y Matemática 1.
* Los requisitos de Objetos 3 son Objetos 2 y Bases de Datos.
* Los requisitos de Programación Concurrente son Objetos 1 y Bases de Datos.
* Biología 2 tiene como único requisito a Biología 1.
* Roque tiene aprobadas Elementos de Programación, Matemática 1, Objetos 1, Bases de Datos, Química y Biología 1.
* Tenemos a: Luisa, Romina y Alicia que aprobaron Elementos de Programación, Objetos 1, y Matemática 1; Ana que aprobó solamente Elementos de Programación. Todas están cursando Programación.
* Objetos 2 tiene cupo para 3 estudiantes.

Realizar estos tests:
* Roque puede inscribirse en Objetos 2, pero no en Objetos 3 (porque le falta Objetos 2) ni en Objetos 1 (porque ya la tiene aprobada).
* Roque puede inscribirse: en Programación, en Objetos 2 y Programación Concurrente; en Medicina, en Biología 2.
* Si se inscriben, en este orden, Luisa, Romina, Alicia y Roque en Objetos 2, entonces las tres primeras quedan confirmadas, y Roque queda en lista de espera.
* Si después se da de baja Romina en Objetos 2, entonces Roque pasa a tener la inscripción confirmada en esa materia.


## Bonus

Contemplar que no todas las materias ponen a otras materias como requisitos. Otras opciones son:
   * Una cantidad de créditos: por ejemplo para hacer el Trabajo Final se necesita acumular 250 créditos previamente. 
   * Por año, es decir, haber aprobado todas las materias del año anterior. Por ejemplo, para cursar Objetos 3, que es una materia de tercer año, es necesario haber aprobado todas las materias del segundo año. De cada materia se conoce a qué año pertence.
   * Nada: Hay materias que no tienen ningún requerimiento, por ejemplo Elementos de Programación, no tiene ninguna condición especial.


Por otro lado, diferentes materias pueden tener diferentes _estrategias para manejar su lista de espera_, a saber:
- Por orden de llegada: si te querés inscribir y no hay lugar vas a la lista de espera por llegar último
- Elitista: entran los que tengan mejor promedio.
- Por grado de avance: Inscribimos al estudiante con más materias aprobadas en la carrera.
