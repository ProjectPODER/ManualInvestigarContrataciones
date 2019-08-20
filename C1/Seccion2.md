## 1.2. Indicios para iniciar investigaciones QQW + Kibana

QQW utiliza Kibana para montar lo datos y alimentarse desde ahí. Kibana es una herramienta de elastic search. Estas dos herramientas juntas permiten encontrar patrones que revelan comportamientos  poco comunes o valores que se salen de la normalidad en las compras públicas que pueden servir como indicios para iniciar una investigación.

Las Unidades Compradoras (UC) son los departamentos dentro de una dependencia,  que hacen las compras públicas. Cada dependencia tiene diferentes UC y no existe una norma sobre cómo deberían estar organizadas, por servicios, geográficamente o de alguna otra forma, pero es importante conocer estas células de las dependencias porque finalmente ellas son las que contratan a los proveedores. 

Por ejemplo, al analizar a la Comisión Federal de Electricidad en la plataforma TodosLosContratos, de PODER, se pueden encontrar los nombres de las UC, y ver que la CFE sigue un esquema de compra regional. 

Con un indicio, el nombre de una empresa originaria de Jalisco, se puede seguir la pista de ese proveedor dentro de la CFE, y descubrir una red de compañías hermanas a las que la CFE les compró gran cantidad (en valor) de uniformes.

Para encontrar esas relaciones se busca **“COMISIÓN FEDERAL DE ELECTRICIDAD”** ** en el filtro de dependencia de QQW, y “maxi uniformes sa de cv” en el filtro de Proveedor. Aparecerán los contratos entre ambas. Se puede revisar los documentos adjuntos a algunos de los contratos y se verá que en más de una ocasión los competidores de Maxi Uniformes eran los mismos: Grupo Oficial y Comercializadora Hagre. Ese es nuestro segundo indicio.

Investigando a las tres empresas se encuentra que en realidad están relacionadas entre sí. Para entender bien el modus operandi de las firmas, se vuelve a usar QQW para encontrar ahora los contratos de Grupo Oficial y Comercializadora Hagre con la CFE. 

Ahora tenemos tres indicios que indican que las empresas se conocen, que compiten entre ellas de manera amañada, que muchas UC de la CFE recuren a las mismas empresas sin importar de qué zona geográfica se trate. A partir de eso, se puede continuar la investigación periodística usando otras herramientas, como portales de contratación estatales y solicitudes de información. Así fue como realizamos en PODER el reportaje [Contratos a medida en la CFE](https://www.rindecuentas.org/reportajes/2018/09/12/contratos-a-medida-en-la-cfe/).

Es importante aclarar que dadas las deficiencias en cómo se reportan los contratos públicos en México,   y la dispersión de plataformas que existen para hacerlo, casi siempre será necesario ampliar las investigaciones por medio de solicitudes de información para obtener los contratos firmados, convenios modificatorios o facturas, pues esa información rara vez está adjunta en Compranet o el POT.

### 1.2.1 Cómo encontrar malas prácticas en contratación

Siguiendo con la crítica a las fallas de las dependencias para reportar sus contrataciones, y debido a que no hay incentivos, como una evaluación o la obligatoriedad por ley de hacer buenos reportes de sus contratos, es posible encontrar malas prácticas en cómo se contrata. Esos datos también pueden ser indicios para comenzar investigaciones. 

En TodosLosContratos.mx, plataforma ligada a QQW, que evalúa cómo se contrata y cómo se reportan esas contrataciones en México, hemos encontrado algunas malas prácticas que puedes [leer aquí](https://www.rindecuentas.org/reportajes/2019/08/20/10-malas-practicas-en-la-contratacion-publica-mexicana/). En este apartado explicamos cómo replicar la búsqueda desde QQW + Kibana para encontrar esos patrones extraños que no suman a la transparencia y rendición de cuentas. 

- Importes cero

Para encontrar los importes cero en Kibana es necesario filtrar por el índice de ocds-cnet, pues sólo es dataset tiene el campo de estatus en cada contrato. De hecho, si se cuentan los contratos con importe 0 en Compranet 3.0, la suma sube de 466 a 486. Después, se usa el filtro “alias_contrato_importe”, con la opción de “is one of”, y se escribe “0” y "0.00"[^1]. Finalmente se usa el filtro “contracts.statusMxCnet” para buscar con la opción de “is”, cuántos contratos aparecen con el estatus terminado, activo o expirado.

- Títulos imprecisos

Títulos que no explican el servicio o bien contratado a profundidad, son títulos imprecisos (Aquí puedes encontrar más definición sobre esto. ENLACE DE DEFINICION DE BANDERAS). Para encontrar algunos basta escribir en el buscador de Kibana dentro del campo tender.title : “servicios profesionales”. Otra forma de buscar los títulos incomprensibles es ver cada uno, seleccionando el filtro de tender.title ente los filtros disponibles en la columna de la izquierda en Kibana dentro de Discover.[^2]

- Campos cambiantes

Compranet se compone de dos datasets: Compranet 3.0, que contiene los contratos de 2002 a 2011 y Compranet, que contiene los contratos de 2010 a 2018. Ambas fuentes han sido incluidas en QuienEsQuien.Wiki / Kibana, y analizadas para encontrar malas prácticas a través de sus campos. A esto se suma que los campos del POT no replican muchos de los que existen en ambas versiones de Compranet. Pero los campos entre los diferentes datasets han ido cambiando, lo que hace difícil estandarizar la búsqueda de contratos. 

“Algo tan simple como el campo que define si el procedimiento de la compra es adjudicación directa, invitación a tres o licitación en Compranet dependiendo de la fuente se llama “Tipo de procedimiento”, “TIPO_PROCEDIMIENTO” o “TIPO DE PROCEDIMIENTO”, en el IMSS “Procedimiento de compra”, en el POT “Procedimiento de contratación” y la API de contrataciones abiertas de la APF que se puede descarga de datos.gob.mx “tender.procurementMethod”. Los valores que contienen cada uno también tienen variaciones de nombre según la fuente”, según define el informe de TodosLosContratos.mx (ENLACE).

Para buscar en Kibana el tipo de procedimiento en Compranet, se debe filtrar por _index is “ocds-cnet”, “ocds-cnet3” o “ocds-pot”, y seleccionar “tender.procurementMethodDetailsTemplateMxCnet."[^3]

---
**: Es recomendable escribir en mayúsculas y con acentos los nombres de las dependencias en la primera búsqueda, de no aparecer nada, se debe intentar en minúsculas y sin acentos.

[^1]: https://kibana-staging.quienesquien.wiki/goto/b9a2b0350353d0a1708cddc3aeb04756
[^2]: https://kibana-staging.quienesquien.wiki/goto/fc5b4e938af86c65665669e74a6f1478
[^3]: https://kibana-staging.quienesquien.wiki/goto/6e5bf82d5644092b5d44a032b40951c0
