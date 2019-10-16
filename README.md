# CT2CT by Sergio Rivera
- If you want to read the Spanish version [click here](#spanish-version)
- Si quieres leer la versión en Español [haz click aquí](#spanish-version)

# ENGLISH VERSION
# CT2CT: Resolution Augmentation of Computed Tomography Scans

## Abstract
The reconstruction of 3D encephala requires to perform the patient a Computed Tomography exam so that "slices" or sections of their head are obtained. The use of conventional systems usually extracts between 100 and 300 slices per patient, higher numbers would imply a longer exposure of the patient to major levels of radiation.
Using the CT2CT system (based on Pix2Pix technology), it is now achieved a higher number of inner slices of the encephalon only by scanning specific "key slices" that allow the model to predict the non-scanned slices in between them. This way, the time of exposure to radiation gets reduced significantly and the number of 2D slices raises for a better reconstruction of the 3D representation of the patient's head.

## How it works?
The CT2CT model obtains un-scanned intermediate layers from known scanned ones in order to augment the resolution of the 3D reconstruction of enchapla without requiring the patient to stay longer times exposed to radiation during medical exams.
Medicine is a field where accuracy is of extreme importance, the CT2CT model has to be retrained every time the target patient changes. This facilitates the AI to adapt to the new intrinsic patterns of the nature of the encephalon of the new patient without mixing previous brain structures of other patients. Once the training has been completed for one target patient, predictions of the brain structure of that patient can be asked to the model as many times as required (bearing in mind that little errors always add up) without having to repeat training constantly.

## Training
The training proccess works by choosing 3 known sections (A, B and C), the input for the generator is X (AxC) and the output obtained is compared with the discriminator unit to B.

Layer A | Layer B | Layer C
-------|--------|--------
![Layer A](/assets/A.jpg) | ![Layer B](/assets/B.jpg) | ![Layer C](/assets/C.jpg)

This way, the generator learns how to create images of intermediate slices of the encephalon since the information of A and C is condensed in the multiplication of both images (X).

Input AxC | Prediction (100 epochs) | Prediction (500 epochs)
----------|-------------------------|------------------------
![Image AxC](/assets/AxC.jpg) | ![Prediction](/assets/B_prediction.jpg) | Image Not Available

The model has been designed so that it only requires less than 100 images (all results shown have been generated with only 80 images of training). 500 epochs have demonstrated a huge capacity of prediction although the only drawback is the computational time. Said training was on-going for at least 12 hours, which is totally recommended if you need to generate a high accuracy scan. In contrary, if you only want the resolution of the 3D reconstruction to agument for visual purposes, 100 epochs are more than enough.

## Evaluation
CT2CT uses 20% (20 images in shown results) of the images of the dataset for evaluating the model.

## Parameters
All parameters, like "PATHS", "epochs" or "slices" can be modified in the first lines of code (explained through comments). The project already comes a default scanner with 240 slices which has been used during the whole development of the model.

## How can I use CT2CT?
It is recommended to use the default scanner (rawIMG, download zip folder included in this repository and upload the images to Drive, if you don't want to touch the code upload it to a folder like this: /brain_ct/PATIENT/rawIMG, this path is registered in code and can be changed in the variable RAW_PATH). If you prefer to use your own scans then this instructions must be followed:
  1. Add the images to the rawIMG folder under the names /IMG-0001-XXXX.jpg being X the number of the slice (i.e. /IMG-0001-0123.jpg).
  2. Change the parameter "slices" to the number of images previously uploaded to the rawIMG folder in Drive.

The software outputs a completely new scan generated in brain_ct/results. 
This is the final output (known slices with predictions in between).

## Google Colaboratory
The code has been written in Google Colaboratory. Future updates will come in order to improve the user experience and try to make it user-friendly having in mind non-developers.
These are the parameters of the environment:
  1. Execution environment -> Change type of execution environment -> GPU
  2. If the training is halted by the automatic disconnection of the user from session, I recomend using an autoclicker so that Google thinks you are actually doing something with the code and, therefore, not being kicked.

## Extra information
During the process of the development of this software some interesting ideas have been raised for the future:
  Image 1: When all the predicted layers are joined together, a scanner of similar resolution of the original is obtained with the only difference that the represented encephalon DOES NOT EXIST. This is an interesting idea since the head that could be extracted in 3D would be based on the original patient's head, but completely new. Face could also be reconstructed and would also be based on a person but not exactly THAT person.
  Image 2: If the images from the dataset contain descriptive HUD, the software would understand it as part of the image and will try to also predict that text. This way, data that does not change and is shown, such as the name of the patient or the date of the exam, are reproduced perfectly. But data that is constantly changing like slice number or distance are predicted in a blury way. This happens because that piece of information is unkown to the software and to the user.
  
  | Image 1 | Image 2 |
  | --- | --- |
  | 3D Predicted Reconstruction | "Blury" HUD (upper left corner) |
  | ![Predicted face](/assets/face.jpg) | ![blury HUD](/assets/B_prediction.jpg) |
  
# SPANISH VERSION
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
