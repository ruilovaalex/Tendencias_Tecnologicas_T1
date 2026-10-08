# TAS1 - Estructura Linux

Autor: Wilmer Alexander Ruilova Merchan
Asignatura: Tendencias Tecnológicas — Semana 1
Fecha: 8 de octubre de 2026

## 1. Título
Crear carpetas y manejar archivos en Linux.

## 2. Tiempo de duración
Unos 14 minutos entre revisar los comandos, tomar la captura y grabar el audio.

## 3. Fundamentos
Para esta práctica se usó la terminal de Ubuntu en Windows. Desde ahí se pueden crear carpetas, escribir archivos y moverlos sin abrir el explorador. WSL permite usar Linux dentro de Windows y Bash interpreta los comandos que se escriben en la terminal.

Lo primero es revisar dónde estamos. Para eso sirve `pwd`, que muestra la carpeta actual. Con `ls` podemos ver lo que hay dentro y con `cd` cambiamos de carpeta. Esto ayuda porque, si usamos una ruta incorrecta, el archivo puede quedar en otro lugar o el comando puede fallar. Una ruta absoluta empieza desde la raíz del sistema. Una ruta relativa parte de la carpeta actual, como documentos/notas.txt en este ejercicio.

Para crear las carpetas se usa `mkdir`. En este caso se creó proyecto_comandos y dentro quedaron documentos, imagenes y scripts. Luego, con `touch`, se creó notas.txt vacío. Si un archivo ya existe, touch actualiza sus fechas, no borra su contenido. El texto se agregó con `echo`. Después se revisó con `cat -n`, que muestra el contenido y numera las líneas.

Los comandos `cp` y `mv` tienen usos distintos. Con cp se hace una copia y el original queda en su carpeta. Con mv se puede mover un archivo o cambiarle el nombre. En la práctica primero se copiaron las notas a scripts. Esa copia se llamó backup_notas.txt y después pasó a imagenes. El archivo original siguió en documentos.

También se trabajó con los símbolos `>` y `>>`. Un signo mayor reemplaza el contenido del archivo de destino. Dos signos mayores agregan texto al final, sin borrar lo anterior. Para resumen.txt primero se pasó el contenido de notas.txt y después se agregó otra línea. Así quedaron las tres líneas originales más una nueva.

Al terminar se borró el respaldo con `rm`. Después se usó `rmdir` para quitar imagenes, que ya estaba vacía. Este comando no elimina una carpeta si todavía tiene archivos. Por último se guardó el historial con `history | tee`. La tubería conecta los dos comandos: history muestra el registro y tee lo guarda en un archivo, además de mostrarlo en pantalla. Ese archivo sirve para revisar cómo se hizo la práctica.

<img src="capturas/resultados-ubuntu.png" alt="Figura 1. Ejemplo real de archivos y redireccion en Ubuntu WSL" width="800">

Figura 1. Aquí se ven las notas y el resumen. El resumen tiene una línea más porque se agregó con >>.

## 4. Conocimientos previos
- Diferencia entre archivo, directorio y ruta.
- Navegación básica con `pwd`, `cd` y `ls`.
- Diferencia entre `>`, `>>` y `|`.
- Uso básico de Markdown y repositorios de GitHub.

## 5. Objetivos a alcanzar
- Crear una estructura de carpetas en Linux.
- Escribir, copiar, renombrar y mover archivos.
- Aplicar redirecciones y tuberías.
- Eliminar un archivo y un directorio vacío.
- Guardar el historial y presentar los resultados de la práctica.

## 6. Equipo necesario
- Computador Windows con Ubuntu en WSL 2.
- Ubuntu 24.04.4 LTS y Bash 5.2.21.
- Terminal y navegador con acceso a EVA.
- Cuenta de GitHub para publicar la entrega.
- Grabadora de sonido para preparar el audio de la entrega.

## 7. Material de apoyo
- Fundamentación teórica de Semana 1 en EVA.
- Instrucciones de TAS1 - Estructura linux.
- Plantilla del docente: https://github.com/maguaman2/informe-tendencias

## 8. Procedimiento
Se usó Ubuntu WSL. La práctica quedó en esta carpeta: `/mnt/c/Users/USER/OneDrive/Desktop/02 - Estudios/Tendencias_Tecnologicas_T1/practica-verificada`.

### Paso 1. Crear las carpetas
```bash
mkdir proyecto_comandos
cd proyecto_comandos
mkdir documentos imagenes scripts
ls -l
```

### Paso 2. Crear las notas y escribir tres líneas
```bash
touch documentos/notas.txt
echo 'Practica de comandos Linux - Semana 1' > documentos/notas.txt
echo 'Autor: Wilmer Alexander Ruilova Merchan' >> documentos/notas.txt
echo 'Objetivo: crear y manipular archivos desde la terminal.' >> documentos/notas.txt
cat -n documentos/notas.txt
```

### Paso 3. Copiar, renombrar y mover
```bash
cp documentos/notas.txt scripts/notas.txt
mv scripts/notas.txt scripts/backup_notas.txt
ls scripts
mv scripts/backup_notas.txt imagenes/backup_notas.txt
ls imagenes
```

### Paso 4. Crear el resumen y agregar una línea
```bash
touch documentos/resumen.txt
cat documentos/notas.txt > documentos/resumen.txt
echo 'La redireccion con >> agrega contenido sin borrar lo anterior.' >> documentos/resumen.txt
cat -n documentos/resumen.txt
```

### Paso 5. Eliminar la copia y el directorio vacío
```bash
rm imagenes/backup_notas.txt
rmdir imagenes
```
La carpeta se llamó `imagenes`, sin tilde, como indica el primer paso de la tarea.

### Paso 6. Comprobar los resultados y guardar el historial
```bash
find . -maxdepth 2 -print
wc -l documentos/notas.txt documentos/resumen.txt
cmp documentos/notas.txt <(head -n 3 documentos/resumen.txt) && echo 'OK: resumen conserva las tres lineas de notas.'
test ! -e imagenes && test -d scripts && echo 'OK: imagenes eliminada y scripts conservada.'
history | tee ../tarea-s1-wilmer_ruilova.txt
```
El historial quedó un nivel arriba de proyecto_comandos. También está subido en el repositorio.

## 9. Resultados esperados
Al final quedó esto:
```text
proyecto_comandos/
├── documentos/
│   ├── notas.txt
│   └── resumen.txt
└── scripts/
```
- `notas.txt`: tres líneas.
- `resumen.txt`: las tres líneas originales y una línea nueva, cuatro en total.
- `scripts`: quedó vacía después de mover el respaldo.
- `imagenes` y `backup_notas.txt`: eliminados según la consigna.
- `tarea-s1-wilmer_ruilova.txt`: registro de los comandos de la práctica.

<img src="capturas/resultados-ubuntu.png" alt="Figura 2. Resultados reales de la practica en Ubuntu WSL" width="800">

Figura 2. Resultado final en Ubuntu. Las notas tienen 3 líneas y el resumen 4. La carpeta imagenes ya no está. Los demás comandos se pueden revisar en el archivo del historial.

## 10. Bibliografía
Instituto Sudamericano. (2026). *1. Fundamentación teórica* [Material de curso]. EVA. https://eva.sudamericano.edu.ec/mod/page/view.php?id=30431

Instituto Sudamericano. (2026). *TAS1 - Estructura linux* [Consigna de práctica]. EVA. https://eva.sudamericano.edu.ec/mod/assign/view.php?id=32765

maguaman2. (s. f.). *informe-tendencias* [Plantilla de informe]. GitHub. https://github.com/maguaman2/informe-tendencias
