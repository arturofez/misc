### Acelerar Time Machine
~~~
sudo sysctl debug.lowpri_throttle_enabled=0
~~~

---

### Cambiar ubicación capturas de pantalla
~~~
defaults write com.apple.screencapture location "RUTA"
killall SystemUIServer
~~~
Para volver a guardarlas en el escritorio:
~~~
defaults write com.apple.screencapture location ~/Desktop
killall SystemUIServer
~~~

---

### Comprimir en zip con contraseña
~~~
zip -e NOMBRE_COMPRIMIDO.zip NOMBRE_ARCHIVO
zip -er NOMBRE_COMPRIMIDO.zip NOMBRE_CARPETA
~~~

---

### Eliminar o añadir iconos del Launchpad
Buscamos el archivo *db* y lo abrimos con *SQLite* para editarlo:
~~~
sudo find /private/var/folders -name com.apple.dock.launchpad
cd db
sqlite3 db
~~~
Para ver las tablas:
~~~
.tables
~~~
Para ver las columnas de una tabla:
~~~
PRAGMA table_info(NOMBRE_TABLA);
~~~
Editamos con sentencias SQL, por ejemplo:
~~~
delete from apps where title='NOMBRE_APP'
~~~
Salimos y reiniciamos el dock:
~~~
.exit
killall Dock
~~~
Para restaurar la configuración por defecto del Launchpad, borrar el archivo *db* y reiniciar el dock

---

### Unir vídeos con FFmpeg
Con FFmpeg podemos concatenar archivos de vídeo siempre que tengan el mismo formato y códec.
Creamos un archivo `mylist.txt` que contenga una lista de los vídeos con el siguiente formato:
~~~
file '/ruta-al-archivo/file1.mp4'
file '/ruta-al-archivo/file2.mp4'
file '/ruta-al-archivo/file3.mp4'
~~~
Y ejecutamos el comando:
~~~
ffmpeg -f concat -safe 0 -i mylist.txt -c copy output.mp4
~~~

---
