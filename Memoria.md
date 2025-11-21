# Memoria Proyecto ABC Corporation

### Conclusiones del Análisis Exploratorio de Datos (EDA)

El archivo *.csv* proporcionado para el proyecto presenta las siguientes columnas con datos:

- [Age](#age)
- [Attrition](#attrition)
- [Business Travel](#businesstravel)
- [Daily Rate](#dailyrate)
- [Department](#department)
- [Distance From Home](#distancefromhome)
- [Education](#education)
- [Education Field](#educationfield)
- [Employee Count](#employeecount)
- [Employee Number](#employeenumber)
- [Environment Satisfaction](#environmentsatisfaction)
- [Gender](#gender)
- [Hourly Rate](#hourlyrate)
- [Job Involvement](#jobinvolvement)
- [Job Level](#joblevel)
- [Job Role](#jobrole)
- [Job Satisfaction](#jobsatisfaction)
- [Marital Status](#maritalstatus)
- [Monthly Income](#monthlyincome)
- [Monthly Rate](#monthlyrate)
- [Number of Companies Worked](#numcompaniesworked)
- [Over 18](#over18)
- [Overtime](#overtime)
- [Percent Salary Hike](#percentsalaryhike)
- [Performance Rating](#performancerating)
- [Relationship Satisfaction](#relationshipsatisfaction)
- [Standard Hours](#standardhours)
- [Stock Option Level](#stockoptionlevel)
- [Total Working Years](#totalworkingyears)
- [Training Times Last Year](#trainingtimeslastyear)
- [Work Life Balance](#worklifebalance)
- [Years at Company](#yearsatcompany)
- [Years in Current Role](#yearsincurrentrole)
- [Years Since Last Promotion](#yearssincelastpromotion)
- [Years with Current Manager](#yearswithcurrmanager)
- [Same as Monthly Income](#sameasmonthlyincome)
- [Date of Birth](#datebirth)
- [Salary](#salary)
- [Role Department](#roledepartament)
- [Number of Children](#numberchildren)
- [Remote Work](#remotework)

---

### En las que se observan los siguientes patrones y características:

#### Patrones globales:

- Valores numericos junto al símbolo '$'

  ``.str.replace()`` ("," por ".") y $ por ' ' 

  Ejemplo de solución para estandarizar los valores numéricos que lo requieran:

  ``.to_numeric()`` - para convertir de objeto a int/float     
  ``.round()`` - redondear a entero o a dos decimales   

  ¿Añadir $ con metodos que desconocemos ahora que no afectan dtype int/float?

- Valores objeto     
``.lower()`` - todo

---
### RAW_DATA.CSV 
### age
(dtype: int64)       
*Edad del empleado*

       Valores numéricos ('51', '52'...) y palabras ('fifty-five').

Propuesta de mejora:
- Homogeneizar al mismo formato numérico.
#
### attrition
(dtype: object)      
*Indica si el empleado dejó la empresa (Yes/No)*

       Objetos: Yes/No. Sin nulos.

Propuesta de mejora:  
Sin Anomalías.

---
### businesstravel
(dtype: object)      
*Frecuencia de viajes*

       Valores nulos (2) y objetos: ('nan'), 'travel_rarely', 'travel_frequently', 'non-travel'.

Hay que investigar si el ``nan`` tiene más valores ``nan`` asociados al mismo empleado.

Propuesta de mejora:        
- Sustituir ``nan`` por ``None`` o ``null`` según queramos procesar los datos más adelante (o si hay paso a SQL).

---
### dailyrate
(dtype: int64)       
*Tarifa diaria estimada para clientes, calculada en base al salario*

       Valores únicos (673) con decimales largos y variados.

Propuesta de mejora:        
- Usar ``round()`` para estandarizar la precisión.

- Asegurarse de aplicar el mismo criterio a todas las columnas numéricas relativas al salario en el dataset (puntuación y redondeo).
---
### department
(dtype: object)   
*Departamento en el que trabaja el empleado*

       Valores nulos y objetos: 'nan', ' Research & Development ', ' Sales ', ' Human Resources '

       En cantidad: 
       NaN                         1366
       Research & Development      203
       Sales                        93
       Human Resources              16

Propuesta de mejora:        
- Convertir a minuscula todos los nombres        
``df["department"] = df["department"].str.lower()``

       Ejemplo:
       array([nan, ' research & development ', ' sales ', ' human resources '],
      dtype=object)

- Comparar los valores nulos con las columnas que incluyen datos aparentemente reiterados, que pueden contener este valor en ausencia de estar presentes en esta columna.

  ->  referencia: columna [roledepartament](#roledepartment)      

  En caso de doble ausencia: recomiendo conservar el nulo en el formato que nos requiera el proyecto para procesarlo, si no es un empleado con todos los valores nulos:   
  ``df['department'] = df['department'].fillna('None')``

- Sustituir espacios innecesarios al inicio, final y entre las palabras del valor (``' Human Resources '``) por valores estandarizados y sin espacios innecesarios:         
``df['department'] = df['department'].str.strip()``

    ``.str.replace(r'\s+', ' ', regex=True)``

---
### distancefromhome
(dtype: int64)       
*Distancia en millas o kilómetros desde el hogar al trabajo*
       
       Valores numéricos positivos, negativos y espaciados extra entre caracteres.
       
        ([  6,   1,   4,   2,   3,  22,  25,   9,   7,  23,  10,  12,  14, -13,  15,   8, -42,  28, -37,   5,  16, -35, 26, -26,  24,  29, -25,  17,  21, -18, -10, -30, -27, 20, -31, -29 -39,  18, -21, -15,  11,  13, -14,  19, -33 -34, -46, -36, -19,  27, -12, -23, -45, -28, -47, -32, -24, -16, -22, -41, -49, -11, -48, -38, -20, -17, -43, -40, -44])


Propuesta de mejora:
- Convertimos en absolutos para eliminar el negativo    
``df["distancefromhome"] = df["distancefromhome"].abs()``

---
### education
(dtype: int64)     
*Nivel educativo del empleado en escala numérica*

       Valores numéricos: ([3, 4, 2, 1, 5])

Propuesta de mejora:        
Sin anomalías.

---
### educationfield
(dtype: object)      
*Campo de estudio académico del empleado*

       Valores nulos y objetos: 'Life Sciences', 'Technical Degree', 'Medical', 'Other',
       'Marketing', 'Human Resources'.

Propuesta de mejora:
- Misma propuesta para los nulos que para la columna [department](#department).
- Convertir a minuscula todos los nombres        
``df["educationfield"] = df["educationfield"].str.lower()``

       Ejemplo
       array([nan, 'life sciences', 'technical degree', 'medical', 'other', 'marketing', 'human resources'], dtype=object)
       
---
### employeecount
(dtype: int64)       
*Valor constante de "1", indicando un solo empleado por registro*

       Valor = [1]

Este campo es redundante, ya que cada registro corresponde a un único empleado (valor siempre igual a 1).

Propuesta de mejora:
- Eliminar columna:  
``df.drop(columns='employeecount', inplace=True)``
---
### employeenumber
(dtype: int64)       
*Número de identificación del empleado*

       Valores = [   1,    2,    3, ..., 1612, 1613, 1614], shape=(1614,)

La columna cumple su función como identificador único y correlativo para cada empleado.

Propuesta de mejora  
Mantener sin cambios

---
### environmentsatisfaction
(dtype: int64)   
*Nivel de satisfacción con el ambiente laboral*

       Valores = ([ 1,  3,  4,  2, 42, 37, 35, 25, 27, 31, 39, 21, 15, 14, 33, 19, 12, 13, 28, 47, 36, 29, 24, 46, 16, 22, 41, 49, 11, 48, 18, 10, 45, 38, 17, 20, 26, 43])

Propuesta de mejora:
- ¿Mantener sin cambios?
- Plantearnos si es un formato tan raro, si podemos apostar por aplanarlo o simplificarlo, por ejemplo: decidir acortar las distancias entre 0 y 50 pasándolos a decimal entre 0-5.

---
### gender
(dtype: int64)       
*Género del empleado*
       
       Valores = array([0, 1])


No está documentado qué significa cada valor (ej: 0=Femenino?, 1=Masculino?)

Propuesta de mejora:
- Definir explícitamente el significado de cada valor:  
``df.rename()``
- ¿Tendremos que referirnos al exponer los datos simplemente al primer género y al segundo género?

       NOTA: No incluye opciones no binarias o diversidad de género, podría ser interesante que se pudieran añadir más valores y tenerlo en cuenta de cara a la presentación como next steps? 

---
### hourlyrate
(dtype: float64)
*Tarifa por hora calculada*
       
       Valores nulos y decimales.

        array([nan,  69.53208262, 172.84325397, 216.04761905,
        79.97321429, 129.06091077, 246.74801587, 207.17460317,
        60.8859127 ,  36.25443872, 139.99503968,  86.24107143,
       ... 67.42460317,  34.82142857, 133.15972222])


Algunos valores son extremadamente altos (ej: 255.96) o bajos (ej: 14.07). ¿Son reales o errores de cálculo/entrada?

Algunos valores son NaN. ¿Es un error de recolección o hay empleados sin tarifa asignada?

Los valores tienen hasta 10 decimales (ej: 69.53208262)

Propuesta de mejora:
- Redondear a 2 decimales (estándar para monedas):       
``df['hourlyrate'] = df['hourlyrate'].round(2)``
- Convertir a numérico (los errores se vuelven NaN)     
``df["hourlyrate"] = pd.to_numeric(df["hourlyrate"], errors='coerce')``
- ¿Compararlo con el resto de valores salariales para comprobar si el punto que aparece es realmente una coma?

---
### jobinvolvement
(dtype: int64)       
*Nivel de compromiso del empleado en el trabajo*

       Valores = array([3, 2, 4, 1])

Propuesta de mejora:        
Mantener sin cambios. 

O:

       NOTA: como next steps, poder definir y documentar explícitamente el significado de cada valor: 
       ej: 1: 'Bajo compromiso',
       2: 'Compromiso moderado',
       3: 'Compromiso alto',
       4: 'Compromiso excepcional'
¿Incluimos 0 y 5?

---
### joblevel
(dtype: int64)       
*Nivel jerárquico del puesto del empleado*
       
       Valores = array([5, 4, 3, 2, 1])

Propuesta de mejora:        
Sin anomalías.

---
### jobrole
(dtype: object)      
Función o rol específico del empleado

       Valores = array([' resEArch DIREcToR ', ' ManAGeR ', ' ManaGER ', ...,
       ' sAlES ExECUTivE ', ' SaLes ExecUtIVe ',
       ' mAnUfactURInG DiRECTOr '], dtype=object)

Objetos como valores con escritura irregular.

Propuesta de mejora:
- Convertir a minuscula todos los nombres        
``df["jobrole"] = df["jobrole"].str.lower()``

       Ejemplo:
       array([' research director ', ' manager ', ' sales executive ',
       ' manufacturing director ', ' research scientist ',
       ' healthcare representative ', ' laboratory technician ',
       ' sales representative ', ' human resources ']
---
### jobsatisfaction
(dtype: int64)       
*Satisfacción general en el puesto*

       Valores = array([3, 4, 1, 2])

Propuesta de mejora:        
Mantener sin cambios.  

O:

       NOTA: como next steps, poder definir y documentar explícitamente el significado de cada valor: 
       ej: 1: 'Insatisfecho',
       2: 'Poco satisfecho',
       3: 'Satisfecho',
       4: 'Muy satisfecho'

¿Incluimos 0 y 5?

---
### maritalstatus
(dtype: object)      
*Estado civil (e.g., Single, Married)*

       Values total 1678 | Unique 5 + NaN | dtype - objects. (incluye NaN - 675 - muchos) Null - TBD

              NaN         675
              Married     419
              Single      343
              Divorced    194
              Marreid      36
              divorced     11

Propuesta de mejora:
- lower() todos      
´´df["maritalstatus"] = df["maritalstatus"].str.lower()´´
- replace ``Marrieid`` por ``Married``    
``df["maritalstatus"] = df["maritalstatus"].str.replace("marreid", "married")``
- Null - TBD
---
### monthlyincome
(dtype: object)       
*Ingreso mensual estimado en base al salario anual*

       Values U1678 | Unique 493 + NaN | dtype - int. (incluye NaN - 498 - muchos) |  **Null - TBD**

              muestra de valores:
              NaN          489
              2342,59$     228
              4492,84$     227

Propuesta de mejora:
- Usar ``replace()`` ``,`` por ``.`` y usar ``replace()`` ``$`` por ``""``:
``df["monthlyincome"] = df["monthlyincome"].str.replace("$", "", regex=False).str.replace(",", ".", regex=False)``

       -->regex false - pandas puede pensar que es una funcion regex
- Cambiar a numérico de tipo float:        
``df["monthlyincome"] = df["monthlyincome"] = pd.to_numeric(df["monthlyincome"], errors="coerce")``
       
       --> errors="coerce" asegura que, si no se cumple, convierte en NaN
       
       ie. 40 esta como 'forty'
              muestra monthlyincome limpio:
              0       16280.83
              1            NaN
              2            NaN
              3       14307.50
              4       12783.92
---
### monthlyrate
(dtype: object)      
*Tarifa mensual estimada en función de la tarifa diaria*

       Values 1678 | Unique 673 | NaN 0 | dtype Object  

Propuesta de mejora:
- Mismo que en ``monthlyincome``   
``df["monthlyrate"] = df["monthlyrate"].str.replace("$", "", regex=False).str.replace(",", ".", regex=False)``

       -->regex false - pandas puede pensar que es una funcion regex
- ``df["monthlyrate"] = df["monthlyrate"] = pd.to_numeric(df["monthlyrate"], errors="coerce")``

       --> errors="coerce" asegura que si no se cumple convierte en NaN
       
       ie. 40 esta como 'forty'

### numcompaniesworked
(dtype: int64)       
*Número de empresas previas en las que ha trabajado*

       Valores = array([7, 0, 1, 3, 2, 4, 8, 9, 5, 6])

       Values 1678 | Unique 10 (0-9) | NaN 0 | dtype int

Propuesta de mejora:
- Entiendo que son la cantidad de empresas donde el trabajador ha trabajado. cv - empleos en companias anteriores.
- ¿Igual podemos llamarlo experiencia en diferentes empresas? ¿Score empleos previos?
---
### over18
(dtype: object)       
*columna no definida*

       Valores = array(['Y', nan], dtype=object)

       Values 1678 | dtype Object | Unique 1 | NaN 1 (938 valores NaN -- muchos, la mayoria)

No existe valor N (No), solo Y (Yes) o NaN.

Interpreto que es muy incompleto, con 56% NaN, para darle peso en el analysis global.

       Muestra de valores y counts:
       NaN    938
       Y      740

Propuesta de mejora:
- Clase: Gestion de Nulos propongo omitirlo por falta de valor/peso analytico.
- ¿Comprobar si coinciden con los valores de la columna [overtime](#overtime)?
---
### overtime
(dtype: object)      
*Indica si el empleado trabaja horas extras (Yes/No)*

       Valores = array(['No', nan, 'Yes'], dtype=object)

Propuesta de mejora: 
- Clase: Gestion de Nulos.
- ¿Atribuir ``NaN`` como ``Desconocido`` y darle valor a la información de quien tiene un claro Yes?
---
### percentsalaryhike
(dtype: int64)       
*Incremento porcentual en el salario*

       Valores = array([13, 14, 11, 19, 12, 25, 16, 17, 22, 23, 20, 15, 21, 24, 18])

Propuesta de mejora:        
Mantener sin cambios.

---
### performancerating
(dtype: object)      
*Evaluación de desempeño en una escala numérica* 

       Valores = array(['3,0', '4,0', nan], dtype=object)

Propuesta de mejora:
- Reemplazar ``,`` por ``.``:      
``df["performancerating"] = df["performancerating"].str.replace(',', '.')``
- Rellenar los vacíos con 0:       
``df["performancerating"] = df["performancerating"].fillna(0)``
- Convertir a float:        
``df["performancerating"] = df["performancerating"].astype(float)``

       Ejemplo:
       array([3., 4., 0.]) // dtype('float64')

- Otra sugerencia: para evitar que el nuevo valor ``0`` baje la media del *performance rating*, ¿sustituir por ``Desconocido``?
---
### relationshipsatisfaction
(dtype: int64)       
*Satisfacción con relaciones interpersonales en el trabajo*

       Valores = array([3, 1, 4, 2])

Propuesta de mejora:        
Mantener sin cambios.  

O:

       NOTA: como next steps, poder definir y documentar explícitamente el significado de cada valor: 
       1: 'Insatisfecho',
       2: 'Poco satisfecho',
       3: 'Satisfecho',
       4: 'Muy satisfecho'

¿Incluimos 0 y 5?

---
### standardhours
(dtype: object)      
*Clasificación de jornada (Full Time/Part Time)*

       Valores = array(['Full Time', nan, 'Part Time'], 
       dtype=object)

Faltan valores: ``NaN``.
standardhours tiene 927 'part time', 400 full time y 351 nulos
-por qué faltan las horas estándar a 351 registros?
-error de registro? categoría ausente para alguna trabajadora?
-dependiendo de lo que sea: 1)Reemplazar nulos por otra catergoría 'desconocido'; 2)Eliminar nulos

Propuesta de mejora:
- Mirar la relacion con otras columnas para asegurarnos si el nulo es por falta de informacion, o por otro tipo de clasificacion de jornada (ej: 'Freelance'?, 'Otro', 'No Especificado'). EJ:    
 ``df['standardhours'] = df['standardhours'].replace(np.nan, 'No especificado')``
 `` df['standardhours'] = df['standardhours'].str.lower()`` # convertir todo a minúsculas para normalizar todas categorías

---
### stockoptionlevel
(dtype: int64)       
*Nivel de opciones sobre acciones asignadas.*

       Valores numéricos ([0, 1, 2, 3])

Propuesta de mejora:
Mantener sin cambios.

---
### totalworkingyears
(dtype: object)      
*Años totales de experiencia laboral*

       Valores = array([nan, '34,0', '22,0', '28,0', '20,0', '21,0', '33,0', '40,0',
       '18,0', '25,0', '15,0', '17,0', '26,0', '16,0', '24,0', '14,0',
       '23,0', '27,0', '19,0', '11,0', '38,0', '37,0', '13,0', '12,0',
       '29,0', '10,0', '36,0', '35,0', '9,0', '31,0', '32,0', '8,0',
       '7,0', '30,0', '6,0', '5,0', '4,0', '3,0', '2,0', '1,0', '0,0'],
      dtype=object)

Propuesta de mejora: 
- Reemplazar ``,`` por ``.``       
``df["totalworkingyears"] = df["totalworkingyears"].str.replace(',', '.')``
- Posibilidad de cambiar a 0 Gestión de nulos:   
``df["totalworkingyears"] = df["totalworkingyears"].fillna(0)``
- Convertir a float:        
``df["totalworkingyears"] = df["totalworkingyears"].astype(float)``

                     
       Resultado: array([ 0, 34, 22, 28, 20, 21, 33, 40, 18, 25, 15, 17, 26, 16, 24, 14, 23, 27, 19, 11, 38, 37, 13, 12, 29, 10, 36, 35,  9, 31, 32,  8,  7, 30, 6,  5,  4,  3,  2,  1])

- Comprobar si el nulo en años de experiencia laboral es dispar con la columna [numcompaniesworked](#numcompaniesworked).
---
### trainingtimeslastyear
(dtype: int64)       
*Número de sesiones de entrenamiento en el último año.*

       Valores numéricos ([5, 3, 2, 0, 1, 4, 6])

Propuesta de mejora:        
Mantener sin cambios.

---
### worklifebalance
(dtype: object)      
*Nivel de balance entre vida personal y laboral.*

       Valores = array(['3,0', nan, '2,0', '4,0', '1,0'], dtype=object)

Propuesta de mejora:
- Reemplazar la ``,`` por ``.``:   
``df["worklifebalance"] = df["worklifebalance"].str.replace(',', '.')``
- Gestión de nulos
- Posibilidad de cambiar a 0 Gestión de nulos:   
``df["worklifebalance"] = df["worklifebalance"].fillna(0)``
- Convertir a float:        
``df["worklifebalance"] = df["worklifebalance"].astype(float)``
- Ahora sí, pasar a entero sin miedo:     
``df["worklifebalance"] = df["worklifebalance"].astype(int)``

       Resultado: array([3, 0, 2, 4, 1])
---
### yearsatcompany
(dtype: int64)   
*Años en la empresa actual.*

       Valores = array([20, 33, 22, 19, 21, 18, 24, 31, 26, 16, 23, 15, 17, 32, 14, 13, 25, 12, 11, 37, 40, 36, 27, 29, 10,  9, 30,  8,  7, 34,  6,  5,  4,  2, 3,  1,  0])

Propuesta de mejora:        
Mantener sin cambios.

- Sería interesante comparar los años en la empresa actual con los valores nulos en la columna [totalworkingyears](#numcompaniesworked) para comprobar qué relato/perfil nos devuelve.
---
### yearsincurrentrole
(dtype: object)      

       Valores = array([nan, '13,0', '12,0', '11,0', '7,0', '6,0', '4,0', '3,0', '2,0',
       '1,0', '0,0'], dtype=object)

Propuesta de mejora:
- Reemplazar la ``,`` por ``.``:   
``df["yearsincurrentrole"] = df["yearsincurrentrole"].str.replace(',', '.')``
- Rellenar los vacíos con 0        
``df["yearsincurrentrole"] = df["yearsincurrentrole"].fillna(0)``
- Convertir a float:        
``df["yearsincurrentrole"] = df["yearsincurrentrole"].astype(float)``
-Ahora sí, pasar a entero sin miedo:      
``df["yearsincurrentrole"] = df["yearsincurrentrole"].astype(int)``

       Resultado:
       array([ 0, 13, 12, 11,  7,  6,  4,  3,  2,  1])
  
---
### yearssincelastpromotion
(dtype: int64)       

       Valores = [15, 11,  5,  2,  4,  7,  0,  1, 13, 14,  8, 12,  3,  6, 10,  9]

Propuesta de mejora:        
Mantener sin cambios.
---
### yearswithcurrmanager
(dtype: int64)       
*Años trabajando con el mismo gerente.*

       Valores = [15,  9,  6,  8,  7, 11, 10, 12,  4,  0,  5, 17,  2, 14,  1, 13,  3, 16]


Propuesta de mejora:        
Mantener sin cambios.

---
### sameasmonthlyincome
(dtype: object)     
*columna sin especificar*

       Valores = Datos tipo objeto, con simbolo en "Español" para los decimales y además incluido en el dato el simbolo $

Propuesta de mejora:
- Cambiar la ``,`` por ``.``, eliminar también el simbolo ``$``. Por último cambiar el valor objeto a float

``df["sameasmonthlyincome"] = df["sameasmonthlyincome"].str.replace(',', '.')``

``df["sameasmonthlyincome"] = df["sameasmonthlyincome"].str.replace('$', '', regex=False)``

``df["sameasmonthlyincome"] = df["sameasmonthlyincome"].astype(float)``

- ¿Comprobar si esta columna es una copia redundante de [monthlyincome](#monthlyincome)?
---
### datebirth
(dtype: int64)       
*Año de nacimiento del empleado*

       Valores = [1972, 1971, 1981, 1976, 1977, 1975, 1964, 1982, 1967, 1985, 1968, 1983, 1965, 1988, 1978, 1990, 1987, 1989, 1970, 1980, 1963, 1991, 1986, 1974, 1984, 1973, 1979, 1993, 1994, 1992, 1969, 1966, 1996, 1995, 1997, 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005]

Propuesta de mejora:
Mantener sin cambios.

---
### salary
(dtype: object)        
*Salario anual calculado para el empleado*

       Valores = Datos tipo objeto, con simbolo en "Español" para los decimales y además incluido en el dato el simbolo $

Propuesta de mejora:
- Cambiar la ``,`` por ``.``, eliminar también el simbolo ``$``. Por último cambiar el valor tipo objeto a float

``df["salary"] = df["salary"].str.replace(',', '.')``

``df["salary"] = df["salary"].str.replace('$', '', regex=False)``

``df["salary"] = df["salary"].astype(float)``

---
### roledepartament
(dtype: object)      
*Combinación de rol y departamento.*

       Valores = array([nan, ' manager  -  research & development ',
       ' healthcare representative  -  research & development ',
       ' sales executive  -  sales ',
       ' laboratory technician  -  research & development ',
       ' manufacturing director  -  research & development ',
       ' research scientist  -  research & development ',
       ' research director  -  research & development ',
       ' human resources  -  human resources ', ' manager  -  sales ',
       ' sales representative  -  sales ',
       ' manager  -  human resources '], dtype=object)

Propuesta de mejora:

- df["roledepartament"] = df["roledepartament"].str.lower() 
    
       [nan, ' manager  -  research & development ',
       ' healthcare representative  -  research & development ',
       ' sales executive  -  sales ',
       ' laboratory technician  -  research & development ',
       ' manufacturing director  -  research & development ',
       ' research scientist  -  research & development ',
       ' research director  -  research & development ',
       ' human resources  -  human resources ', ' manager  -  sales ',
       ' sales representative  -  sales ',
       ' manager  -  human resources ']

- ¿Comprobar si esta columna es redundante o si contiene los datos que faltan en [department](#department) y [jobrole](#jobrole)?
- ¿Destinarla a eliminación una vez reubicados todos los valores?
---
### numberchildren
(dtype: float64)     
*Número de hijos del empleado*

       Valores = [nan]

Propuesta de mejora:
- Posible columna a eliminar.
- ¿Es información la ausencia de información al respecto?

---
### remotework
(dtype: object)      
*Indica si el empleado trabaja de forma remota (Yes/No).*

       Valores =[ 'Yes', '1', 'False', '0', 'True']

Todos son objetos aunque haya número de por medio. Quizás el 0 signifique Si/Yes y el 1 signifique No. También es posible que el True sea igual a Si/Yes y el False sea No

Propuesta de mejora:
- Unificar datos.
