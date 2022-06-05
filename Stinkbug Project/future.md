El trabajo a desarrollar incluye:

  
- Desarrollo de modelos:  
  
Los modelos previos tienen una estructura matemática basada en datos de cuentas con distribuciones de probabilidad Binomial y Poisson. Ésta estructura supone que la cantidad de paños semanales es constante y dificulta el manejo de semanas en las cuales no se tomaron datos.  
Los nuevos modelos tendrán una estructura matemática basada en densidades con distribuciones de probabilidad Normales. Esto permitirá distintos tamaños muestrales en distintas semanas y simplifica el manejo de semanas con datos faltantes.  
  
Los nuevos modelos van a ser ajustados con el software Stan en vez de JAGS. Stan es un software más avanzado que JAGS. Permite un mejor ajuste de los modelos y mejor diagnóstico de cuándo y cómo los modelos fallan.  
  
- Evaluación de la capacidad predictiva de los modelos usando LFO-CV:  
   
Leave Future Out Cross Validation (LFO-CV) es una medida del poder predictivo de un modelo que contempla la estructura temporal de los datos y nos va a permitir comparar el desempeño de distintos modelos (modelos que incluyen diferentes variables predictoras y variaciones en estructuras lineales y no-lineales). Esto implica una mejora sustancial respecto de las evaluaciones hechas hasta ahora que no contemplan la estructura temporal de los datos.  
  
A su vez, LFO-CV permite evaluar el desempeño de las predicciones de un modelo a lo largo de toda la serie temporal. Es decir en todas las etapas del ciclo de cultivo. Además, podremos evaluar la capacidad predictiva para la siguiente semana como función de la longitud de la serie temporal de los datos.  
  
Esto, sumado al análisis de incertidumbre en función del tamaño muestral (el cual permite determinar la cantidad de paños mínimos semanales que son necesarios para que el modelo haga buenas predicciones), va a permitir tener una buena noción de bajo qué circunstancias los modelos hacen buenas predicciones. Es decir qué cantidad de paños por semana y cantidad de semanas con datos son necesarias para tener predicciones confiables.  
  
  
- Bayesian Model Averaging:  
  
Distintos modelos predictivos de dinámica chinches capturan distintas características del funcionamiento del sistema natural, siendo prácticamente imposible tener un modelo que capture perfectamente todas las características del funcionamiento del sistema. Por ejemplo, algunos modelos pueden capturar mejor el proceso de explosión poblacional durante la fructificación, mientras que otros pueden capturar mejor la implosión poblacional durante R8. Bayesian Model Averaging es una metodología que permite asignar distintos "pesos" a los distintos modelos en base a cuán  
buenas sean sus predicciones en distintos escenarios, y luego hacer un promedio ponderado para obtener una predicción que contemple los mejores aspectos de cada uno de los modelos.  
  
- Desarrollo de un entorno computacional reproducible