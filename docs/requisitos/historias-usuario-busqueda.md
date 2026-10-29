# Historias de usuario de búsqueda

| Campo | Valor |
| --- | --- |
| Proyecto | Proyecto Simbiosis |
| Fecha | 29/10/2026 |
| Versión | 0.1 |
| Estado | Borrador |

## Fuentes comunes

- [Acta de UC-21 Buscar recetas](../captura/acta-acuerdos-uc-21-buscar-recetas.md), v1.1, Vigente.
- [Catálogo de requisitos](catalogo-requisitos.md), UR-08 y FR pertinentes.
- [Modelo de casos de uso](../modelos/modelo-casos-de-uso.md), UC-21.

## Épica de búsqueda

Como persona usuaria registrada, quiero localizar recetas combinando una palabra o frase, ingredientes que deben aparecer e ingredientes que no deseo, para encontrar rápidamente una receta que se ajuste a lo que quiero cocinar.

**Estado:** descompuesta en US-01, US-02 y US-03. Conserva la necesidad conjunta.

## Justificación de la división

La división separa tres resultados útiles que se pueden entregar por sí solos: encontrar recetas por lo que dice su texto, por los ingredientes que contienen y por los ingredientes que se quieren evitar. La exclusión se mantiene como historia propia porque puede usarse sin ningún otro criterio y porque responde a una necesidad distinta de buscar lo que se quiere encontrar.

## US-01

**Título:** Buscar recetas mediante una palabra o frase

Como persona usuaria registrada, quiero buscar recetas escribiendo una palabra o frase, para encontrar las recetas cuyo título o descripción breve mencionan lo que tengo en mente.

**Fuentes:** UR-08; UC-21; FR-085; acta, apartados «Criterios de búsqueda» y «Búsqueda sin resultados».

### Criterios de aceptación

- **CA-01.** Dado que existen publicadas y validadas la receta «Puré de calabaza» y la receta «Sopa de cebolla», cuando la persona busca la frase «PURE DE CALABAZA», entonces el sistema muestra «Puré de calabaza» y no muestra «Sopa de cebolla», sin distinguir mayúsculas ni tildes y porque la frase aparece seguida y en el mismo orden en el título.
- **CA-02.** Dado que ninguna receta contiene la frase «sopa galáctica» en su título ni en su descripción breve, cuando la persona la busca, entonces el sistema indica que no hay resultados para esa búsqueda, conserva el texto «sopa galáctica» en el campo y muestra las sugerencias, si las tiene, separadas de los resultados.
- **CA-03.** Dado que la persona no ha indicado ningún criterio de búsqueda, cuando solicita buscar, entonces el sistema le pide que indique al menos un criterio y no ejecuta la búsqueda.

## US-02

**Título:** Buscar recetas por ingredientes incluidos

Como persona usuaria registrada, quiero seleccionar los ingredientes que quiero usar, para ver solo las recetas que los contienen todos y aprovechar lo que tengo en casa.

**Fuentes:** UR-08; UC-21; FR-086; acta, apartados «Criterios de búsqueda» y «Resultados y detalle».

### Criterios de aceptación

- **CA-01.** Dado que existen publicadas y validadas la receta A con tomate y huevo, la receta B solo con tomate y la receta C con huevo y arroz, cuando la persona selecciona los ingredientes «tomate» y «huevo», entonces el sistema muestra únicamente la receta A.
- **CA-02.** Dado que la persona ha seleccionado «huevo» para incluirlo y también para excluirlo, cuando solicita buscar, entonces el sistema señala el conflicto sobre «huevo» y no ejecuta la búsqueda hasta que la persona lo corrige.
- **CA-03.** Dado que la receta D contiene «tomate» y «huevo» pero está pendiente de validación, y que la receta A está publicada y validada desde el 20/10/2026 y la receta E desde el 25/10/2026, ambas con esos ingredientes, cuando la persona busca «tomate» y «huevo», entonces el sistema no muestra la receta D y muestra primero la receta E y después la receta A.

## US-03

**Título:** Excluir ingredientes de la búsqueda

