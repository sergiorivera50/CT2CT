# CT2CT: Resolution Augmentation of Computed Tomography Scans

## Abstract
The reconstruction of 3D encephala requires to perform the patient a Computed Tomography exam so that "slices" or sections of their head are obtained. The use of conventional systems usually extracts between 100 and 300 slices per patient, higher numbers would imply a longer exposure of the patient to major levels of radiation.
Using the CT2CT system (based on Pix2Pix technology), it is now achieved a higher number of inner slices of the encephalon only by scanning specific "key slices" that allow the model to predict the non-scanned slices in between them. This way, the time of exposure to radiation gets reduced significantly and the number of 2D slices raises for a better reconstruction of the 3D representation of the patient's head.

## Funcionalidad
El modelo CT2CT obtiene capas intermedias de escaneos CT desconocidas para aumentar la resolución de las reconstrucciones 3D encefálicas sin necesidad de aumentar el tiempo de los exámenes médicos y, por ende, de exposición a la radiación.
Ya que en el campo de la medicina la precisión es de extrema importancia, el entrenamiento del modelo se ha de repetir cada vez que se trate con un nuevo paciente. Así se consigue que la IA se adapte a los patrones específicos de cada encéfalo sin mezclarlos entre pacientes.
Una vez el entrenamiento se ha realizado, se puede pedir al modelo predicciones tantas como se deseen de manera que no es necesario repetir el proceso constantemente.

## Entrenamiento
El entrenamiento funciona escogiendo 3 secciones conocidas (A, B y C), el input para el generador es X (AxC) y el output se compara con el discriminador con B.

Capa A | Capa B | Capa C
-------|--------|--------
![Capa A](/assets/A.jpg) | ![Capa B](/assets/B.jpg) | ![Capa C](/assets/C.jpg)

De esta manera, el generador aprende a crear imágenes de capas intermedias del encéfalo ya que la información de las capas A y C está condensada en la multiplicación de ambas imágenes (X).

Input AxC | Predicción (100 epochs) | Predicción (500 epochs)
----------|-------------------------|------------------------
![Imagen AxC](/assets/AxC.jpg) | ![Predicción](/assets/B_prediction.jpg) | Imagen No Disponible

El modelo ha sido diseñado para que solo requiera de tan solo 80 imágenes de entrenamiento para que sea útil para la gran mayoría de escaneos CT. 500 epochs han demostrado una gran capacidad de predicción aunque el único inconveniente es el tiempo de computación. Dicho entrenamiento tardó una noche aproximadamente, lo cual es totalmente recomendable si se necesita generar un escáner de alta precisión.
Por el contrario, si tan solo se quiere aumentar la resolución de la reconstrucción 3D de forma visual, 100 epochs son más que suficientes.

## Evaluación
CT2CT utiliza 20 imágenes para la evaluación del modelo que jamás han sido previamente conocidas extraídas del propio escáner original.

## Parámetros
Todos los parámetros como los PATHS, epochs o slices del escaner pueden ser modificados en las primeras celdas del código (explicado mediante comentarios). El proyecto viene con un escáner por defecto de 240 capas o "slices" y es el que se ha utilizado en todo momento para el desarrollo del modelo.

## Uso del Software
Es recomendable utilizar el escaner por defecto (rawIMG, descargar carpeta zip incluida en el repositorio y subir a Drive las imágenes al RAW_PATH: /brain_ct/PATIENT/rawIMG) ya que esto es un proyecto no comercial. Pero si se desea hacer pruebas con otros escáneres habrá que seguir las siguientes instrucciones:
  1. Añadir las imágenes a la carpeta rawIMG bajo el nombre /IMG-0001-XXXX.jpg siendo X el número de capa (ej, /IMG-0001-0214.jpg)
  2. Cambiar el parámetro "slices" al número de imágenes previamente introducidas en la carpeta rawIMG.

El software obtiene como output un escáner totalmente generado en brain_ct/results.

