Y luego nos fuimos adaptando y perfeccionando a la naturaleza
de los diferentes tipos de datos que usábamos.
Redes neuronales conversacionales para entender datos espaciales
como imágenes, redes neuronales recurrentes
para entender los datos secuenciales como textos, redes neuronales
que no sólo se utilizaban para aprender a analizar patrones,
sino que también eran capaces de generarlos con resultados
que todos vosotros habéis podido ver aquí en el canal.
Y si bien el desarrollo
de esta tecnología en tan poquito tiempo ha sido impresionante,
es en 2017 cuando una nueva publicación
empieza literalmente a transformar nuestra concepción
de lo que la inteligencia artificial es capaz de hacer.
Aparecen los Transformers y desde ese momento
no hemos parado de ver
grandísimos logros del live learning que en su funcionamiento se apoyan
principalmente en el rendimiento que esta tecnología ofrece.
Alpha Fold 2 para analizar secuencias de datos ge nómicos,
Tesla en su sistema de conducción Auto Pilot GPT3 para la modelización
y generación de texto o Transformers para que las VQGAN
de este paper de aquí puedan generar estas espectaculares obras de arte.
De todo esto ya hemos hablado en el canal siempre buena información,
pero hoy os voy a llevar más allá.
Hoy por fin es el comienzo de una serie de vídeo
donde os voy a explicar cuál es la intuición tras el funcionamiento

de los Transformers y por dónde vamos a empezar.

Atención! Para poder entender

qué tipo de mejoras nos ofrece un modelo como los Transformers.

Primero tenemos que entender con qué herramientas contábamos antes,

en concreto para tareas

de procesamiento del lenguaje natural, que es de donde surge todo esto.

Vamos, que la pregunta aquí es si yo tengo una frase como esta,

como la analizo?

Pues dada la naturaleza secuencial de una frase donde

cada palabra ocupa una posición en el tiempo una tras otra.

La estrategia que se ha venido

utilizando desde el

campo del dip learning es la siguiente Tomamos una red neuronal normal

y le damos como input la primera palabra.

Internamente esta palabra se procesará multiplicándose

capa tras capa con los parámetros aprendidos de la red.

Vamos, lo típico de siempre.

Sin embargo, la novedad viene ahora y es que la información

que ha sido procesada por la red ahora será agregada a la nueva información

que introduciremos en el siguiente paso de nuestra secuencia

a la siguiente palabra.

Así, haciendo este proceso de encadenar el output de la red

con el input del siguiente paso

y dejando que analice todas las palabras,

acabaremos en un punto donde toda la información
de nuestra secuencia habrá sido procesada y analizada,
y cuyo resultado tendremos en este punto de aquí.
Es esta idea que parece sacada de la película
de Ciempiés humanos de conectar
el procesamiento del output anterior con el input del procesamiento actual,
lo que da nombre a este tipo de redes.
Las redes neuronales recurrentes y estas responden
a una idea muy intuitiva.
Y es que tú, cuando lees ahora que me estás escuchando, vas
procesando cada palabra individualmente, pero apoyándote
del contexto de todas las palabras que he dicho anteriormente.
Tú cuando lees seguramente lo haces de manera secuencial,

no escaneas automáticamente todas las palabras

que aparecen en la página de un libro, verdad?

Pues esto es igual.

Con este tipo de redes es con lo que en el pasado

se construía la mayoría de generadores de texto, traductores neuronales

y otras tantas movidas que requerían el análisis de secuencias

como por ejemplo, cuál era la secuencia de acciones

que a un jugador del DOTA 2 hacía con el ratón y el teclado.

Como vimos en el vídeo de Tesla,

una día de hoy encontramos proyectos que se siguen pasando

en este tipo de redes neuronales recurrentes

y parecería que todo es maravilloso e ideal con este tipo de redes

neuronales recurrentes, excepto por un pequeño detalle.

Y es que este vídeo no se titula

Las redes neuronales recurrentes son maravillosas e ideales.

Quiero que me respondas una pregunta ¿Cuál ha sido

