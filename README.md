![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/6c92243a-e90b-48e2-abf4-77d61eca0d09)


# PROYECTO_DATA_ANALYTICS


Link Dashboard Tableu  https://public.tableau.com/views/PROYECTO_2_16967996370940/ACCIDENTESAEREOS?:language=es-ES&:display_count=n&:origin=viz_share_link

TRANSFORMACIÓN DE LOS DATOS.

La base de datos contiene información sobre 5008 accidentes aéreos que ocurrieron entre 1908 y 2023, renombro todas las columnas y creo un nuevo data frame para mayor entendimiento.

fecha: La fecha del accidente en formato de texto.
HORA declarada: La hora reportada del accidente
Ruta: El origen y destino del vuelo cuando aplica
OperadOR: Si el vuelo era militar, comercial, privado, etc.
flight_no: Número de vuelo cuando aplica
route: Otra columna que parece indicar la ruta del vuelo
ac_type: Tipo de aeronave (avión, dirigible, etc)
registration: Matrícula o registro de la aeronave
cn_ln: Número de serie de la aeronave
all_aboard: Cantidad total de personas a bordo
PASAJEROS A BORDO: Cantidad de pasajeros
crew_aboard: Cantidad de tripulación
cantidad de fallecidos: Cantidad total de fallecidos
passenger_fatalities: Cantidad de pasajeros fallecidos
crew_fatalities: Cantidad de tripulación fallecida
ground: Cantidad de fallecidos en tierra
summary: Resumen del accidente

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/bc06e116-1abf-4fc3-90f2-310e70f0fac2)


![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/34b3d5e5-598e-447c-8742-60549b733e71)

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/99e1f4f1-5867-4fa9-8472-d765f1f8a690)

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/88291c66-f6c0-4210-947d-d2342309638b)

Ahora elimino columnas que no voy a usar para el análisis dado que no proporcionan información relevante.
df_1 = df_1.drop(["numero_vuelo","matricula", "numero_serie", "Unnamed: 0", "ID", "origen_destino", "ruta_vuelo",'resumen_accidente','fallecidos_en_tierra'], axis=1)

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/3c53b4dc-9f10-4a15-af49-42f0ec359e13)

Agrupamos la columna operador por Militar y no militar, para mejor manejo de los datos.

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/e7d234a8-9a18-494c-be86-6f34e8586543)


IDENTIFICACIÓN DE RELACIONES ENTRE VARIABLES.


Ahora para ver la relación entre las variables podemos hacer una matriz de correlación, dado que tenemos columnas que tienen diferentes tipos de datos entre sí, haremos sub-data set para poder hacer la matriz de correlación, además crearemos un sub-data set que contenga las columnas categóricas códificadas para hacer una matriz de correlación con el mayor número de columnas posibles, así veremos las relaciones entre las columnas.

El primer subset lo haremos con las variables númericas, el cual será, con las columnas que contienen datos de las personas y el año y el mes del accidente.

El segundo subset lo haremos codificando las variables categóricas, operador, tipo de aeronave, ruta, y también usaremos las anteriores variables númericas-

Por último pasaremos a identificar outliers con diferentes tipos de gráficos para determinadas columnas, las analizaremos cada una.

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/bb6e4f03-826d-41d7-9e14-9a06a7120fd2)

La correlación entre el año del accidente y el mes del accidente es muy débil (-0.033764). Esto significa que no hay una relación significativa entre estas dos variables.

La correlación entre el número total de personas a bordo y el número total de fallecidos es fuerte (0.739646). Esto significa que existe una relación positiva entre estas dos variables, lo que indica que cuanto mayor es el número de personas a bordo, mayor es el número de fallecidos en un accidente aéreo.

La correlación entre el número de pasajeros a bordo y el número de fallecidos de pasajeros también es fuerte (0.738965). Esto significa que existe una relación positiva entre estas dos variables, lo que indica que cuanto mayor es el número de pasajeros a bordo, mayor es el número de fallecidos de pasajeros en un accidente aéreo.

La correlación entre el número de tripulantes a bordo y el número de fallecidos de tripulantes también es fuerte (0.720937). Esto significa que existe una relación positiva entre estas dos variables, lo que indica que cuanto mayor es el número de tripulantes a bordo, mayor es el número de fallecidos de tripulantes en un accidente aéreo.


IDENTIFICACIÓN DE OUTLIERS.

Para identificar outliers uso el z-score,  utiliza un umbral de ± 3. Los puntos de datos con un z-score mayor que 3 o menor que -3 se consideran outliers.

Por ejemplo, si la media de una distribución es 10 y la desviación estándar es 5, un z-score de 3 significa que el punto de datos está 3 desviaciones estándar por encima de la media.

El z-score es una buena herramienta para identificar outliers porque:

Es una medida estandarizada que se utiliza en muchos campos.
Es fácil de calcular y de interpretar.