## Google Colaboratory
El código está programado para que su uso sea en el entorno de Google Colaboratory. En el futuro se realizarán actualizaciones para mejorar la experiencia y que sea más facil el uso del software para usuarios no-desarrolladores.
Estos son los parámetros del entorno:
  1. Entorno de ejecución -> Cambiar tipo de entorno de ejecución -> GPU
  2. En caso de que en el entrenamiento desconecte al usuario de la sesión, recomiendo el uso de un autoclicker para que no cese la     actividad y google no te expulse del software.

## Observaciones
En el proceso del desarollo de este software han surgido algunos temas de interés para el futuro:
  Imagen 1: Al juntar todas las capas predecidas de un paciente se puede obtener un escáner de igual resolución que el original con la distinción de que el encéfalo que se representa NO EXISTE! Es un tema interesante ya que la cabeza que se podría extraer en 3D sería del paciente pero al mismo tiempo no es 100% real? Interesante sin más.
  La recreación 3D de las facciones de la cara serían otro tema de interés ya que se trataría de un rostro que NO EXISTE pese a que está basado en el del paciente original.
  Imagen 2: Si las imágenes del escáner original tienen un HUD descriptivo, el software lo tomará como parte de la imagen a predecir e intentará predecir también el texto que la rodea. De esta manera, datos que no cambian y que se muestran, como el nombre del paciente o la fecha del examen son reproducidos a la perfección, pero datos como el número de capa o los milímetros avanzados se ven de manera borrosa ya que no existen esos datos pues son desconocidos para el software y para el humano.
  
  | Imagen 1 | Imagen 2 |
  | --- | --- |
  | Reconstrucción 3D Predecida | HUD "borroso" (esquina sup. izqda.) |
  | ![Cara predecida](/assets/face.jpg) | ![HUD borroso](/assets/B_prediction.jpg) |

# CT2CT: Aumentación de la Resolución de Escáneres de Tomografía Computada (CT)

## Abstracto
La reconstrucción 3D de encéfalos requiere de realizar un examen CT de Tomografía Computada al paciente para así obtener "capas" o secciones de la cabeza del individuo. Mediante sistemas convencionales se suelen extraer entre 100 y 300 capas por paciente, ya que números superiores implicarían una prolongación de la exposición del paciente a niveles de radiación importantes.
Mediante el sistema CT2CT (basado en la tecnología Pix2Pix), se consigue aumentar radicalmente el número de capas internas del encéfalo con tan solo el escaneo de unos "key slices" o capas clave que permiten al modelo predecir las capas que no se han escaneado. De esta manera se reduce el tiempo de exposición del paciente a la radiación y se aumenta el número de capas 2D para la reconstrucción 3D del encéfalo.

## Funcionalidad
El modelo CT2CT obtiene capas intermedias de escaneos CT desconocidas para aumentar la resolución de las reconstrucciones 3D encefálicas sin necesidad de aumentar el tiempo de los exámenes médicos y, por ende, de exposición a la radiación.
Ya que en el campo de la medicina la precisión es de extrema importancia, el entrenamiento del modelo se ha de repetir cada vez que se trate con un nuevo paciente. Así se consigue que la IA se adapte a los patrones específicos de cada encéfalo sin mezclarlos entre pacientes.
Una vez el entrenamiento se ha realizado, se puede pedir al modelo predicciones tantas como se deseen de manera que no es necesario repetir el proceso constantemente.

## Entrenamiento
El entrenamiento funciona escogiendo 3 secciones conocidas (A, B y C), el input para el generador es X (AxC) y el output se compara con el discriminador con B.

Capa A | Capa B | Capa C
-------|--------|--------
![Capa A](/assets/A.jpg) | ![Capa B](/assets/B.jpg) | ![Capa C](/assets/C.jpg)

De esta manera, el generador aprende a crear imágenes de capas intermedias del encéfalo ya que la información de las capas A y C está condensada en la multiplicación de ambas imágenes (X).