la primera palabra que he pronunciado al comienzo de este vídeo?

Si no te acuerdas, no pasa nada.

Y es que es normal

que después de haber escupido tantas palabras durante el vídeo

tú no hayas sido capaz de retenerla.

Pero y si te dijera que este problema no es exclusivo de tu limitado

cerebro de primate, no?

Y si te dijera que este es el

principal problema al que se enfrentan las redes neuronales recurrentes?

Y es que está comprobado que uno de los principales problemas

de este tipo de redes es que cuando este proceso de nutrir

el input con el aporte anterior se repite durante muchos pasos

el peso que tienen

durante el entrenamiento, las primeras palabras

respecto a las últimas que hemos agregado

es menor a efectos prácticos, esto es el equivalente a la red,

olvidando cuáles eran las primeras palabras de nuestra frase.

Y esto es un problema?

Pues sí, ya que frases como "el pangolín

dormía plácidamente colgado de la rama de un árbol usando su cola",

no permitiría la red de encontrar una relación

que es interesante en este caso.

Y es que su hace referencia

a la posesión que tiene en este caso el sujeto de la frase el pan bolín.

Cómo solucionamos este problema?

Pues bien, vamos a poner atención, pero literalmente

vamos a aplicar una serie de mecanismos que sirven de alternativa

para dar solución a este problema de falta de memoria,

unos mecanismos que se denominan mecanismos de atención.

Y antes de empezar con las matemáticas épicas, dejadme recordar una cosa

hasta el momento hemos estado hablando de redes

que procesan y analizan palabras, pero si habéis seguido

la serie de vídeos sobre NLP, Natural Language Processing,

tenéis que saber que estas palabras

en realidad vienen representadas como vectores numéricos,

vectores multidimensionales

que capturan gran parte de la

información semántica y sintáctica de la palabra que representan

y con los que podemos además operar matemáticamente.

Por ejemplo, vectores cuya dirección en este espacio multidimensional

sea muy parecida,

representarÃn a conceptos cuyas palabras también sean parecidas

y se alejarán de aquellas palabras que poco tengan que ver .

Matemáticamente, este ángulo además lo podríamos calcular para así

estudiar cuál es la similitud entre palabras, frases o documentos.

Si queréis conocer más en detalle sobre esto, recomiendo ver estos

dos vídeos de aquí que dan comienzo a la serie de NLP.

Pero por ahora para este vídeo me vale con que entendáis que aquí

cada palabra viene representada

por uno de estos vectores matemáticos y con ellos vamos a trabajar,

porque aquí nuestro objetivo es buscar una solución

a este problema de falta de memoria

que parece estar presente en las redes neuronales recurrentes.

Esa falta de conexión

que parece que existe entre palabras que están muy distanciadas,

que no nos permiten estudiar cuáles son sus relaciones.

Veamos, por ejemplo, con esta frase de aquí el pangolín duerme en su árbol.

Aquí nuestro objetivo será que cada una de las palabras de nuestra frase,

no importa la distancia que hay entre ellas, pueda estudiar

cuál es su relación con cada una de las otras palabras de la frase

estamos buscando.

Cuál es la relación de todas las palabras con todas las palabras?

Y te estarás preguntando

qué tipo de relaciones estamos buscando nosotros, no?

Qué tipo de relaciones está buscando la red neuronal?

Por ejemplo, existe una relación interesante entre la palabra Pango

Linh y àrbol que semánticamente nos traslada al concepto de naturaleza

o la palabra duerme, que como verbo de la oración estará

muy conectado al sujeto Colin, quién es el que realiza la acción?

Así es como vemos que cada palabra

puede tener una relación interesante o no

con cualquiera de las otras palabras que conforman a nuestra frase.

La pregunta es cómo

podemos automatizar este proceso de búsqueda de relaciones?

Cómo lo hacemos?

Pues la idea es que si esas relaciones existen,

tendrán que ser redes neuronales las que aprendan a encontrarlas.

Para ello, lo que vamos a hacer será

entrenar a dos redes neuronales diferentes para que con estas palabras