0      -0.608393
1      -0.608393
2      -0.494109
3      -0.608393
4      -0.236969
          ...   
5003   -0.494109
5004   -0.322682
5005   -0.294111
5006    0.791591
5007    0.163027
Name: total_fallecidos, Length: 5008, dtype: float64

Para el z_score uso la columna total fallecidos, por cuestiones de etica, pues lo importante es el total de personas que han muerto sin importar si son de la tripulación o pasajeros, hacer la diferencia en este caso no arroja mayor información.

En este caso, el z-score de cada punto de datos representa el número de desviaciones estándar que se encuentra por debajo de la media. Por ejemplo, el z-score de -0.608393 en la fila 0 indica que el valor de total_fallecidos en esa fila es 0.608393 desviaciones estándar por debajo de la media.

Como se puede apreciar, la mayoría de los z-scores son negativos, lo que indica que la mayoría de los valores de total_fallecidos son inferiores a la media. Los únicos valores positivos son los de las filas 5006 y 5007, que indican que los valores de total_fallecidos en esas filas son superiores a la media.

En este caso, hay dos outliers en el data frame, uno en la fila 5006 y otro en la fila 5007. Estos outliers podrían representar accidentes aéreos muy graves con un número inusualmente alto de víctimas. Al observar el Data Frame df_1 podemos ver que esto se debe a que había un gran número de personas abordo.



ANÁLISIS DE DATOS.



Gráfico de líneas: Este gráfico es el más adecuado para ver la tendencia a largo plazo. Podemos utilizar este gráfico para ver si ha habido un cambio en el número de fallecidos a lo largo de los años, así podremos identificar Outliers.

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/85f5c3c0-ee8f-49e3-a2c7-8c44c244c4e5)

 El gráfico muestra que el número de accidentes aéreos ha disminuido en general a lo largo de los años, con un pico en la década de 1970 .

El gráfico también muestra que el número de accidentes aéreos ha sido más variable en los últimos años, con un aumento significativo en el número de accidentes en 2021. Este aumento puede deberse a una serie de factores, como la pandemia de COVID-19, que provocó una reducción en el número de vuelos, y el conflicto en Ucrania, que ha afectado a la aviación civil en Europa, también el envejecimiento de las flotas áreas puede aumentar los accidentes aéreos.

En general, el gráfico muestra que la seguridad de la aviación ha mejorado significativamente en los últimos años. Sin embargo, es importante seguir tomando medidas para reducir aún más el número de accidentes aéreos.

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/51d776c2-fdc6-47b9-b7ce-69f8372468ee)

El gráfico muestra el total de fallecidos por operador. El segmento azul del gráfico representa el porcentaje de fallecidos por operadores  militares, mientras que el segmento naranja representa el porcentaje de fallecidos por operadores  no militares.

El gráfico muestra que el 80,8% de los fallecidos estaban en un operador  no militares, mientras que el 19,2% estban en operadores  militares. 

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/35df4e2b-2f20-4c44-9b14-a23340ee2de6)

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/6b2a4d7d-65e8-431a-918f-c71749d370bb)

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/5d65b151-d089-49b5-bf80-d6d57da36b79)

El gráfico muestra que el porcentaje de pasajeros fallecidos ha disminuido a lo largo del tiempo. En la decada de  1920, el porcentaje de pasajeros fallecidos era del 20%. En 2020, ese número se ha reducido a menos del 5%.

Esta disminución se debe a una serie de factores, entre los que se incluyen:

Mejoras en la seguridad de las aeronaves.
Mejoras en las prácticas de vuelo.
Mejoras en la respuesta a los accidentes.



MÉTRICAS

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/ef19043d-e92e-417d-9bd4-f54626465db9)

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/e59adf4f-9c14-4501-9a57-ab380b4a3635)

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/53925775-49f4-4d8a-9391-56d9ba9e8037)

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/5f0cf134-4f75-4d05-a265-0190e013b671)
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>tipo_aeronave</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>other</td>
      <td>1166</td>
    </tr>
    <tr>
      <th>1</th>
      <td>McDonnell Douglas</td>
      <td>1124</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Boeing</td>
      <td>411</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Lockheed Martin</td>
      <td>352</td>
    </tr>
    <tr>
      <th>4</th>
      <td>De Havilland</td>
      <td>293</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Antonov</td>
      <td>285</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Ilyushin</td>
      <td>140</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Fokker</td>
      <td>138</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Tupolev</td>
      <td>105</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Vickers</td>
      <td>93</td>
    </tr>
  </tbody>
</table>
</div>






KPIS

KPIS: Un KPI (Key Performance Indicator) es una medida cuantificable que muestra cómo efectivamente se están cumpliendo los objetivos de una empresa. Los KPIs son utilizados para medir el rendimiento de la empresa en relación a sus objetivos estratégicos más importantes.



