Input AxC | Predicción (100 epochs) | Predicción (500 epochs)
----------|-------------------------|------------------------
![Imagen AxC](/assets/AxC.jpg) | ![Predicción](/assets/B_prediction.jpg) | Imagen No Disponible

El modelo ha sido diseñado para que solo requiera de tan solo 80 imágenes de entrenamiento para que sea útil para la gran mayoría de escaneos CT. 500 epochs han demostrado una gran capacidad de predicción aunque el único inconveniente es el tiempo de computación. Dicho entrenamiento tardó una noche aproximadamente, lo cual es totalmente recomendable si se necesita generar un escáner de alta precisión.
Por el contrario, si tan solo se quiere aumentar la resolución de la reconstrucción 3D de forma visual, 100 epochs son más que suficientes.

## Evaluación
CT2CT utiliza 20 imágenes para la evaluación del modelo que jamás han sido previamente conocidas extraídas del propio escáner original.

## Parámetros
Todos los parámetros como los PATHS, epochs o slices del escaner pueden ser modificados en las primeras celdas del código (explicado mediante comentarios). El proyecto viene con un escáner por defecto de 240 capas o "slices" y es el que se ha utilizado en todo momento para el desarrollo del modelo.

## Uso del Software
Es recomendable utilizar el escaner por defecto (rawIMG, descargar carpeta zip incluida en el repositorio y subir a Drive las imágenes al RAW_PATH: /brain_ct/PATIENT/rawIMG) ya que esto es un proyecto no comercial. Pero si se desea hacer pruebas con otros escáneres habrá que seguir las siguientes instrucciones:
  1. Añadir las imágenes a la carpeta rawIMG bajo el nombre /IMG-0001-XXXX.jpg siendo X el número de capa (ej, /IMG-0001-0214.jpg)
  2. Cambiar el parámetro "slices" al número de imágenes previamente introducidas en la carpeta rawIMG.

El software obtiene como output un escáner totalmente generado en brain_ct/results.

## Google Colaboratory
El código está programado para que su uso sea en el entorno de Google Colaboratory. En el futuro se realizarán actualizaciones para mejorar la experiencia y que sea más facil el uso del software para usuarios no-desarrolladores.
Estos son los parámetros del entorno:
  1. Entorno de ejecución -> Cambiar tipo de entorno de ejecución -> GPU
  2. En caso de que en el entrenamiento desconecte al usuario de la sesión, recomiendo el uso de un autoclicker para que no cese la     actividad y google no te expulse del software.

## Observaciones
En el proceso del desarollo de este software han surgido algunos temas de interés para el futuro:
  Imagen 1: Al juntar todas las capas predecidas de un paciente se puede obtener un escáner de igual resolución que el original con la distinción de que el encéfalo que se representa NO EXISTE! Es un tema interesante ya que la cabeza que se podría extraer en 3D sería del paciente pero al mismo tiempo no es 100% real? Interesante sin más.
  La recreación 3D de las facciones de la cara serían otro tema de interés ya que se trataría de un rostro que NO EXISTE pese a que está basado en el del paciente original.
  Imagen 2: Si las imágenes del escáner original tienen un HUD descriptivo, el software lo tomará como parte de la imagen a predecir e intentará predecir también el texto que la rodea. De esta manera, datos que no cambian y que se muestran, como el nombre del paciente o la fecha del examen son reproducidos a la perfección, pero datos como el número de capa o los milímetros avanzados se ven de manera borrosa ya que no existen esos datos pues son desconocidos para el software y para el humano.
  
  | Imagen 1 | Imagen 2 |
  | --- | --- |
  | Reconstrucción 3D Predecida | HUD "borroso" (esquina sup. izqda.) |
  | ![Cara predecida](/assets/face.jpg) | ![HUD borroso](/assets/B_prediction.jpg) |