dadas como input, aprendan a generar dos vectores distintos.

Una de las redes generará un vector que servirá para identificar

las propiedades interesantes que caracterizan a dicha palabra.

Y por otro lado, la otra red neuronal generará un vector

que servirá para describir

aquellas propiedades interesantes que esta palabra está buscando.

Tal y como suena esto, casi parece que estamos entrenando

estas redes neuronales para generarse un perfil de Tinder.

Hola que tal? Soy la segunda palabra de esta frase.

Soy el pan Goli y esta de aquí

se encargaría de generar su descripción, que diría algo

así como yo soy un sujeto que tengo una parte muy animal

y que estoy interesado por la naturaleza y esta otra red

generaría la descripción de lo que está buscando,

pues actualmente lo que estoy buscando es otra palabra interesada

por la naturaleza

a poder ser verbos que puedan dar un poco de sentido a lo que hago.

Y así, si apareciera otra palabra

cuya descripción fuera compatible con lo que busca nuestro pangolin,

esto debería de generar un match, algo que como toda cita

Tinder, sabemos como va a acabar esto de aquí es otra forma de entenderlo.

Sería mediante la metáfora de una llave y una cerradura.

Podríamos decir que con cada palabra de nuestra secuencia,

estas dos redes neuronales

se van a encargar de aprender a generar una llave y una cerradura,

llaves que podrán interactuar

con el resto de cerraduras de las otras palabras.

Claro, tenemos que entender que estas llaves

aquí son diferentes a las que solemos utilizar en la vida real.

Y es que aquí cada llave

puede funcionar en distintas cerraduras con mejor o peor resultado.

De hecho, quieren ver cómo funcionan matemáticamente estos candados,

pues en realidad es, como ya he dicho antes, aquí no estamos trabajando

ni con llaves , ni con cerraduras, ni perfiles de Tinder,

sino con vectores.

Esto de aquí es un vector y esto de aquí es otro vector.

Y como vectores que son nosotros podemos operar matemáticamente con

ellos para, por ejemplo, estudiar si su dirección es similar o no.

Esto lo podemos hacer a través de una operación matemática denominada

producto escalar o en inglés Dot Product, que viene

en honor de su creador, que en este caso apoya este producto.

Escalar nos dará un valor numérico que será mayor en relación

a cuanto coincidan las direcciones de los vectores.

Es decir, si las redes que han generado

estos vectores hicieran representar que dos palabras son compatibles,

pues tendrán que transformar a estas palabras

en vectores cuya direcciones se aproximen en este espacio

donde llave y cerradura encajen.

Y creo que estamos en un

punto en el que ya podemos empezar a llamar a cada cosa por su nombre.

Y es que en el paper original a lo que aquí estamos llamando cerradura,

se le conoce como vector query, y a lo que estamos llamando llave

se le conoce como vector aquí, que en este caso tiene más sentido.

Estas dos nomenclaturas creo que son interesantes

porque además nos

acerca a la filosofía de trabajo que encontramos, por ejemplo,

en la recuperación de información dentro de bases de datos,

donde términos como query o key, pues también son utilizados.

Esta misma idea es la que estamos intentando implementar aquí,

pero en este caso utilizando redes neuronales.

Como hemos visto,

cada palabra obtendrá

con estas redes neuronales su vector query y su vector aquí y ahora.

Por ejemplo, para esta palabra podemos tomar su vector query

y calcular cuál es la compatibilidad que tiene con el resto de palabras.

Como lo haremos?

Pues ya lo sabes, calculando el producto escalar

entre el vector Query de esta palabra y los vectores Key del resto.

Como hemos visto, este producto escalar

nos devolverá un valor numérico que entre más alto

sea, nos estará indicando que mayor es la compatibilidad.

Así podemos ver cuáles son las palabras más compatibles

con esta de aquí, pero realmente son algo más que porcentajes.

Y es que esto que acabamos de computar

aquí es lo que se conoce como el vector de atención.

Si, atención, porque si te fijas y coloreamos los valores numéricos

que hemos calculado para verlos mejor, podemos ver qué importancia

