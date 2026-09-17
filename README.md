# STATA-dbcrp
Comando automatizado para Stata que descarga, limpia y consolida series de tiempo directamente desde el API del Banco Central de Reserva del Perú (BCRP).

# dbcrp: Descargador automatizado del BCRP para Stata

`dbcrp` es un comando nativo para Stata que permite descargar, limpiar y estructurar series de tiempo macroeconómicas directamente desde el API del Banco Central de Reserva del Perú (BCRP). 

El comando maneja automáticamente las etiquetas HTML residuales del servidor gubernamental, detecta la frecuencia temporal (anual, trimestral, mensual) y consolida múltiples series en un panel de datos listo para estimaciones econométricas, protegiendo las descripciones originales en las notas del sistema.

## Instalación

Puedes instalar el comando directamente ejecutando la siguiente línea en la consola de Stata:

```stata
net install dbcrp, from("[https://raw.githubusercontent.com/TU_USUARIO/STATA-dbcrp/main/](https://raw.githubusercontent.com/TU_USUARIO/TU_REPOSITORIO/main/)") replace

## Sintaxis

La estructura general del comando es:

```stata
dbcrp CODIGO1 [CODIGO2 ...] [INICIO FIN] [, names(nombre1 nombre2 ...)]
