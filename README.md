# Robofut_UAM_Lerma

# Segmentación Iterativa de Video de Robots con SAM 3

[cite_start]Este repositorio contiene la solución para realizar la segmentación de objetos múltiples en video utilizando el modelo SAM 3 (Segment Anything Model 3) de Meta[cite: 26]. [cite_start]El proyecto procesa un video de robots jugando al fútbol, segmentando por capas los equipos y la pelota, además de actualizar dinámicamente un marcador cuando se anota un gol[cite: 3, 5, 6].

---

## 📋 Arquitectura y Enfoque de la Solución

[cite_start]La segmentación del video se realiza de forma **iterativa y por capas** utilizando la notebook `test_multisegmentation_iter_video.ipynb`[cite: 1, 2, 5]. [cite_start]En cada iteración se segmenta una categoría específica de objeto y el resultado sirve como entrada para la siguiente etapa[cite: 4, 6]:

1. [cite_start]**Iteración 1 (Equipo 1):** Segmenta los robots pertenecientes al Equipo 1[cite: 5].
2. [cite_start]**Iteración 2 (Equipo 2):** Toma el video resultante de la primera iteración y añade la segmentación de los robots del Equipo 2[cite: 6].
3. [cite_start]**Iteración 3 (Pelota):** Realiza la segmentación y detección de la pelota[cite: 6]. [cite_start]En esta etapa se evalúa si la pelota ingresa a las porterías para modificar el marcador en tiempo real y lanzar un mensaje de "¡Gol!"[cite: 6].

---

## 🎥 Descripción de los Videos

### Video Original
* [cite_start]**Contenido:** Tres robots y una pelota de color naranja[cite: 9].
* [cite_start]**Equipos:** * **Equipo 1:** Formado por dos robots de color verde[cite: 10]. [cite_start]Defienden la portería azul[cite: 11].
  * [cite_start]**Equipo 2:** Formado por un solo robot de color blanco[cite: 10].
* [cite_start]**Evento clave:** El Equipo 2 anota un gol metiendo la pelota en la portería azul[cite: 11].

### Video Segmentado
* [cite_start]Mantiene los mismos eventos del video original pero resalta los objetos por categorías con máscaras consistentes a lo largo del tiempo[cite: 12, 13, 15]:
  * [cite_start]**Equipo 1:** Robots resaltados en color verde (etiquetados como `robot 0` y `robot 1`)[cite: 14, 17].
  * [cite_start]**Equipo 2:** Robot resaltado en color blanco (etiquetado como `robot 0`)[cite: 14, 17].
  * [cite_start]**Pelota:** Segmentada en color naranja (etiquetada como `id 0`)[cite: 14, 17].
* [cite_start]**Marcador Dinámico:** Se muestra un marcador negro en la parte superior izquierda (inicia en `0-0`)[cite: 16, 17]. [cite_start]Al entrar la pelota a la portería izquierda, cambia a `1-0` y muestra el mensaje en color blanco: **"¡Gol en la portería izq!"**[cite: 16, 17].

---

## 🛠️ Requisitos del Sistema

[cite_start]Para ejecutar correctamente la notebook, asegúrate de cumplir con lo siguiente[cite: 19]:

1. [cite_start]**Hardware y Software de Meta:** Cumplir con los requerimientos mínimos del [repositorio oficial de Meta SAM 3](https://github.com/facebookresearch/segment-anything-2) *(Nota: Validar enlace)*[cite: 20, 26].
2. [cite_start]**Hugging Face Token:** Se requiere un token de lectura para autenticar la cuenta y descargar el modelo por primera vez[cite: 21, 24].
3. [cite_start]**FFmpeg:** Debe estar instalado en la computadora y correctamente añadido a las variables de entorno (`PATH`) para su ejecución por comandos en la terminal[cite: 22, 31].
4. [cite_start]**Triton:** Requerido para la optimización del modelo[cite: 28].

> [cite_start]💡 **Nota:** Se adjunta el archivo `requirements.txt` con las versiones exactas de las librerías utilizadas en este proyecto[cite: 23].

---

## 🚀 Instalación y Reproducción Paso a Paso

[cite_start]Sigue estos pasos para configurar el entorno y ejecutar la segmentación[cite: 25]:

### 1. Clonar e instalar dependencias de SAM 3
[cite_start]Primero, clona el repositorio oficial de SAM 3 de Meta e instala sus librerías a través de su archivo `.toml`[cite: 26, 27]:
```bash
git clone <URL_DEL_REPOSITORIO_OFICIAL_DE_SAM3>
cd <REPOSITORIO_DE_SAM3>
# Instalar dependencias del archivo .toml