le da a nuestro modelo de inteligencia artificial al resto de palabras.

Cuando está leyendo esta de aquí nos está mostrando

qué palabras considera relevantes para dar contexto a su palabra.

O dicho de otra forma, a qué parte de la frase está prestando atención?

De hecho, si comparamos estos vectores para cada palabra de nuestra frase,

finalmente acabaremos con lo que se conoce como una matriz de atención.

Algo como esto. Donde podremos ver

la importancia que cada palabra está asignando al resto de la frase.

Estos son matrices muy interesantes de visualizar,

ya que lo que nos van a mostrar

son a qué parte de la información dada como input.

La inteligencia artificial

está prestando atención para tomar sus decisiones.

En este ejemplo típico de traducción

vemos que cuando

calculamos la atención entre la frase en inglés y en francés,

la inteligencia artificial es capaz de encontrar la relación

entre las palabras en distintos idiomas, aún cuando el orden

no siempre se preserva,

como en este caso de aquí, donde el orden de las palabras

zona económica europea varía según el idioma.

Pues ahora la pregunta importante que hay que hacerse es para qué?

Para qué nos interesa calcular este vector o matriz de atención

que nos aporta saber a dónde focaliza su atención?

La red neuronal en cada momento es esto útil?

Atiende ahora, al igual que utilizamos en un principio,

vamos a usar una red neuronal para que procese a

cada una de nuestras palabras.

No la he mencionado hasta ahora,

pero su papel es equivalente al procesamiento que hace también

la red principal de las redes recurrentes transformar cada palabra

al vector de salida necesario para cumplir la tarea que estamos buscando.

Este vector de salida

es el que encontramos en el paper denominado como vector valor.

Si antes con las redes neuronales recurrentes teníamos el problema de

que por usar la recurrencia perdíamos la relación

que pudiera existir entre palabras muy distanciadas.

Ahora hemos creado un mecanismo donde podemos relacionarlas

sin importar qué tan lejos estén.

Y aquí es donde viene lo interesante, porque aquí es donde las atenciones

calculadas previamente van a jugar su principal papel.

Y es que en esta frase, como hemos visto antes,

la palabra Manolin podría tener una relación interesante

con estas dos palabras taqui.

Y es por eso que la atención que presta a nuestro sistema

cuando el input es la palabra

pangolín, va a ser muy alta con estas dos palabras de aquí.

Así, el uso que le daremos a cada una de las atenciones calculadas

será el de computar una suma ponderada donde utilizaremos la atención

que prestamos a cada palabra

como factor de mezcla de cada uno de los vectores de valor.

Es decir, para la palabra pangolín dada como input su vector de atención

nos servirá como una receta que nos va a ir indicando

en qué porcentaje tenemos que ir mezclando el resto de valores.

¿Lo veis? Así este output de alguna manera

tendrá el contexto necesario

del resto de palabras que conforman a la frase, dando mayor importancia

a aquellas a las que le haya prestado atención.

Esto, repetido para cada una de las palabras de nuestro input,

no dará como resultado unos vectores de palabras

cuya transformación ahora recoge el contexto del resto de la frase.

Como ves, con este mecanismo

hemos encontrado una forma de poder

contextualizar a cada una de las palabras de nuestra frase

con cualquier otra palabra que se pueda encontrar a cualquier distancia.

Hemos resuelto el principal problema al que se enfrentaban

las redes neuronales recurrentes la falta de memoria.

Y es que estos mecanismos de atención han sido realmente de ayuda

para solucionar este problema que estaba presente

en las redes neuronales recurrentes. La falta de memoria a largo plazo.

Y ha sido gracias a la combinación

de estos mecanismo de atención con este tipo de redes

con las que hemos conseguido

mejorarlas, potenciarlas

y aplicarlas a numerosas tareas de procesamiento del lenguaje natural.

Pero lo interesante ocurre en 2017, cuando uno de los papers

más influyentes de la época apareció con una idea muy atractiva.

Pues que esta idea de querer

potenciar a las redes neuronales recurrentes con mecanismo de atención

