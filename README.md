# PS4 9.00 Kernel Exploit
---
## Resumen
En este proyecto encontrará una implementación que intenta hacer uso de un error del sistema de archivos para Playstation 4 en el firmware 9.00.

El error se encontró al comparar los kernels 9.00 y 9.03. Requerirá una unidad con un sistema de archivos exfat modificado.

Activarlo con éxito le permitirá ejecutar código arbitrario como kernel, para permitir el jailbreak y modificaciones a nivel de kernel en el sistema. lanzará el lanzador de carga útil habitual (en el puerto 9020).

## Parches Incluidos
Los siguientes parches se aplican al kernel:
1) Permitir mapeo de memoria RWX (lectura-escritura-ejecución) (mmap / mprotect)
2) Instrucción Syscall permitida en cualquier lugar
3) Resolución dinámica (`sys_dynlib_dlsym`) permitida desde cualquier proceso
4) Llamada al sistema personalizada #11 (`kexec()`) para ejecutar código arbitrario en modo kernel
5) Permita que los usuarios sin privilegios llamen a `setuid(0)` con éxito. Funciona como una verificación de estado, se duplica como una escalada de privilegios.
6) (`sys_dynlib_load_prx`) parche
7) Deshabilita sysVeri

## Tutorial breve
Este exploit es diferente a los anteriores en los que se basaban únicamente en el software. Activar la vulnerabilidad requiere conectar un dispositivo USB con formato especial en el momento justo. En el repositorio encontrarás un archivo .img. Puede escribir este .img en un USB usando algo como Win32DiskImager.

**Nota: Esto borrará la unidad USB, asegúrese de seleccionar la unidad correcta y de que está de acuerdo con eso antes de hacer esto**

![](https://i.imgur.com/qpiVQGo.png)

Cuando ejecute el exploit en la PS4, espere hasta que llegue a una alerta con "Insertar USB ahora. No cierre el cuadro de diálogo hasta que aparezca la notificación, retire el usb después de cerrarlo". Como dice el cuadro de diálogo, inserte el USB y espere hasta que aparezca la notificación "formato de disco no compatible", luego cierre la alerta con "Aceptar".

El exploit puede tardar un minuto en ejecutarse, y la animación giratoria en la página puede congelarse; esto está bien, déjelo continuar hasta que aparezca un error o tenga éxito y muestre "Esperando carga útil".

## Notas extra
- Desconecte el USB antes de un ciclo de (re)arranque o correrá el riesgo de corromper el montón del kernel en el arranque.
- El navegador puede tentarlo a cerrar la página prematuramente, no lo haga.
- El círculo de carga puede congelarse mientras se activa el exploit webkit, esto no significa que el exploit haya fallado.
- El error es anterior al firmware 1.00, por lo que 1.00-9.00 debería poder explotarse con la misma estrategia (necesitará un exploit y dispositivos de usuario diferentes).
- Puede reemplazar el cargador con una carga útil específica para cargar cosas directamente en lugar de hacerlo a través de enchufes.
- Este error funciona en ciertos firmwares de PS5, sin embargo, no existe una estrategia conocida para explotarlo en este momento. No se recomienda usar este error contra la persiana de PS5.
- Por favor, no abras temas para decirme que no los hay... ni intentes hacerme hacer la tarea por ti.
- Este repositorio no proporciona nada más allá de los parches iniciales del kernel que le permiten ejecutar cargas útiles.
Si encuentra problemas con ciertas cargas útiles, debe informar sus problemas a los desarrolladores de esas cargas útiles a través de cualquier medio que pongan a su disposición.
- El nombre del repositorio es una fusión de las palabras 'ps4' y '[OOB](https://cwe.mitre.org/data/definitions/787.html)', siendo este último el tipo de vulnerabilidad que intenta esta implementación. para explotar, cualquier otra interpretación es pura coincidencia y no intencionada.
- As stated before, this bug was found by diffing the 9.00 and 9.03 kernels, this does imply that the bug was fixed on 9.03.
## Colaboradores

- laureeeeeee
- [Specter](https://twitter.com/SpecterDev)
- [Znullptr](https://twitter.com/Znullptr)

## Gracias especiales
- [Andy Nguyen](https://twitter.com/theflow0)
- [sleirsgoevy](https://twitter.com/sleirsgoevy) - [9.00 Webkit exploit](https://github.com/sleirsgoevy/bad_hoist/tree/9.00)