Como persona usuaria registrada, quiero indicar los ingredientes que no quiero que aparezcan, para descartar recetas que contienen ingredientes que no deseo consumir.

**Fuentes:** UR-08; UC-21; FR-087; acta, apartados «Criterios de búsqueda» y «Búsqueda sin resultados».

### Criterios de aceptación

- **CA-01.** Dado que existen publicadas y validadas una receta con cacahuete, una receta con leche y una receta sin ninguno de los dos, cuando la persona selecciona solo «cacahuete» y «leche» para excluirlos, sin ningún otro criterio, entonces el sistema muestra únicamente la receta que no contiene ninguno de los dos ingredientes.
- **CA-02.** Dado que la persona indica el texto «ensalada», incluye «tomate» y excluye «cebolla», cuando solicita buscar, entonces el sistema muestra solo las recetas que cumplen los tres criterios a la vez: «ensalada» en el título o en la descripción breve, con tomate y sin cebolla.
- **CA-03.** Dado que ninguna receta cumple a la vez el texto «ensalada», la inclusión de «tomate» y la exclusión de «cebolla», cuando la persona busca y el sistema propone alternativas relacionadas, entonces todas las sugerencias mantienen «cebolla» excluida, se muestran separadas de los resultados y ninguna propone retirar esa exclusión.

## Revisión INVEST

La revisión abarca US-01, US-02 y US-03. «Aplicado» indica si se ha realizado la comprobación. «Cumple» indica si todas las historias cumplen el criterio. Si alguna no lo cumple, indicar «No» e identificar la historia y el motivo en la justificación. Si no se ha realizado la comprobación o faltan datos, indicar «Pendiente» en «Cumple».

| Criterio | Pregunta de revisión | Aplicado | Cumple | Justificación |
| --- | --- | --- | --- | --- |
| Independiente | ¿Puede implementarse cada historia y ofrecer un resultado útil sin implementar antes las otras historias del conjunto? Puede compartir infraestructura con ellas. | Sí | Sí | US-01, US-02 y US-03 ofrecen cada una un resultado útil por sí solas: buscar por texto, por ingredientes o solo excluyendo. Comparten la infraestructura de búsqueda y de resultados. Los criterios US-02 CA-02 y US-03 CA-02 usan criterios de otra historia y se comprueban cuando ese otro criterio está disponible. |
| Negociable | ¿Cada historia explica qué necesita la persona y deja margen para discutir los detalles de la solución, respetando los acuerdos confirmados? | Sí | Sí | Las tres historias describen la necesidad sin fijar pantallas, campos ni tecnología. Los criterios solo recogen los acuerdos del acta, como la coincidencia del texto, la inclusión de todos los ingredientes y la conservación de las exclusiones. |
| Valiosa | ¿La parte «para…» de cada historia explica el beneficio que obtiene la persona al usar esa capacidad? | Sí | Sí | US-01 permite encontrar recetas por lo que tiene en mente, US-02 aprovechar ingredientes disponibles y US-03 descartar ingredientes no deseados. |
| Estimable | ¿Están claros el alcance y los datos necesarios para estimar el trabajo de cada historia? | Sí | Sí | Cada historia tiene una fuente (FR-085, FR-086 o FR-087) y criterios con datos de ejemplo. Las reglas de coincidencia, conflicto, orden y ausencia de resultados proceden del acta v1.1. |
| Pequeña | ¿Se centra cada historia en una única capacidad de alcance manejable? | Sí | Sí | Cada historia se centra en un único tipo de criterio de búsqueda. Los demás filtros, las recomendaciones, el historial y las acciones sobre la receta quedan fuera, igual que en el acta. |
| Comprobable | ¿Los criterios de aceptación de cada historia describen acciones y resultados observables que permiten distinguir un comportamiento correcto de uno incorrecto? | Sí | Sí | Los nueve criterios indican la situación, la acción y un resultado observable con datos concretos (recetas, ingredientes y fechas) que permiten decidir si el comportamiento es el esperado. |

## Dudas pendientes

Ninguna.
