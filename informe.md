# TAS1 - Estructura Linux

Autor: Wilmer Alexander Ruilova Merchan
Asignatura: Tendencias Tecnológicas — Semana 1
Fecha: 8 de octubre de 2026

## 1. Título
Organización de carpetas y manejo de archivos con comandos de Linux.

## 2. Tiempo de duración
Aproximadamente 14 minutos, considerando la revisión de los comandos, las capturas y la grabación del audio.

## 3. Fundamentos
La terminal de Linux permite trabajar con archivos y carpetas mediante comandos. En lugar de abrir varias ventanas y hacer clic en cada opción, se escribe una instrucción para realizar una tarea. Bash es la shell que interpreta estos comandos. Para esta práctica se usó Ubuntu con WSL 2, que permite utilizar Linux dentro de Windows sin tener que reiniciar el computador.

Antes de crear o mover un archivo, conviene saber en qué carpeta estamos. El comando `pwd` muestra la ubicación actual y `ls` permite revisar su contenido. Para cambiar de carpeta se utiliza `cd`. Estos comandos ayudan a evitar confusiones, sobre todo cuando existen varios archivos con nombres parecidos. Las rutas también son importantes: una ruta absoluta indica la ubicación desde la raíz del sistema, mientras que una relativa parte de la carpeta en la que estamos trabajando.

Para organizar la práctica se creó una carpeta principal y tres subcarpetas. El comando `mkdir` sirve para crear directorios. Después se utilizó `touch` para crear un archivo vacío. Si el archivo ya existe, este comando actualiza sus marcas de tiempo. Con `echo` se escribió el texto de las notas y con `cat` se revisó su contenido. La opción `-n` de `cat` muestra los números de las líneas y facilita comprobar cuántas hay.

La diferencia entre copiar y mover se puede ver con `cp` y `mv`. Al copiar, el archivo original se conserva y aparece otra copia en el destino. Al mover, el archivo cambia de ubicación. Además, `mv` sirve para cambiar su nombre. Por eso se pudo copiar notas.txt a scripts, renombrar la copia y llevarla a imagenes.

Otro punto de la práctica fue la redirección. El símbolo `>` envía el contenido a un archivo y reemplaza lo que había antes. En cambio, `>>` agrega texto al final. Esta diferencia permitió que resumen.txt conservara las tres líneas de notas y tuviera una cuarta línea adicional.

Para terminar, `rm` eliminó el archivo de respaldo y `rmdir` borró la carpeta cuando quedó vacía. El historial se guardó con `history | tee`: la tubería pasa la salida del primer comando al segundo, y `tee` la muestra en pantalla y la escribe en un archivo. Así queda un registro que permite revisar los pasos realizados.

<img src="capturas/resultados-ubuntu.png" alt="Figura 1. Ejemplo real de archivos y redireccion en Ubuntu WSL" width="800">

Figura 1. En la terminal se observan las carpetas, las tres líneas de notas y la cuarta línea añadida al resumen. Este ejemplo muestra la diferencia entre leer un archivo y agregarle contenido.

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
La práctica se realizó en Ubuntu WSL. La carpeta de trabajo fue `/mnt/c/Users/USER/OneDrive/Desktop/02 - Estudios/Tendencias_Tecnologicas_T1/practica-verificada`.

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
Se utilizó `imagenes`, sin tilde, porque así se llama la carpeta creada en las instrucciones iniciales.

### Paso 6. Comprobar los resultados y guardar el historial
```bash
find . -maxdepth 2 -print
wc -l documentos/notas.txt documentos/resumen.txt
cmp documentos/notas.txt <(head -n 3 documentos/resumen.txt) && echo 'OK: resumen conserva las tres lineas de notas.'
test ! -e imagenes && test -d scripts && echo 'OK: imagenes eliminada y scripts conservada.'
history | tee ../tarea-s1-wilmer_ruilova.txt
```
El historial quedó guardado fuera de `proyecto_comandos`. Su copia se subió al repositorio junto con este informe.

## 9. Resultados esperados
Al finalizar, la estructura de carpetas quedó así:
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

Figura 2. Captura de los resultados en Ubuntu WSL. Se ve el contenido de los archivos y la comprobación de que imagenes ya no existe. Los pasos de copia, cambio de nombre y movimiento pueden revisarse en tarea-s1-wilmer_ruilova.txt.

## 10. Bibliografía
Instituto Sudamericano. (2026). *1. Fundamentación teórica* [Material de curso]. EVA. https://eva.sudamericano.edu.ec/mod/page/view.php?id=30431

Instituto Sudamericano. (2026). *TAS1 - Estructura linux* [Consigna de práctica]. EVA. https://eva.sudamericano.edu.ec/mod/assign/view.php?id=32765

maguaman2. (s. f.). *informe-tendencias* [Plantilla de informe]. GitHub. https://github.com/maguaman2/informe-tendencias
