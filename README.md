# Robofut_UAM_Lerma

# Segmentación Multi-Objeto por Iteraciones en Video

Este proyecto implementa un enfoque de segmentación por capas e iterativo para identificar y rastrear múltiples objetos (equipos de robots y la pelota) en un video utilizando el modelo **SAM 3** (Segment Anything Model 3) de Meta[cite: 3, 6, 26].

---

## 🛠️ Descripción del Enfoque y Arquitectura de la Solución

La notebook principal (`test_multisegmentation_iter_video.ipynb`) contiene todo el código necesario para procesar y segmentar el video original[cite: 2]. 

La segmentación del video requiere clasificar múltiples objetos pertenecientes a tres categorías específicas: **Equipo_1**, **Equipo_2** y **pelota**[cite: 3]. El pipeline funciona de manera **iterativa y por capas**[cite: 4, 5]:

1. **Primera Iteración (Equipo_1):** Se segmentan únicamente los robots pertenecientes al Equipo_1. El resultado es un video intermedio con esta capa aislada[cite: 5].
2. **Segunda Iteración (Equipo_2):** Se toma el video resultante de la iteración anterior y se realiza la segmentación sobre los robots del Equipo_2[cite: 6].
3. **Última Iteración (Pelota y Marcador):** Se procesa la pelota y se aplica una detección basada en zonas (porterías izquierda y derecha) para modificar dinámicamente un marcador en pantalla y lanzar un mensaje de anotación[cite: 6].

---

## 📹 Descripción del Video Original y Segmentado

### Video Original
* Presenta tres robots en total y una pelota de color naranja[cite: 9].
* **Equipo_1:** Compuesto por dos robots de color verde[cite: 10]. Defienden la portería azul durante un tiempo[cite: 11].
* **Equipo_2:** Compuesto por un único robot de color blanco[cite: 10]. Este equipo logra anotar un gol en la portería azul[cite: 11].

### Video Segmentado
* Muestra los mismos eventos pero resaltando visualmente la pelota y los robots[cite: 12].
* Cada objeto se divide en las tres categorías mencionadas, asignándoles un color y una etiqueta (*label*) con un ID numérico que inicia desde 0[cite: 13, 14]:
  * **Equipo_1:** Color verde (Robot 0 y Robot 1)[cite: 14, 17].
  * **Equipo_2:** Color blanco (Robot 0)[cite: 14, 17].
  * **Pelota:** Color naranja (Pelota 0)[cite: 14, 17].
* Las máscaras de segmentación mantienen la consistencia a lo largo de todo el video[cite: 15].
* **Marcador dinámico:** En la esquina superior izquierda se visualiza un marcador negro[cite: 16]. Inicia en `0-0` y, en el instante en que la pelota cruza la portería izquierda, cambia a `1-0` junto con un mensaje en texto blanco: `"¡Gol en la portería izq!"`[cite: 16, 17].

---

## 💻 Requisitos del Hardware y Software

Para ejecutar la notebook correctamente, asegúrate de cumplir con lo siguiente[cite: 19]:

* **Repositorio de Meta:** Cumplir con los requerimientos mínimos del repositorio oficial de SAM 3 de Meta[cite: 20, 26].
* **FFmpeg:** Tener instalado FFmpeg en el sistema operativo y debidamente configurado en las variables de entorno (*PATH*) para su ejecución en CMD[cite: 22, 31].
* **Hugging Face Account:** Disponer de una cuenta en Hugging Face, haber solicitado acceso al modelo SAM 3 y contar con un token de autenticación (necesario solo para la primera descarga)[cite: 21, 24, 29, 30].
* **Dependencias de Python:** Se adjunta un archivo `requirements.txt` con las versiones de las librerías empleadas en este desarrollo[cite: 23].

---

## 🚀 Instrucciones de Instalación y Reproducción Paso a Paso

Sigue estos pasos en orden para montar el entorno y ejecutar la segmentación:

1. **Clonar el repositorio oficial** de SAM 3 de Facebook (Meta)[cite: 26].
2. **Instalar las librerías** requeridas incluidas en el archivo `.toml` del repositorio oficial de Meta[cite: 27].
3. **Instalar Triton** en tu entorno[cite: 28].
4. **Solicitar acceso** al modelo SAM 3 en Hugging Face y generar tu Token de autenticación[cite: 29, 30].
5. **Instalar FFmpeg** y habilitarlo en el *PATH* de tu computadora[cite: 31].
6. Configurar un archivo `.env` en la raíz del proyecto que contenga tu token de Hugging Face[cite: 33].
7. Colocar el video original (debe ser obligatoriamente el archivo `IMG_9856.MOV`, ya que los polígonos de detección de la portería están calibrados específicamente para las zonas de este video) dentro de la ruta: `assets/videos/`[cite: 37, 38].

### Ejecución de la Notebook (`test_multisegmentation_iter_video.ipynb`) [cite: 32]

* **Celda 1:** Realiza la autenticación con Hugging Face leyendo el archivo `.env`[cite: 33].
* **Celda 2:** Carga las funciones base de segmentación[cite: 34]. Contiene un diccionario para definir los colores por cada *prompt* y la función `etiqueta` encargada de transformar los textos de los *prompts* en los labels de los objetos[cite: 35, 36].
* **Celda 3:** Imprime la información del sistema y define la ruta del video origen en la variable `SOURCE_VIDEO`[cite: 39].
* **Celda 4:** Ejecuta la segmentación iterativa por capas empleando la lista de *prompts*[cite: 40]. *Nota: Asegúrate de que esta lista coincida exactamente con la configuración de colores y etiquetas de la celda 2[cite: 40].*
* **Celda 5 (Penúltima):** Permite visualizar el video procesado dentro del IDE de Jupyter (Nota: Solo es compatible con formatos `.mp4`)[cite: 41].
* **Celda 6 (Última):** Cierra el predictor y finaliza de manera segura la sesión del modelo[cite: 42].

---

## 📸 Capturas de Pantalla o GIFs
*(Espacio reservado para añadir imágenes/GIFs demostrativos del proceso de segmentación)* [cite: 43]

---

## 📱 Reel de Instagram
*(Espacio reservado para incluir el enlace al Reel demostrativo del proyecto)* [cite: 44]

---

## 📄 Licencia
*(Espacio reservado para definir la licencia del proyecto)* [cite: 45]
