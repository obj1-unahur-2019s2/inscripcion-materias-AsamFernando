# Inscripción a materias

Queremos implementar un sistema que permita realizar la inscripción a materias de una Universidad. Ojo, prestar bien atención a las reglas del dominio, que pueden no ser exactamente iguales a las de tu universidad.

En esta universidad de cada materia hay un único curso y el programa tiene sólo información de la inscripción actual, no nos interesan inscripciones anteriores. 
En cambio, sí debemos conocer el historial de materias aprobadas de un estudiante. 
De cada materia aprobada hay que saber qué materia aprobó y con qué nota.

> Tip: La nota con la que un estudiante aprobó una materia, no puede ser atributo del estudiante (porque un estudiante tiene muchas notas) ni de la materia (porque una materia tiene muchos estudiantes y cada uno tiene su nota). Entonces se necesita un objeto que represente "Juan Pérez aprobó Objetos 1 con 7", que es distinto tanto al objeto que representa a Juán Pérez como al objeto que representa a la materia Objetos 1.

1. Determinar si un estudiante puede cursar una materia. Para esto se deben cumplir tres condiciones: 
   * La materia debe corresponder a alguna de las carreras que esté cursando el estudiante.	Tener en cuenta que: 
    a) un estudiante puede estar cursando varias carreras y 
    b) cada materia pertenece a una única carrera.
   * El estudiante no puede haber cursado la materia previamente, ni estar inscripto.
   * Además cada materia tiene sus propios prerrequisitos, que pueden tener diferentes formas y se detallan a continuación.
   
   Los prerrequisitos de una materia pueden ser:
   * Un conjunto de materias correlativas: por ejemplo para cursar Algormitmos 3 es necesario haber cursado Algoritmos 2 y Matemática.
   * Una cantidad de créditos: por ejemplo para hacer el Trabajo Final se necesita acumular 250 créditos previamente. (Cada materia aprobada otorga una cantidad de créditos determinada.)
   * Por año, es decir haber aprobado todas las materias del año anterior. Por ejemplo, para cursar PHM, que es una materia de tercer año, es necesario haber aprobado todas las materias del segundo año.
   * Nada: Hay materias que no tienen ningún requerimiento, por ejemplo Laboratorio, no tiene ninguna condición especial.

2. Registrar una materia aprobada por un estudiante, verificando que no se cargue dos veces la nota de una misma materia.

3. Inscribir un alumno a un curso, verificando las condiciones de inscripción de la materia. Además, cada materia tiene un “cupo”, es decir, una cantidad máxima de estudiante que se pueden inscribir. Para manejar el exceso en los cupos, las materias tienen una lista de espera, de estudiantes que quisieran cursar pero no tienen lugar 
(ver punto 5). 

   No se requiere que el sistema conteste nada con respecto al resultado de la inscripción. 

4. Dar de baja un estudiante de una materia. En caso de haber estudiantes en lista de espera, el primer estudiante de la lista debe obtener su lugar en el curso.

5. Resultados de inscripción. Luego de la inscripción, el sistema debe poder contestar
    * Dada una materia los estudiantes inscriptos.
    * Dada una materia los estudiantes en lista de espera

6. Guía para el estudiante: 
    * Dado un estudiante y una carrera, conocer todas las materias de esa carrera a las que se puede inscribir. Sólo vale si el estudiante está inscripto a esa carrera.
    * Dado un estudiante, todas las materias en las que está inscripto.
    * Dado un estudiante, todas las materias en las que quedó en lista de espera.

7. Implementar los tests descritos a continuación. Un alumno se intenta inscribir a una materia que ya cursó, se rechaza.
    * Un alumno se intenta inscribir a una materia pero le falta una correlativa, se rechaza.
    * Alumno quiere inscribirse a la materia y cumple los requisitos pero no hay cupo. Usar criterio por orden de llegada y el alumno queda en lista de espera.

## Bonus
8. Diferentes materias pueden tener diferentes estrategias para manejar su lista de espera, a saber:
Pero el criterio para ver quién va a la lista de espera, es distinto según la carrera:
    * Por orden de llegada: si te querés inscribir y no hay lugar vas a la lista de espera por llegar último
    * Elitista: entran los que tengan mejor promedio.
    * Por grado de avance: Inscribimos al estudiante con más materias aprobadas en la carrera.
