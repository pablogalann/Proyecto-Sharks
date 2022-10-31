# Proyecto-Sharks

- 1º) IMPORTAR PANDAS, NUMPY, VISUALIZACION FILAS Y COLUMNAS, BLOQUE DE ERRORES

- 2º) ABRIR EL ARCHIVO. ( r' + RUTA CARPETA UBICACION DE ARCHIVO + \NOMBRE_ARCHIVO.csv ,encoding='latin1' )

- 3º) VISUALIZACION DE INFORMACION GENERAL: .head .info, .shape .columns

- 4º) MODIFICIAR TITULOS DE LAS COLUMNAS:
Queremos evitar espacios y diferencias entre mayusculas y minusculas.

- 5º) Localizar valores nulos:

     Creamos una nueva variable donde apareceran las columnas con valores NaN, llamada nan_cols.
     ¿Que valores del dataFrame son nulos? df.isna() 
     Muestrame las columnas con valores nulos donde en esas columnas dichos valores sean superiores a cero.

    A. Muestrame los valores segun el PORCENTAJE % que representan en la columna
    B. Muestame el SUMATORIO de datos nulos en cada columna.


- 6º) Borrado de columnas con un porcentaje de nulos muy elevado/ con un gran numero de nulos 

                data.drop( columns = nombre_columna[nombre_columna>condición].index , inplace = True)
                
        EJEMPLOS               

        - Borrame las columnas(columns = ) de dentro de las columnas con nulos(nan_cols) cuyos % valores nulos es superior a 90%(>90) 

        data.drop(columns=nan_cols[nan_cols>90].index, inplace = True)

        - Borrame las columnas(columns = ) de dentro de las columnas con nulos(nan_cols) cuyos valores son superiores 10000ud 

        data.drop(columns=nan_cols[nan_cols>1e4].index, inplace = True) 


- 7º) Localizacion gráfica de datos nulos según los datos obtenidos anteriormente

- 8º) BORRADO DE FILAS CON ALTO CONTENIDO EN NULOS:

    ES MÁS RAPIDO Y PREFERIBLE UTILIZAR EL MÉTODO DE BORRAR DUPLICADOS:
    data.drop_duplicates().shape==data.shape

    data.drop_duplicates(inplace=True)

    AQUI METODO DE BORRADO POR FILAS ↓ ↓ ↓
    
            Nombredataframe.dropna(subset=nombredataframe.columns, inplace = True, how= 'all')
            
         Para cada FILA en una grupo de columnas(data.columns, también puede ser una lista de columnas) eliminame aquellas cuyo valor serepite en cada una de las columnas seleccionas(data.columns) IMPORTANTE how = 'all'

        Elimina las filas inferiores, ya que en esas filas los valores en las columnas seleccionadas(data.columns) son todos NAN y se repiten en todas y cada una de las casillas de esa fila (how = 'all')



-9º) MODIFICACIÓN DE VALORES NULOS E INCONSISTENTES

Comprobamos que en la columna 'HrefFormula' hay 1 valores nulos

Lineas de codigo basicas de busqueda/modificacion

A ¿ Cuantos nulos hay por columna? ¿Cuantos nulos tengo que modificar?

nan_cols = data.isna().sum()
nan_cols[nan_cols>0]

B ¿En que fila estan estos nulos? Contextualizamos con la informacion en el resto de columnas

data[data['nombrecolumna'].isna()]

C SUSTITUIR NULOS por 'Unknown' ceros .... Para poder pasarle la lista de valores a la funcion, nan no interan

data1.nombrecolumna.fillna('Unknown',inplace = True) data1.nombrecolumna.fillna(0,inplace = True)

D ¿ QUE VALORES/OBJETOS HAY en esa columna? Buscamos valores nan y/o inconsistente

data.nombrecolumna.unique()

E ¿ CUANTOS valores/objetos/elementos hay en esa columna? Buscamos la CANTIDAD de valores inconsistentes

data1.Age.value_counts()

F USO DE FILTROS DE COMPARACIÓN

bad_index = df.nombrecolumna[(df.nombrecolumna == 'condicional') & (df.nombrecolumna=='condicional')].index

G USO DE FUNCIONES PARA LIMPIEZA DE DATOS INCONSISTENTES, DEFINIR FUNCIÓN.

H REEMPLAZAR DATOS INCONSISTENTES POR AQUELLOS QUE CONSIDEREMOS APROPIEADOS

data.nombrecolumna = data1.nombrecolumna.str.replace('reemplazable','reemplazo')

data1.loc[indice fila ,'nombrecolumna'] = 'nuevo valor'

-10º) EXPORTAMOS LA TABLA DE PANDA A EXCEL

%pip install xlwt

data1.to_excel(r'C:\Users\pablo\2.5.-Proyecto-Sharks\data\nombrearchivocvs.xls', index=False)



CASO AGE:

1º Localizamos los valores nulos y los sustituimos.
2º Observamos un alto contenido de valores inconsistentes, que no responden a tipo entero, y nos impiden hacer operaciones aritmeticas
3º Realizamos una funcion que limpie dichos valores, buscando patrones de repetición y los convierta a enteros
4º La funcion de limpieza no es capaz de limpiar todo y tenemos que utilizar el replace.
5º Una vez con los datos limpios y enteros realizamos por ejemplo la media


CASO SPECIE:

1º Localizamos los valores nulos y los sustituimos.
2º Observamos un alto contenido de valores inconsistentes
3º Realizamos una funcion que limpie dichos valores, considerando los 20 tiburones mas comunes como una muestra representativa de todos aquellos que aperecen
4º La funcion de limpieza no es capaz de limpiar todo y tenemos que utilizar el replace.


CASO FATAL:

1º Localizamos los valores nulos
2º Observamos en un golpe de vista que muchos de los valores nan estan asociados a la columna Type invalid
3º Según la descripción los valores invalidos son aquellos que no tienen validez a la hora de contabilizarlos como ataque real.
4º Prescindimos de las filas en donde se produce este paralelismo entre Type y Fatal, ya que a mi modo de ver no aportan informacion relevante

CASO ACTIVITY:

1º Localizamos los valores nulos y los sustituimos.
2º Observamos un alto contenido de valores inconsistentes
3º Realizamos una funcion que limpie dichos valores, agrupando las actividades mas representativas.
4º La funcion de limpieza no es capaz de limpiar todo y tenemos que utilizar el replace.


