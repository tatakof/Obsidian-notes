
Para qué queremos estudiar movimiento animal? para que nos va a servir? qué vamos a aprender? Una de las cosas a  entender son los procesos ecologicos a nivel poblacional, tratar de entender lo que pasa en una población a traves de lo que le pasa a los individuos, la cuestión de escalar nivel individuo a poblacion. 

Los modelos clasicos de dinámica poblacional suponen poblaciones bien mezcladas, los procesos dependen de cuestiones de campos medios. Pero en el mundo real hay heterogeneidad que afecta los procesos y depende de como se mueven los individuos. 

La importancia del movimiento animal para entender procesos ecológicos tiene bastante historia, todo el mundo lo consideró pero era mas dificil entender cómo estudiar esa dinamica de movimiento y qué implicaba para la dinámica de sistemas no bien mezclados. Aca es donde parece todar la parte de toma de datos avanzada, como los acelerómetros, magnetómetros, gps, buenos mapas que representen la heterogeneidad del ambiente, etc. Esto llevó a representar en su momento el movimiento de manera muy sencilla usando modelos preexistentes de la fisica y en sistemas homogeneos (e.g. usando como modelo cómo se mueve un gas). 

En terminos de desafios de modelado está por un lado el hecho de que ahora tenemos toneladas de datos. Esto hace que alguno de los tipos de análisis que se hacían antes sean poco prácticos. Los métodos bayesianos acá tienen problemas por la gran cantidad de datos. Hay un desafio por este lado de cómo procesar muchos datos. 

Un desafio más conceptual es cómo realmente escalar desde las decisiones de movimiento minuto a minuto a cómo realmente usan el espacio los animales a escalas más grandes. Ahí aparecen procesos de comportamiento que son difíciles de modelar y difícil de tener datos de lo que está ocurriendo. Esto es, por ej, porque aparecen cosas como la importancia de la memoria. En todo modelo de movimiento sin memoria, los animales terminan desparramándose por todo el espacio y esto no es algo real. 

Lo clásico es pensar un paisaje con 2 ambientes, uno donde los animales se mueven mas lento y permanecen más tiempo, y otro donde los animales se mueven más rápido y no tienden a permanecer mucho tiempo en el lugar. Hay un modelo que se llama area restricted search, que implica por un lado distancias de movimiento cortas y ángulos de giro grandes, y por el otro, distancias de movimiento más largos y ángulos de giro cortos. Si ajustás este modelo de forma bayesiana con un MCMC, el animal termina haciendo una difusión para cualquier lado. Pero lo que ocurre en realidad es que los animales se quedan en un home range que es mas o menos estacionario, porque prefieren estar en lugares donde estuvieron antes, que es donde entra la memoria y los puntos de atraccion. esto ultimo es dificil de modelar porque te falta la parte anterior a la trayectoria que vos tenes. 
Puede tmb haber interacciones con otros individuos que no tenes en cuenta. 

Si tenes animales gregarios, las decisiones de movimiento de un individuo depende de lo que hacen los otros. 

El caso de hacer simulaciones es un poco diferente, no es tanto ajustar modelos a datos sino que evaluar distintos escenarios y conectarlo con datos de verdad. 

De lo que mas se usa ahora para analizar datos de movimiento de gps son los HMM, este es como uno de los caballitos de batalla de hoy en día. 
El otro es el que se llama step selection o integrated step selection. Este modelo permite estimar qué características del ambiente son las que usa el animal, al analizar los puntos a los que decide ir el animal. Parte de lo que se está haciendo ahora es integrar HMM con Step selection. 

Otra dicotomía importante es entre modelos de tempo continuo y de tiempo discreto. Los ultimos 2 modelos (HMM y Step selection) suelen ser en tiempo discreto, aunque hay versiones en continuo. La ventaja del tiempo continuo es que no dependés de la escala arbitraria del gps y es más facil tratar con datos perdidos. Son también más fáciles de armar modelos tipo espacio estado donde podes incluir el error en el gps. La contra de los modelos de tiempo continuo es que las formulaciones matemáticas no son muy transparentes. Muchos usuarios no le encuentran mucha interpretacion a los parametros que encontras o no quieren usar ecuaciones diferenciales. 

