![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/6c92243a-e90b-48e2-abf4-77d61eca0d09)


# PROYECTO_DATA_ANALYTICS


Link Dashboard Tableu  https://public.tableau.com/views/PROYECTO_2_16967996370940/ACCIDENTESAEREOS?:language=es-ES&:display_count=n&:origin=viz_share_link

TRANSFORMACIÓN DE LOS DATOS.

La base de datos contiene información sobre 5008 accidentes aéreos que ocurrieron entre 1908 y 2023, renombro todas las columnas y creo un nuevo data frame para mayor entendimiento.



![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/bc06e116-1abf-4fc3-90f2-310e70f0fac2)


![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/34b3d5e5-598e-447c-8742-60549b733e71)




IDENTIFICACIÓN DE RELACIONES ENTRE VARIABLES.


Ahora para ver la relación entre las variables podemos hacer una matriz de correlación, dado que tenemos columnas que tienen diferentes tipos de datos entre sí, haremos sub-data set para poder hacer la matriz de correlación, además crearemos un sub-data set que contenga las columnas categóricas códificadas para hacer una matriz de correlación con el mayor número de columnas posibles, así veremos las relaciones entre las columnas.



![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/bb6e4f03-826d-41d7-9e14-9a06a7120fd2)

La correlación entre el año del accidente y el mes del accidente es muy débil (-0.033764). Esto significa que no hay una relación significativa entre estas dos variables.

La correlación entre el número total de personas a bordo y el número total de fallecidos es fuerte (0.739646). Esto significa que existe una relación positiva entre estas dos variables, lo que indica que cuanto mayor es el número de personas a bordo, mayor es el número de fallecidos en un accidente aéreo.




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




ANÁLISIS DE DATOS.



Gráfico de líneas: Este gráfico es el más adecuado para ver la tendencia a largo plazo. Podemos utilizar este gráfico para ver si ha habido un cambio en el número de fallecidos a lo largo de los años, así podremos identificar Outliers.

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/85f5c3c0-ee8f-49e3-a2c7-8c44c244c4e5)

 El gráfico muestra que el número de accidentes aéreos ha disminuido en general a lo largo de los años, con un pico en la década de 1970 .

El gráfico también muestra que el número de accidentes aéreos ha sido más variable en los últimos años, con un aumento significativo en el número de accidentes en 2021. Este aumento puede deberse a una serie de factores, como la pandemia de COVID-19, que provocó una reducción en el número de vuelos, y el conflicto en Ucrania, que ha afectado a la aviación civil en Europa, también el envejecimiento de las flotas áreas puede aumentar los accidentes aéreos.

En general, el gráfico muestra que la seguridad de la aviación ha mejorado significativamente en los últimos años. Sin embargo, es importante seguir tomando medidas para reducir aún más el número de accidentes aéreos.




MÉTRICAS

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/ef19043d-e92e-417d-9bd4-f54626465db9)

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/e59adf4f-9c14-4501-9a57-ab380b4a3635)

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/53925775-49f4-4d8a-9391-56d9ba9e8037)

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/5f0cf134-4f75-4d05-a265-0190e013b671)



KPIS

KPIS: Un KPI (Key Performance Indicator) es una medida cuantificable que muestra cómo efectivamente se están cumpliendo los objetivos de una empresa. Los KPIs son utilizados para medir el rendimiento de la empresa en relación a sus objetivos estratégicos más importantes.

# Agregamos una columna con el total de accidentes por año
df_1['total_accidentes'] = df_1.groupby('ano_accidente')['ano_accidente'].transform('size')
# Filtramos los datos para los últimos 10 años
df_last_10_years = df_1[df_1['ano_accidente'] >= 2011]

# Filtramos los datos para la década anterior
df_previous_decade = df_1[(df_1['ano_accidente'] >= 2000) & (df_1['ano_accidente'] <= 2010)]

# Calculamos la tasa de fatalidad de la tripulación para los últimos 10 años
tasa_fatalidad_tripulacion_last_10_years = df_last_10_years['fallecidos_tripulacion'].sum() / df_last_10_years['total_accidentes'].sum()



DASHBOARD

![imagen](https://github.com/alber1010/PROYECTO_DATA_ANALYTICS/assets/112127531/aa3245c0-be78-462a-a559-5d85df505c8e)


CONCLUSIÓN

La tasa de mortalidad en accidentes aéreos también ha disminuido. En 1908, el 90% de los accidentes aéreos resultaron en muertes, mientras que en 2021 solo el 50% de los accidentes aéreos resultaron en muertes. Esto representa una disminución del 40%.

Estas mejoras en la seguridad aérea se deben a una serie de factores, entre los que se incluyen:

El desarrollo de nuevas tecnologías y procedimientos de seguridad.
La mejora de la formación de pilotos y personal de mantenimiento.
La intensificación de los esfuerzos de investigación de accidentes.
A pesar de estos avances, es importante tener en cuenta que los accidentes aéreos siguen siendo una posibilidad. Sin embargo, las probabilidades de que ocurra un accidente aéreo son muy bajas.


















