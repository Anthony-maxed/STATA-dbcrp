# dbcrp: Data directa del BCRP para Stata

`dbcrp` es un comando nativo para Stata que permite descargar, limpiar y estructurar series de tiempo macroeconómicas directamente desde el API del Banco Central de Reserva del Perú (BCRP).

El comando detecta automáticamente si la serie es anual, trimestral o mensual, se encarga de los formatos de fecha del BCRP y junta varias series en una sola base lista para usar en Stata, guardando los títulos originales en las notas del sistema. Esta versión incluye un motor de red universal para evadir bloqueos de firewall institucionales.

## Instalación y actualización

Puedes instalar el comando directamente ejecutando la siguiente línea en la consola de Stata:

```stata
net install dbcrp, from("https://raw.githubusercontent.com/Anthony-maxed/STATA-dbcrp/main/") replace
```

> **Nota de actualización:** Si ya habías instalado una versión anterior de `dbcrp`, vuelve a ejecutar esta misma línea. El parámetro `replace` forzará a Stata a descargar la versión 8.0 más reciente y estable.

## Sintaxis

La estructura general del comando es:

```stata
dbcrp CODIGO1 [CODIGO2 ...] [INICIO FIN] [, names(nombre1 nombre2 ...)]
```

- **CODIGOS:** Los identificadores oficiales de las series (ej. `PN01205PM`). No se recomienda mezclar distintas frecuencias (mensual con anual) en una misma ejecución.
- **INICIO FIN (opcional):** El rango de fechas. Si no se especifican años, el comando enviará una solicitud limpia y el BCRP devolverá la historia reciente por defecto. **Importante:** si deseas delimitar un periodo, debes especificar estrictamente ambos años (inicio y fin).
- **names() (opcional):** Permite renombrar las variables al instante. Debe contener la misma cantidad de palabras que series solicitadas.

## Ejemplos de uso

### 1. Descargar la data reciente (piloto automático)

```stata
dbcrp PN39276BQ PN39279BQ
```

Al no colocar fechas, el servidor del banco envía automáticamente los datos más recientes. Descarga, alinea los periodos y declara la base como serie de tiempo.

### 2. Descargar un rango de años (autocompletado inteligente)

```stata
dbcrp PN01770AM PN01771AM 2015 2024, names(PBI sec_prima)
```

Descarga los datos desde 2015 hasta 2024 y renombra las columnas automáticamente.

> **Nota:** El comando es inteligente; no necesitas especificar meses o trimestres si quieres años completos. `dbcrp` completará automáticamente los meses (`2015-1` a `2024-12`) o trimestres (`2015-1` a `2024-4`) según el tipo de serie para evitar errores de servidor.

### 3. Descargar meses o trimestres de corte específicos

```stata
dbcrp PN01770AM PN01771AM 2015-5 2024-10
```

Si necesitas un corte muy específico, el número que va después del guion depende de la frecuencia de la serie: para datos mensuales va de 1 a 12 (ej. `2015-5` = mayo 2015), y para datos trimestrales va de 1 a 4 (ej. `2015-1` = primer trimestre 2015).

##
MIT
