# CT2CT by Sergio Rivera - 2020/01/22
# Version 0.1.0-alpha -> [changelog](/changelog.md)

- If you want to read the Spanish version click [here](#spanish-version)
- Si quieres leer la versión en Español haz click [aquí](#spanish-version)

This project was mentioned in the AI YouTube channel DotCSV! ([link](https://youtu.be/BerOC6n8j9Q?t=1011) to the video)

# 💂‍♂️ENGLISH VERSION
# CT2CT: Resolution Augmentation of Computed Tomography (CT) Scans

## 📝Abstract
The reconstruction of 3D encephala requires to perform the patient a Computed Tomography exam so that "slices" or sections of their head are obtained. The use of conventional systems usually extracts between 100 and 300 slices per patient, higher numbers would imply a longer exposure of the patient to radiation. A 2009 study of medical centers in the San Francisco Bay Area calculated that there is one extra case of cancer for every 400 to 2,000 routine chest CT exams. This has been linked to the abusive execution of the phenomena known as "defensive medicine", meaning that many CT Scans are not necessary and its overuse can potentially harm the patient if performed repeatedly under the said practice.
Using the CT2CT system (based on Pix2Pix technology), it is now possible to achieve a high number of slices of the encephalon only by scanning a lower number of "key slices" that allow the model to predict the non-scanned parts of the brain. This way, the time of exposure to radiation gets reduced significantly and the number of 2D slices can even be increased by a factor of 10.

Original complete scan (240 frames) | Original Slices + Predictions (480 frames, 2x original)
---------------------- | -----------------------------
![Original Scan gif](/assets/original.gif) | ![Predicted Scan gif](/assets/results.gif)

## ⚙️How it works?
The CT2CT model obtains non-scanned intermediate layers from known scanned ones in order to augment the resolution of the 3D reconstruction of enchapla without requiring the patient to stay longer times exposed to radiation during medical exams.
Once the training has been completed, predictions of the brain structure of a patient can be asked to the model as many times as required (bearing in mind that little errors always add up).

## 🏋️Training
The training proccess works by choosing 3 known sections (A, B and C), the input for the generator is a merge of A and C (AmC) and the output obtained is compared with the discriminator unit to B.

Layer A | Layer B | Layer C
-------|--------|--------
![Layer A](/assets/A.jpg) | ![Layer B](/assets/B.jpg) | ![Layer C](/assets/C.jpg)

This way, the generator learns how to create images of intermediate slices of the encephalon since the information of A and C is contained in the merge of both images (AmC).

Input AmC | Prediction (10 epochs)[X] | Prediction (50 epochs)[X]
----------|-------------------------|------------------------
![Image AmC](/assets/AmC.jpg) | ![Prediction 10 epochs](/assets/B_10e.jpg) | ![Prediction 50 epochs](/assets/B_50e.jpg)

[X]: Generated from other AmC not showed here.

The model has been designed so that it only requires less than 100 slices (all results shown have been generated with only 80 images of training). 50 epochs have demonstrated a huge capacity for prediction.

## ✅Evaluation
CT2CT uses 20% (20 images in shown results) of the images of the dataset for evaluating the model.

## 🧔How can I use CT2CT?
Support for custom scans is possible but not easy to use unless you know how the code works. That feature will be added in a near future but you can follow a step-by-step guide in the CT2CT.ipynb to train a model, understand the process, see the results, and save the model.
I am currently developing the user-friendly dekstop version for getting a complete predicted scan.

## ❗Google Colaboratory
The code has been written in Google Colaboratory. If you want to use this software, please open CT2CT.ipynb in Google Colaboratory.

## ℹ️Extra information
During the process of the development of this software some interesting ideas have been raised for the future:
  Image 1: When all the predicted layers are joined together, a scanner of similar resolution of the original is obtained with the only difference that the represented encephalon DOES NOT EXIST. This is an interesting idea since the head that could be extracted in 3D would be based on the original patient's head, but completely new. Face could also be reconstructed and would also be based on a person but not exactly THAT person.
  Image 2: If the images from the dataset contain descriptive HUD, the software would understand it as part of the image and will try to also predict that text. This way, data that does not change and is shown, such as the name of the patient or the date of the exam, are reproduced perfectly. But data that is constantly changing like slice number or distance are predicted in a blury way. This happens because that piece of information is unkown to the software and to the user.
  
  | Image 1 | Image 2 |
  | --- | --- |
  | 3D Predicted Reconstruction | "Blury" HUD (upper left corner) |
  | ![Predicted face](/assets/face.jpg) | ![blury HUD](/assets/B_prediction.jpg) |
  
# 💃SPANISH VERSION
# CT2CT: Aumentación de la Resolución de Escáneres de Tomografía Computada (CT)

## 📝Abstracto
La reconstrucción 3D del encéfalo requiere de realizar un examen CT de Tomografía Computada al paciente para así obtener "capas" o secciones de la cabeza del individuo. Mediante sistemas convencionales se suelen extraer entre 100 y 300 capas por paciente, ya que números superiores implicarían una prolongación de la exposición del paciente a radiación ionizante.
Mediante el sistema CT2CT (basado en la tecnología Pix2Pix), se consigue aumentar radicalmente el número de capas internas del encéfalo con tan solo el escaneo de unas "capas clave" que permiten al modelo predecir las partes del cerebro que no se han escaneado. De esta manera se reduce el tiempo de exposición del paciente a la radiación y se puede llegar a aumentar el número de capas 2D incluso 10 veces el número de frames originales.

Escáner original (240 frames) | Capas originales + Predecidas (480 frames, 2x original)
---------------------- | -----------------------------
![Escáner original gif](/assets/original.gif) | ![Escáner predecido gif](/assets/results.gif)

## ⚙️Como funciona?
El modelo CT2CT obtiene capas intermedias de escaneos CT desconocidas para aumentar la resolución de las reconstrucciones 3D encefálicas sin necesidad de aumentar el tiempo de los exámenes médicos y, por ende, de exposición a la radiación.
Una vez el entrenamiento se ha realizado, se puede pedir al modelo predicciones tantas como se deseen (teniendo en cuenta que el error se va aumentando conforme se predicen capas).

## 🏋️Entrenamiento
El entrenamiento funciona escogiendo 3 secciones conocidas (A, B y C), el input para el generador es A unión C (AuC) y el output se compara con el discriminador con B.

Capa A | Capa B | Capa C
-------|--------|--------
![Capa A](/assets/A.jpg) | ![Capa B](/assets/B.jpg) | ![Capa C](/assets/C.jpg)

De esta manera, el generador aprende a crear imágenes de capas intermedias del encéfalo ya que la información de las capas A y C está condensada en la unión de ambas imágenes (AuC).

Input AuC | Predicción (10 epochs)[X] | Predicción (50 epochs)[X]
----------|-------------------------|------------------------
![Imagen AuC](/assets/AmC.jpg) | ![Predicción 10 epochs](/assets/B_10e.jpg) | ![Predicción 50 epochs](/assets/B_50e.jpg)

[X]: Generado por otro AuC no mostrado aquí.

El modelo ha sido diseñado para que solo requiera de tan solo 80 imágenes de entrenamiento para que sea útil para la gran mayoría de escaneos CT. 50 epochs han demostrado una gran capacidad de predicción.

## ✅Evaluación
CT2CT utiliza el 20% del dataset para la evaluación del modelo que jamás han sido previamente conocidas extraídas del propio escáner original.

## 🧔Como puedo usarlo yo?
Por el momento no es fácil de utilizar tus propios scans a no ser que entiendas el código. Esta funcionalidad será añadida en un futuro cercando pero puedes seguir la guía paso-por-paso abriendo CT2CT.ipyinb en Google Collaboratory para entrenar un modelo, ver los resultados y guardar el modelo entrenado.
Ahora mismo estoy desarrollando la aplicación de escritorio que permitirá conseguir un scan predecido al completo.

## ❗Google Colaboratory
El código está programado en Google Colaboratory. Si desesa utilizar este software, abra CT2CT.ipynb en Google Colaboratory.

## ℹ️Información Extra
En el proceso del desarollo de este software han surgido algunos temas de interés para el futuro:
  Imagen 1: Al juntar todas las capas predecidas de un paciente se puede obtener un escáner de igual resolución que el original con la distinción de que el encéfalo que se representa NO EXISTE! Es un tema interesante ya que la cabeza que se podría extraer en 3D sería del paciente pero al mismo tiempo no es 100% real? Interesante sin más.
  La recreación 3D de las facciones de la cara serían otro tema de interés ya que se trataría de un rostro que NO EXISTE pese a que está basado en el del paciente original.
  Imagen 2: Si las imágenes del escáner original tienen un HUD descriptivo, el software lo tomará como parte de la imagen a predecir e intentará predecir también el texto que la rodea. De esta manera, datos que no cambian y que se muestran, como el nombre del paciente o la fecha del examen son reproducidos a la perfección, pero datos como el número de capa o los milímetros avanzados se ven de manera borrosa ya que no existen esos datos pues son desconocidos para el software y para el humano.
  
  | Imagen 1 | Imagen 2 |
  | --- | --- |
  | Reconstrucción 3D Predecida | HUD "borroso" (esquina sup. izqda.) |
  | ![Cara predecida](/assets/face.jpg) | ![HUD borroso](/assets/B_prediction.jpg) |
