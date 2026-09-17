# STATA-dbcrp
Comando automatizado para Stata que descarga, limpia y consolida series de tiempo directamente desde el API del Banco Central de Reserva del Perú (BCRP).

# dbcrp: Descargador automatizado del BCRP para Stata

`dbcrp` es un comando nativo para Stata que permite descargar, limpiar y estructurar series de tiempo macroeconómicas directamente desde el API del Banco Central de Reserva del Perú (BCRP). 

El comando maneja automáticamente las etiquetas HTML residuales del servidor gubernamental, detecta la frecuencia temporal (anual, trimestral, mensual) y consolida múltiples series en un panel de datos listo para estimaciones econométricas, protegiendo las descripciones originales en las notas del sistema.

## Instalación

1. Descarga el archivo `dbcrp.ado` de este repositorio.
2. Cópialo en tu carpeta de comandos personales de Stata. Usualmente la ruta es:
   * **Windows:** `C:\ado\personal\` o `C:\Users\TuUsuario\ado\plus\`
   * **Mac:** `~/Library/Application Support/Stata/ado/personal/`

## Sintaxis

La estructura general del comando es:

```stata
dbcrp CODIGO1 [CODIGO2 ...] [INICIO FIN] [, names(nombre1 nombre2 ...)]
