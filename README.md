# Robofut_UAM_Lerma

# Segmentación Multi-Objeto por Iteraciones en Video

Este proyecto implementa un enfoque de segmentación por capas e iterativo para identificar y rastrear múltiples objetos (equipos de robots y la pelota) en un video utilizando el modelo **SAM 3** (Segment Anything Model 3) de Meta.

---

## 🛠️ Descripción del Enfoque y Arquitectura de la Solución

La notebook principal (`test_multisegmentation_iter_video.ipynb`) contiene todo el código necesario para procesar y segmentar el video original. 

La segmentación del video requiere clasificar múltiples objetos pertenecientes a tres categorías específicas: **Equipo_1**, **Equipo_2** y **pelota**. El pipeline funciona de manera **iterativa y por capas**:

1. **Primera Iteración (Equipo_1):** Se segmentan únicamente los robots pertenecientes al Equipo_1. El resultado es un video intermedio con esta capa aislada.
2. **Segunda Iteración (Equipo_2):** Se toma el video resultante de la iteración anterior y se realiza la segmentación sobre los robots del Equipo_2.
3. **Última Iteración (Pelota y Marcador):** Se procesa la pelota y se aplica una detección basada en zonas (porterías izquierda y derecha) para modificar dinámicamente un marcador en pantalla y lanzar un mensaje de anotación.

---

## 📹 Descripción del Video Original y Segmentado

### Video Original
* Presenta tres robots en total y una pelota de color naranja.
* **Equipo_1:** Compuesto por dos robots de color verde. Defienden la portería azul durante un tiempo.
* **Equipo_2:** Compuesto por un único robot de color blanco. Este equipo logra anotar un gol en la portería azul.

### Video Segmentado
* Muestra los mismos eventos pero resaltando visualmente la pelota y los robots.
* Cada objeto se divide en las tres categorías mencionadas, asignándoles un color y una etiqueta (*label*) con un ID numérico que inicia desde 0:
  * **Equipo_1:** Color verde (Robot 0 y Robot 1).
  * **Equipo_2:** Color blanco (Robot 0).
  * **Pelota:** Color naranja (Pelota 0).
* Las máscaras de segmentación mantienen la consistencia a lo largo de todo el video.
* **Marcador dinámico:** En la esquina superior izquierda se visualiza un marcador negro. Inicia en `0-0` y, en el instante en que la pelota cruza la portería izquierda, cambia a `1-0` junto con un mensaje en texto blanco: `"¡Gol en la portería izq!"`.

---

## 💻 Requisitos del Hardware y Software

Para ejecutar la notebook correctamente, asegúrate de cumplir con lo siguiente:

* **Repositorio de Meta:** Cumplir con los requerimientos mínimos del repositorio oficial de SAM 3 de Meta.
* **FFmpeg:** Tener instalado FFmpeg en el sistema operativo y debidamente configurado en las variables de entorno (*PATH*) para su ejecución en CMD.
* **Hugging Face Account:** Disponer de una cuenta en Hugging Face, haber solicitado acceso al modelo SAM 3 y contar con un token de autenticación (necesario solo para la primera descarga).
* **Dependencias de Python:** Se adjunta un archivo `requirements.txt` con las versiones de las librerías empleadas en este desarrollo.

---

## 🚀 Instrucciones de Instalación y Reproducción Paso a Paso

Sigue estos pasos en orden para montar el entorno y ejecutar la segmentación:

1. **Clonar el repositorio oficial** de SAM 3 de Facebook (Meta).
2. **Instalar las librerías** requeridas incluidas en el archivo `.toml` del repositorio oficial de Meta.
3. **Instalar Triton** en tu entorno.
4. **Solicitar acceso** al modelo SAM 3 en Hugging Face y generar tu Token de autenticación.
5. **Instalar FFmpeg** y habilitarlo en el *PATH* de tu computadora.
6. Configurar un archivo `.env` en la raíz del proyecto que contenga tu token de Hugging Face.
7. Colocar el video original (debe ser obligatoriamente el archivo `IMG_9856.MOV`, ya que los polígonos de detección de la portería están calibrados específicamente para las zonas de este video) dentro de la ruta: `assets/videos/`.

### Ejecución de la Notebook (`test_multisegmentation_iter_video.ipynb`)

* **Celda 1:** Realiza la autenticación con Hugging Face leyendo el archivo `.env`.
* **Celda 2:** Carga las funciones base de segmentación. Contiene un diccionario para definir los colores por cada *prompt* y la función `etiqueta` encargada de transformar los textos de los *prompts* en los labels de los objetos.
* **Celda 3:** Imprime la información del sistema y define la ruta del video origen en la variable `SOURCE_VIDEO`.
* **Celda 4:** Ejecuta la segmentación iterativa por capas empleando la lista de *prompts*. *Nota: Asegúrate de que esta lista coincida exactamente con la configuración de colores y etiquetas de la celda 2.*
* **Celda 5 (Penúltima):** Permite visualizar el video procesado dentro del IDE de Jupyter (Nota: Solo es compatible con formatos `.mp4`).
* **Celda 6 (Última):** Cierra el predictor y finaliza de manera segura la sesión del modelo.

---

## 📸 Capturas de Pantalla o GIFs
![](robofut_gif.gif)
![](robofut_gif_2.gif)
<img width="1842" height="877" alt="Zona_gol" src="https://github.com/user-attachments/assets/511af8ef-99c0-41aa-b7c0-8314ace270ba" />
<img width="1167" height="972" alt="image" src="https://github.com/user-attachments/assets/78f90546-c7b0-406d-9b38-9389a2b35107" />
<img width="1171" height="1010" alt="image" src="https://github.com/user-attachments/assets/b51bda4a-7a0b-4e11-b04a-1e47b0214489" />
<img width="1175" height="1011" alt="image" src="https://github.com/user-attachments/assets/dedf7a4d-c812-492a-bdd2-c9163922f111" />
<img width="1171" height="1007" alt="image" src="https://github.com/user-attachments/assets/4e7472f9-0210-4a57-92e0-e8bcc126b5d1" />
<img width="1187" height="1007" alt="image" src="https://github.com/user-attachments/assets/edb9d16a-b02a-43d1-ac89-fbce635c5af6" />


---
## Video
*(El video se encuentra en Youtube)* \
![Video](https://youtube.com/shorts/447f1iQCiPE?feature=share)](https://youtube.com/shorts/447f1iQCiPE?feature=share)

---
## 📱 Reel de Instagram
*(Espacio reservado para incluir el enlace al Reel demostrativo del proyecto)*

---

## 📄 Licencia
*(Espacio reservado para definir la licencia del proyecto)* [cite: 45]