para que funcionen mejor está muy bien,

pero que en realidad las redes recurrentes en todo esto sobran.

Que de hecho en aquel paper proponían un nuevo tipo de red neuronal,

una arquitectura diferente a la que vamos a llamar Transformers

y donde nos van a demostrar que esto de aplicar mecanismos de atención

es suficiente para poder conseguir rendimientos superiores

a los de las PORTODOS utilizadas redes neuronales recurrentes.

Un paper titulado Attention Is All You Need

lo único que necesitas es atención.

Ese paper fue el que introdujo el concepto de Transformers,

un nuevo tipo de red neuronal

que venía a sumarse al resto de arquitecturas

que ya conocíamos en el campo del deep learning redes convencionales,

redes recurrentes y ahora Transformers o una arquitectura que poco a poco

vamos conociendo, pero que fundamentalmente se basa

en los principios de lo que hemos visto hoy,

en los mecanismos de atención con lo que hemos visto

hoy, sin haber hablado ningún caso de Transformers.

Ya conocéis cuál es la idea clave que hace funcionar a este sistema

y de dónde surge

parte de la ventaja que logran frente a las arquitecturas recurrentes.

Pero eso no quita que todavía queden cosas importantes por explicar.

Antes, en este punto decía

que el pangolín se presentaba

como Hola, soy la segunda palabra de esta frase,

pero cómo puede saber el Pango Linke es la segunda palabra de la frase

si realmente ya no estamos hablando de secuencias que mediante recurrencia

están conectadas, cómo puedes saber cuál es su posición en la frase?

Y también que otros mecanismos y técnicas se aplican

dentro del transformer para que todo funcione correctamente?

Y por último, pero no menos importante,

cómo hemos conseguido adaptar a esta arquitectura

para que nos sirva tanto

para el entrenamiento

de un modelo tan impresionante como sería GPT3 como para poder también

utilizarlo en problemas de visión por

ordenador con los Visual Transformers?

Cómo funciona todo esto?

Pues todas las respuestas

a estas preguntas la vais a encontrar en un próximo.

Vídeo un vídeo que servirá de segunda parte a esta introducción

al funcionamiento de los Transformers y que dará continuación a la serie de

NLP de procesamiento de lenguaje natural

que ya introduje con estos vídeos de aquí.

Si no habéis visto esta serie, pues también os la recomiendo.

Voy a dejar en la descripción enlaces para que podáis seguirla entera y así

tengáis una visión más completa de cómo funciona este fascinante mundo.

Por último, simplemente deciros que si este vídeo os ha servido,

si ha sido útil para vosotros, si habéis aprendido,

si queréis apoyar este contenido

porque lo veis valioso, pues podéis apoyarlo a través de Patreon.

Voy a explicar un poco qué es esta plataforma para el que no la conozca,

pero es una de las fuentes que tiene este canal para financiarse.

Podéis hacer una pequeña aportación mensual,

pues lo que sería una invitación a una cerveza o una comida

o simplemente el apoyo que queráis aportar,

pues será una forma de indicar

que mi trabajo para vosotros

es de valor y es una forma de recompensar el esfuerzo de traeros

todo este contenido divulgativo científico aquí a YouTube

y que esto sirva para apoyar

este contenido en abierto para que lo pueda disfrutar todo el mundo

al que se lo pueda permitir y el que no podía

dejar el enlace abajo en la caja de suscripción

para que le podáis echar un vistazo y si os interesa, podéis apoyar.

Y por último, último último, recordaros que el patrocinador

de este vídeo es el podcast de Cuidado con las macros ocultas,

un podcast de 4 80 donde se va a hablar de tecnología

y que creo que os va a interesar sobre todo el primer programa

donde Andrés Torrubia y un servidor estamos hoy conversando

sobre inteligencia artificial,

así que si queréis escucharlo

puede dejar también el

enlace abajo en la cajita descripción para que le echéis un vistazo.

Mientras tanto, nos vemos con más inteligencia artificial

la próxima semana.

Cuidado con las macros ocultas.

Un podcast de 4 80.