# VB6-Librerias

Repositorio central **público** de librerías para los programas VB6 (Doscar/Prosicar).
Lo consume la utilidad `controlLibrerias` para saber cuál es la **última versión** de cada
librería propia y descargarla cuando hace falta.

> Público a propósito: estos binarios ya viajan a todos los clientes dentro de los ZIP de los
> programas, así que no son secreto. Sin token, descarga directa por URL raw.

## Estructura

```
versiones.json     <- la "última versión" oficial de cada fichero + su URL raw (fuente de verdad)
propias/           <- binarios propios al día: Tbai.dll/.tlb, Verifactu.dll/.tlb, CorreoCore.dll, VBFLXGRD18.OCX
sistema/           <- set redistribuible de OCX/DLL estándar (MSCOMCTL.OCX, COMDLG32.OCX, ...) para reparar registros caídos
```

## Cómo se actualiza

1. Se compila una versión nueva de una librería propia (p.ej. `Verifactu.dll`).
2. Se copia el binario a `propias/` (con sus dependencias .NET si las tiene).
3. Se sube su número a `versiones.json` (campo `Version` = el FileVersion del binario).
4. `controlLibrerias /comprobar` en los clientes detectará que la instalada es inferior y ofrecerá
   reparar (descarga de aquí + re-registro).

> **Nota de dependencias**: `Tbai.dll` arrastra ensamblados .NET (Newtonsoft, System.*). Para que
> `regasm /codebase` funcione, esas dependencias deben acompañar al binario en `propias/` (y
> descargarse junto a él). Pendiente de definir el empaquetado de dependencias.
