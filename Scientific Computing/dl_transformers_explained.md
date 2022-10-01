
las redes estan adaptadas para los diferentes tipos de datos que usamos

redes convolucionales son para entender datos espaciales como imágenes
redes recurrentes para entender datos secuenciales como texto

para poder entender que tipo de mejoras nos ofrece un modelo como los transformers, primero tenemos que entender con qué herramientasz contábamos antes para procesamiento de lenguaje natural nlp.  

La pregunta es: 
si yo tengo una frase cualquiera, cómo la analizo? 

dada la naturaleza secuencial de una frase, donde cada palabra ocupa una posicion en el tiempo una tras otra, la estrategia que se ha venido utilizando en el campo del deep learning es la siguiente 

Tomamos una red neuronal normal, y le damos como input la primera palabra.

![[Pasted image 20221001193519.png]]
dotcsv



Interamente esta palabra se procesará multiplicándose capa tras capa con los parámetros aprendidos de la red. 

![[Pasted image 20221001193719.png]]
![[Pasted image 20221001193653.png]]

Esto es lo tipico de siempre, la novedad viene ahora y es que la informacion que ha sido procesada por la red ahora sera agregada a la nueva informacion que introduciremos en el siguiente paso de nuestra secuencia a la siguiente palabra. 
![[Pasted image 20221001193905.png]]

![[Pasted image 20221001194954.png]]
Conectar el output anterior con el input del procesamiento actual es lo que le da el nombre a este tipo de redes: las RNN

esto permite procesar palabras teniendo en cuenta el contexto de lo que vino antes 

El problema de las RNN es vanishing gradients y ... 
Es decir, que cuando se hace este proceso de nutrir el input con el output anterior muchas muchas veces, el peso que tienen durante el entrenamiento las primeras palabras respecto a las ultimas que hemos agregado es menor a efectos practicos. Esto es el equivalente a la red olvidando cuales eran las primeras palabras de nuestra frase y en consecuencia perdiendo informacion relevante. 

![[Pasted image 20221001195803.png]]

Este problema se soluciona con los mecanismos de atención. 

Recuerden que las palabras vienen representadas como vectores numéricos y multidimensionales que capturan gran parte de la información semántica y sintáctica de la palabra que representan y con los que podemos ademas operar matematicamente. 

Vectores cuya dirección en este espaciomultidimensional sea muy parecida, representan conceptos cuyas palabras tambien sean parecidas y se alejaran de aquellas palabras que poco tengan que ver. 

![[Pasted image 20221001200626.png]]


![[Pasted image 20221001200714.png]]


Matematicamente podriamos calcular este angulo para asi estudiar cual es la similitud entre palabras, frases o documentos. 

![[Pasted image 20221001200747.png]]

Nuestro objetivo es buscar una solución a este problema de falta de memoria que esta presente en las RNN, es decir esa falta de conexion que parece que existe entre palabras que estan muy distanciadas, que no nos permiten estudiar cuales son sus relaciones. 

Nuestro objetivo sera que cada una de las palabras de nuestra frase, no importa la distancia que hay entre ellas, pueda estudiar cual es su relacion con cada una de las otras palabras de la frase. 
Estamos buscando cual es la relacion de todas las palabras con todas las palabras. 


que tipo de relaciones esta buscando la red neuronal?
relaciones semanticas, etc... 

la pregunta es como podemos automatizar este proceso de busqueda de relaciones?? la idea es que si esas relaciones existen tendran que ser redes neuronales las que aprendan a encontrarlas. 

Para ello, lo que vamos a hacer sera entrenar a dos redes neuronales diferentes par que con estas palabras dadas como input (mismo input a cada red), aprendan a generar dos vectores distintos. 

![[Pasted image 20221001204635.png]]

Una de las redes generara un vector que servira para identificar las propiedades interesantes que caracterizan a dicha palabra. 
La otra red neuronal generara un vector que servira para describir aquellas propiedades interesantes que esta palabra esta buscando. 

Podemos usar la metafora de una llave y una cerradura. Podriamos decir que con cada palabra de nuestra secuencia, estas dos redes neuronales se van a encargar se van a encargar de aprender a generar una llave y una cerradura, llaves que podran interactuar con el resto de las cerraduras de las otras palabras. 

![[Pasted image 20221001205031.png]]

![[Pasted image 20221001205107.png]]
![[Pasted image 20221001205134.png]]

Tenemos que entender que estas llaves aqui son diferentes a las que solemos utilizar en la vida real, y es que aqui cada llave puede funcionar en distintas cerraduras con mejor o peor resultado. Pero en realidad con las redes neuronales no estamos trabajando ni con llaves ni con cerraduras, sino que con vectores. Tenemos un vector llave y un vector cerradura. 

![[Pasted image 20221001205344.png]]
Y por ser vectores (los llave y los cerradura) podemos opera 
