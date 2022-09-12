En este proyecto, se propone estudiar cómo se vinculan la transmisión de enfermedades parasitarias y el comportamiento y uso del espacio de los animales, utilizando a _Fasciola hepatica_ en ovejas como sistema de estudio.

El ciclo de vida de este parásito involucra un hospedador intermediario (caracoles limneidos), y formas de vida libre del parásito en cuerpos de agua (miracidios y cercarias) y en la vegetación (metacercarias). Los hospedadores definitivos son mamíferos que se infectan al ingerir vegetación o agua contaminada.

**PATTERN 
Las enfermedades parasitarias como la fasciolasis se caracterizan por una distribución agregada de los parásitos donde muchos hospedadores presentan una carga parasitaria baja mientras que unos pocos presentan una carga alta [(Shaw and Dobson 1995)](https://www.zotero.org/google-docs/?cCpwrC). Esta variabilidad resulta de diferencias en el grado de exposición de cada animal a las fuentes de infección y de variaciones en la susceptibilidad a la infección, que dependen de factores como la edad, el sexo, la condición física, la genética o el comportamiento [(Wilson et al. 2002)](https://www.zotero.org/google-docs/?L2GJMc). A su vez, pueden existir variaciones estacionales y espaciales en la abundancia de los parásitos, de manera que el comportamiento y el uso de hábitats tenga un fuerte impacto en la probabilidad de infección y la carga parasitaria de los individuos.**

**Tanto los pobladores como las autoridades de APN, INTA y SENASA reconocen la alta prevalencia de _F. hepatica_ en las ovejas, con reportes relativamente frecuentes de mortalidad por intensas infestaciones con _F. hepatica_.**

**Al tener como input mapas detallados del paisaje, estos modelos resultan atractivos como herramienta para predecir los efectos de una estrategia de manejo determinada, ya que el control de _F. hepatica_ puede depender en gran medida de las características y el estado del paisaje que se busca manejar.** Fasciola dynamics should depend on characteristics and current state of the landscape. 


La hipótesis general de este proyecto es que existe una vinculación estrecha entre el comportamiento espacial de ovejas y la transmisión de _F. hepatica_, donde ambos procesos están modulados por la heterogeneidad ambiental y las decisiones a nivel de individuo en torno al uso del espacio. Siguiendo esta hipótesis, se desarrollarán modelos basados en agentes para explorar la relación entre comportamiento y dinámica de enfermedades. Se van a recolectar datos de GPS, acelerómetros y magnetómetros en ovejas para parametrizar estos modelos y evaluar su capacidad predictiva en base al monitoreo de la carga de _F. hepatica_ en estos individuos.


**ENVIRONMENT 
El estudio se realizará en un área rural en el valle del río Manso Inferior (41° 35’ S; 71° 26’ O), SO de la provincia de Río Negro. El paisaje es cordillerano, con una temperatura media de 15,2 °C en enero, 3,8 °C en julio y anual de 9,3 °C y precipitación media anual de 1255 mm. La vegetación es subantártica y alto-andina, con zonas de bosque, de arbustos y de pastizales de altura, además de zonas deforestadas (pastizales) utilizadas para la ganadería [(Cabrera 1971)](https://www.zotero.org/google-docs/?yh9LqO). Existen múltiples cuerpos de agua: ríos, arroyos, lagunas y mallines. En el área se permite la cría de ganado de forma controlada por la Administración de Parques Nacionales (APN) [(Martín and Chehébar 2001)](https://www.zotero.org/google-docs/?opI1ky) y existen siete asentamientos rurales ganaderos.**

**El paisaje será representado con una grilla de <30 m de resolución en base a los mapas de variables ambientales que se están compilando como parte del PICT 2017 en el sitio de estudio.**

**. Toda esta información se integrará con la obtenida en un proyecto PICT (2017, ver factibilidad) sobre el mapeo y caracterización de los distintos tipos de hábitats de la zona, variables climáticas y distribución y abundancia de _F. hepatica_ en cada ambiente que se utilizará en **III**.**


**AGENTS
El ganado ovino pastorea libremente durante el día y a la noche generalmente se los encierra en corrales.**

**Los animales simulados podrán adoptar distintos comportamientos básicos de forrajeo, descanso, desplazamiento dirigido entre distintos “parches” del ambiente y exploración. Los individuos (agentes) pasarán un tiempo variable en cada comportamiento que será “muestreado” de distribuciones de tiempos de actividades. Una vez que el tiempo dedicado a una actividad llega a su fin, funciones de probabilidades de transición determinarán qué tipo de comportamiento se va a realizar. Cada comportamiento estará asociado a distintos tiempos de residencia en celdas del paisaje y a distintas probabilidades de elegir celdas vecinas para desplazarse. Tanto los tiempos de residencia como las probabilidades de elegir celdas como destino serán función del tipo de comportamiento, de la condición del individuo (saciedad, porcentaje de grasa corporal, etc.) y de las características ambientales (altura, pendiente, exposición, tipo de hábitat, etc.) de estas celdas. Ver Morales et al. (2005) para más detalles sobre este tipo de modelos.**



**STOCHASTICITY
El mismo consistirá en un modelo estocástico basado en agentes [(Grimm and Railsback 2005)](https://www.zotero.org/google-docs/?5s8Z0t), lo que permitirá incorporar variaciones de comportamiento y uso del espacio a nivel de individuo e integrar la heterogeneidad del paisaje y el clima. De esta forma, se tratará de manera explícita la conexión entre distintos tipos de comportamiento y de uso del espacio. El modelo basado en agentes funcionará en tiempo continuo y espacio discreto, siguiendo un esquema similar al modelo de Morales et al. (2005)**



**INPUT DATA
Se va a monitorear el movimiento y la carga parasitaria de 50 ovejas durante tres temporadas (períodos de seis meses, primavera-verano). Se elegirán 5 productores cuyos campos provean una muestra representativa de los hábitats del área. De cada campo, se seleccionarán 5 borregas y 5 ovejas adultas. Dos meses antes del inicio del seguimiento, se aplicará un tratamiento antiparasitario intensivo a los 50 animales seleccionados y se realizará un análisis de la carga parasitaria antes del comienzo del seguimiento. Luego, este análisis se repetirá con una frecuencia mensual durante toda la temporada.
Para iniciar el seguimiento, primero se corroborará que los animales seleccionados no presenten parásitos y luego serán equipados con collares (con los que el grupo ya ha trabajado anteriormente en ovinos [(Virgilio et al. 2018)](https://www.zotero.org/google-docs/?IYZgn1)) que constan de GPS CatLog-B (Perthold Engineering, [www.perthold.de](http://www.perthold.de/)) combinados con acelerómetros y magnetómetros (DailyDiary, [http://www.wildbytetechnologies.com/](http://www.wildbytetechnologies.com/)) y con pequeños paneles solares que fueron diseñados durante el PICT 2015-0815 (IR JM Morales). Durante el seguimiento, los equipos GPS registrarán las posiciones cada 5 minutos y los acelerómetros y magnetómetros registrarán en tres ejes aceleración y variación en el campo magnético, respectivamente, a alta frecuencia (40 y 20 Hz) de manera continua.**

**A partir de los datos de GPS y magnetómetros se reconstruirá la trayectoria de movimiento de los animales y se cuantificará el patrón de uso de hábitats. . Toda esta información se integrará con la obtenida en un proyecto PICT (2017, ver factibilidad) sobre el mapeo y caracterización de los distintos tipos de hábitats de la zona, variables climáticas y distribución y abundancia de _F. hepatica_ en cada ambiente que se utilizará en III.**

**Al tener como input mapas detallados del paisaje, estos modelos resultan atractivos como herramienta para predecir los efectos de una estrategia de manejo determinada, ya que el control de _F. hepatica_ puede depender en gran medida de las características y el estado del paisaje que se busca manejar.
**

**SUBMODELS
Al modelo base desarrollado en I, se le añadirá un módulo que permita evaluar el efecto de distintas prácticas de manejo y un módulo de transmisión de enfermedades. El primero permitirá evaluar el impacto de prácticas de manejo tales como suplementar la alimentación o aplicar restricciones en el área de pastoreo. El paisaje modelado ahora incluirá también la presencia de _F. hepatica_ en distintos ambientes y en distintos momentos del año (información siendo compilada por PICT 2017) y los animales tendrán la posibilidad de infectarse cuando pasen tiempo en celdas del paisaje donde estén presentes las formas infectivas de _F. hepatica_. Un submódulo del modelo seguirá el desarrollo de _F. hepatica_ dentro de los animales infectados y la deposición de huevos con las heces de los animales. De esta forma, se tratará de manera explícita la conexión entre distintos tipos de comportamiento, de uso del espacio y el riesgo de infección y de transmisión de _F. hepatica_, así como el efecto de distintas prácticas de manejo sobre estos factores.**

