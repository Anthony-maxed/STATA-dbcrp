# dbcrp: Data directa del BCRP para Stata

`dbcrp` es un comando nativo para Stata que permite descargar, limpiar y estructurar series de tiempo macroeconómicas directamente desde el API del Banco Central de Reserva del Perú (BCRP).

El comando maneja automáticamente las etiquetas HTML residuales del servidor gubernamental, detecta la frecuencia temporal (anual, trimestral, mensual), resuelve los requerimientos estrictos de formato de fecha del servidor y consolida múltiples series en un panel de datos listo para estimaciones econométricas, protegiendo las descripciones originales en las notas del sistema.

## Instalación

Puedes instalar el comando directamente ejecutando la siguiente línea en la consola de Stata:

```stata
net install dbcrp, from("https://raw.githubusercontent.com/Anthony-maxed/STATA-dbcrp/main/") replace
```

### Sintaxis

La estructura general del comando es:

```stata
dbcrp CODIGO1 [CODIGO2 ...] [INICIO FIN] [, names(nombre1 nombre2 ...)]
```

* **CODIGOS**: Los identificadores oficiales de las series (ej. `PN01205PM`). No se recomienda mezclar distintas frecuencias (mensual con anual) en una misma ejecución.
* **INICIO FIN** (Opcional): El rango de fechas. Si no se especifica, el comando autocompletará los formatos exigidos por el API del BCRP y descargará toda la historia disponible de la serie (1900-2099). Si se especifica una sola fecha, descargará desde ese punto hasta la actualidad.
* **names()** (Opcional): Permite renombrar las variables al instante. Debe contener la misma cantidad de palabras que series solicitadas.

## Ejemplos de uso

### 1. Descargar el historial completo (Piloto Automático)

```stata
dbcrp PN39276BQ PN39279BQ
```

Descarga toda la data disponible desde el origen hasta hoy, alinea los periodos y declara la base como serie de tiempo.

### 2. Descargar un periodo cerrado con nombres personalizados

```stata
dbcrp PN01770AM PN01771AM 2015-1 2024-12, names(PBI sec_prima)
```

Descarga datos mensuales desde enero de 2015 hasta diciembre de 2024 y renombra las columnas automáticamente.

> **Nota sobre el formato de fecha:** el número que va después del guion depende de la frecuencia de la serie: para datos **mensuales** va de **1 a 12** (ej. `2015-1` = enero 2015), y para datos **trimestrales** va de **1 a 4** (ej. `2015-1` = primer trimestre 2015).

### 3. Descargar desde una fecha específica hasta la actualidad

```stata
dbcrp PM04998AA 2005
```

Descarga la serie anual desde el año 2005 en adelante.

## Notas y Etiquetas

Para mantener la limpieza en los cuadros de regresión, `dbcrp` deja las etiquetas (`labels`) en blanco, pero guarda el título completo original del BCRP de forma segura en las notas de la variable. Para consultarlo, simplemente escribe en Stata:

```stata
notes
```

## Autor

Anthony Facundo Huaynate Onofre

## Licencia

MIT