Una alternativa que no está del todo desarrollada, no es mainstream y que hay pocas herramientas, son los modelos a tiempo continuo y espacio discreto, que eso se adapta bastante a la simulación que yo voy a hacer con los abms. 
Los pixeles pueden ser cuadrados o hexagonales, vos modelás el movimiento a partir de tiempos de residencia en cada pixel, con cierta probabilidad que depende de muchas cosas. Entonces acá podés poner la selección de hábitats con lo del step selection. Es también fácil incorporar barreras al movimiento porque a ese pixel no puede ir y punto. El tiempo que se queda en cada pixel también lo podes hacer que dependa de covariables. Tal vez va a haber persistencia en la dirección de movimiento. Por ahora estos modelos no tienen cambio de comportamiento, pero fácilmente se podria incorporar ese cambio de tipo de comportamiento. Para que sea más sencillo, los cambios de comportamiento deben ser uno por pixel, que seria como un hidden semi markov model donde la posibilidad de cambiar de comportamiento ocurre despues de terminar un tiempo de residencia. 

Cualquiera de estos 3 modelos (HMM, step selection y los modelos a tiempo continuo y espacio discreto) los podes hacer como un ABM. 

Hay una distincion entre modelos eulerianos y lagrangianos. Los primeros implican modelar densidades y los 2dos modelan individuos. Un modelo euleriano seria uno de difusión, el 2do seria una trayectoria de particulas haciendo un random walk. Para algunos casos se pueden conectar de forma matematica los modelos eulerianos y lagrangianos pero solo en casos sencillos. 
Los 3 modelos (HMM, step selection y los modelos a tiempo continuo y espacio discreto) son lagrangianos. 

Parte de lo que no está resuelto es que yo por ej ajusto un hmm y simulo un individuo y miro las trayectorias, éstas no son similares. 


Los ABMs tienen varias utilidades, tradicionalmente no se usan para ajustar modelos a datos, se usan mas para explorar escenarios y consecuencias de reglas, la cosa es que hoy en dia se puede intentar hace runa conexion explicita entre ABMs y datos. Ahí se empieza a desdibujar un poco la diferencia entre ajustar modelos a datos y hacer simulaciones. 
Lo que hacia la gente es a partir del modelo de simulación con ciertos parámetros, ver cómo estimar ciertos parametros con datos y para los parámetros donde no hay datos, no estimarlos y despues ver con un análisis de sensibilidad si ese parámetro era importante.  Después aparece el pattern oriented modeling, y ahora el aproximate bayesian computation es una version mas sofisticada y rigurosa que el pom. 


Armar el modelo pensando que se va a conectar con datos. ir poniendo valores de cosas sin importar mucho la conexion con los datos pero que se puedan hacer experimentos, ej en sistema con tales condiciones espero que pase tal cosa. 


Los ABMs pueden tener un nivel de detalle excesivo. 





Pensar en que es relevante par alo nuestro a la hora de hacer el ODD, ser mas pragmatico, no buscar representar la realidad total. 

Que es lo conveniente responder del ODD en este momento. que queres representar y que conviene representar ahora del ODD. Pensar en varias iteraciones del modelo en terminos de complejidad. Una vez que tenes el modelo simple, ver que falta incorporar, si es memoria, si es sensing de otros individuos, etc. 

Si surje una duda, ir por lo mas simple. 


son pocas las cosas que son urgentes. 

tampoco tengo que mandarle algo completo del protocolo, que sea algo mas interactivo, no esperar a tener algo perfecto. 




## Preguntas

- Un poco de historia de movimiento animal



- Progreso de modelos de animal movement



- Open problems en el modelado de animal movement




- Qué patrones tenemos que reproducir? algún otro proceso emergente?

si la idea de que este modelo represente el riesgo de transmision, necesitamos que el modelo represente bien el uso del espacio de los distintos ambientes donde pueden contagiarse y donde pueden ir dejando huevos. 




- Contraints, qué patrones NO tenemos que reproducir? 






- Theoretical Issues, problemas teóricos a resolver en movimiento animal, 




- Relación entre este modelo y modelos previos? modelado de heterogeneidad?




- Adaptive behaviour de las ovejas? 




- Decisiones que toman las ovejas? solo qué comportamiento hacer?




- Agent's objectives? maximizar fitness?




- Learning? cambian comportamiento en base a experiencia?




- Ovejas preciden condiciones futuras? ambientales o internas.




- Sensing del ambiente por parte de las ovejas?




- Modelamos interacción entre ovejas o solo con el ambiente?





- Observation: location, time of residence in specific patches, distribution of behaviors. 









- Scheduling? random model steps for each agent?





- Submodels. desarrollo de fasciola dentro del individuo, dinámica de fasciola, dinámica de vegetación?






