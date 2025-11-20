# Memoria Proyecto ABC Corporation

### Conclusiones del Análisis Exploratorio de Datos (**EDA**)

El archivo *.csv* proporcionado para el proyecto presenta las siguientes columnas con datos:

    ['age',
    'attrition',
    'businesstravel',
    'dailyrate',
    'department',
    'distancefromhome',
    'education',
    'educationfield',
    'employeecount',
    'employeenumber',
    'environmentsatisfaction',
    'gender',
    'hourlyrate',
    'jobinvolvement',
    'joblevel',
    'jobrole',
    'jobsatisfaction',
    'maritalstatus',
    'monthlyincome',
    'monthlyrate',
    'numcompaniesworked',
    'over18',
    'overtime',
    'percentsalaryhike',
    'performancerating',
    'relationshipsatisfaction',
    'standardhours',
    'stockoptionlevel',
    'totalworkingyears',
    'trainingtimeslastyear',
    'worklifebalance',
    'yearsatcompany',
    'yearsincurrentrole',
    'yearssincelastpromotion',
    'yearswithcurrmanager',
    'sameasmonthlyincome',
    'datebirth',
    'salary',
    'roledepartament',
    'numberchildren',
    'remotework']

En las que se observan los siguientes patrones y características:

**age**     
Edad del empleado
> presenta números y ('51', '52'...) y palabras ('fifty-five').

propuesta de mejora:
> .

**attrition**   
Indica si el empleado dejó la empresa (Yes/No)
> .

propuesta de mejora:
> .

**businesstravel**  
Frecuencia de viajes
> .

propuesta de mejora:
> .

**dailyrate**   
Tarifa diaria estimada para clientes, calculada en base al salario

> .

propuesta de mejora:
> 

**department**
Departamento en el que trabaja el empleado
> .

propuesta de mejora:
> .

**distancefromhome**
Distancia en millas o kilómetros desde el hogar al trabajo
> .

propuesta de mejora:
> .

**education**   
Nivel educativo del empleado en escala numérica
> .

propuesta de mejora:
> .

**educationfield**  
Campo de estudio académico del empleado
> .

propuesta de mejora:
> .

**employeecount**   
Valor constante de "1", indicando un solo empleado por registro
> Valor = [1]
dtype('int64')

- Este campo es redundante, ya que cada registro corresponde a un único empleado (valor siempre igual a 1).

propuesta de mejora:
> # 1. Eliminar columna
df.drop(columns='employeecount', inplace=True)

**employeenumber**
Número de identificación del empleado
> Valores = [   1,    2,    3, ..., 1612, 1613, 1614], shape=(1614,)
dtype('int64')

La columna cumple su función como identificador único y correlativo para cada empleado.

propuesta de mejora:
> Mantener sin cambios

**environmentsatisfaction** 
Nivel de satisfacción con el ambiente laboral
> Valores = ([ 1,  3,  4,  2, 42, 37, 35, 25, 27, 31, 39, 21, 15, 14, 33, 19, 12, 13, 28, 47, 36, 29, 24, 46, 16, 22, 41, 49, 11, 48, 18, 10, 45, 38, 17, 20, 26, 43])

dtype('int64')

propuesta de mejora:
> Mantener sin cambios?
  
**gender**  
Género del empleado
> . Valores = array([0, 1])


- No está documentado qué significa cada valor (ej: 0=Femenino?, 1=Masculino?)

propuesta de mejora:
> # 1. Definir explícitamente el significado de cada valor: 
df.rename()

- NOTA: No incluye opciones no binarias o diversidad de género, podría ser interesante que se pudieran añadir más valores y tenerlo en cuenta de cara a la presentación como next steps? 


**hourlyrate**  
Tarifa por hora calculada
> . array([         nan,  69.53208262, 172.84325397, 216.04761905,
        79.97321429, 129.06091077, 246.74801587, 207.17460317,
        60.8859127 ,  36.25443872, 139.99503968,  86.24107143,
       197.84641831,  61.06646825, 245.62003968, 123.97718254,
       148.44246032, 255.96329365, 134.41071429,  71.92559524,
       113.78869048, 175.10019841, 247.49007937, 220.83234127,
        91.34821429,  37.77480159, 198.9593254 , 124.05456349,
       247.58035714, 108.48809524,  43.17857143,  68.46924603,
        32.48710317,  55.26289683,  83.46825397,  79.26388889,
        72.28670635,  45.96428571,  31.66170635,  65.19345238,
        52.24503968, 143.9156746 , 113.40178571, 143.19345238,
       139.86607143,  70.57142857,  97.04861111,  45.02281746,
       223.47619048, 134.9781746 ,  74.40178571,  67.14087302,
        58.06150794,  35.05357143,  73.18948413, 164.33134921,
        43.53968254,  54.79861111, 252.59722222,  83.81646825,
        46.71230159,  33.00297619,  70.77777778,  69.23015873,
        54.55357143,  81.53373016, 217.76289683,  50.76190476,
        88.24007937,  57.36507937, 115.2718254 ,  35.77579365,
        59.95734127,  28.20535714,  54.91468254, 227.48710317,
        78.18055556,  54.08928571, 177.0218254 ,  52.9672619 ,
        46.38988095,  80.88888889, 118.70238095,  56.39781746,
        31.33928571,  38.35515873,  35.67261905,  83.99702381,
        55.25      ,  28.70833333,  69.29464286,  69.7718254 ,
        50.86507937,  38.17460317, 244.35615079,  83.37797619,
        25.97420635, 243.02777778,  26.1031746 ,  76.60714286,
...
        36.60119048, 108.02380952, 226.55853175,  68.27579365,
        31.42956349,  59.94444444,  14.07043651,  66.43154762,
        27.65079365,  26.69642857,  35.99503968,  74.96924603,
        34.76984127,  29.12103175, 108.23015873, 247.47718254,
        67.42460317,  34.82142857, 133.15972222])
dtype('float64')

Tipo de dato: float

- Algunos valores son extremadamente altos (ej: 255.96) o bajos (ej: 14.07). ¿Son reales o errores de cálculo/entrada?

- Algunos valores son NAN. ¿Es un error de recolección o hay empleados sin tarifa asignada?

- Los valores tienen hasta 10 decimales (ej: 69.53208262)

propuesta de mejora:
# 1. Redondear a 2 decimales (estándar para monedas): 
df['hourlyrate'] = df['hourlyrate'].round(2)
# 2. Convertir a numérico (los errores se vuelven NaN)
df["hourlyrate"] = pd.to_numeric(df["hourlyrate"], errors='coerce')

**jobinvolvement**
Nivel de compromiso del empleado en el trabajo
> Valores = array([3, 2, 4, 1])
dtype('int64')

propuesta de mejora:
> Mantener sin cambios  

NOTA: como next steps, poder definir y documentar explícitamente el significado de cada valor: 
ej: 1: 'Bajo compromiso',
    2: 'Compromiso moderado',
    3: 'Compromiso alto',
    4: 'Compromiso excepcional'

**joblevel**
Nivel jerárquico del puesto del empleado
> .

propuesta de mejora:
> .

**jobrole**
Función o rol específico del empleado
> .

propuesta de mejora:
> . 


**jobsatisfaction**
Satisfacción general en el puesto
> Valores = array([3, 4, 1, 2])
dtype('int64')

propuesta de mejora:
> > Mantener sin cambios  

NOTA: como next steps, poder definir y documentar explícitamente el significado de cada valor: 
ej: 1: 'Insatisfecho',
    2: 'Poco satisfecho',
    3: 'Satisfecho',
    4: 'Muy satisfecho'

**maritalstatus**
Estado civil (e.g., Single, Married)
> .

propuesta de mejora:
> . 

**monthlyincome**
Ingreso mensual estimado en base al salario anual
> .

propuesta de mejora:
> . 

**monthlyrate**
Tarifa mensual estimada en función de la tarifa diaria
> .

propuesta de mejora:
> . 

**numcompaniesworked**
Número de empresas previas en las que ha trabajado
> .

propuesta de mejora:
> . 

  
**over18**  
Columna no definida
> .

propuesta de mejora: 
> .

**overtime**  
Indica si el empleado trabaja horas extras (Yes/No)
> . 

propuesta de mejora: 
> . 


**percentsalaryhike** 
Incremento porcentual en el salario
> . 

propuesta de mejora: 
> . 


**performancerating** 
Evaluación de desempeño en una escala numérica 
> . 

propuesta de mejora: 
> . 


**relationshipsatisfaction** 
Satisfacción con relaciones interpersonales en el trabajo
> . 

propuesta de mejora: 
> . 


**standardhours**  
Clasificación de jornada (Full Time/Part Time)
> . 

propuesta de mejora: 
> . 


**stockoptionlevel** 
Nivel de opciones sobre acciones asignadas 
> . 

propuesta de mejora: 
> . 


**totalworkingyears** 
Años totales de experiencia laboral 
> . 

propuesta de mejora: 
> . 


**trainingtimeslastyear** 
Número de sesiones de entrenamiento en el último año 
> . 

propuesta de mejora: 
> . 


**worklifebalance**  
Nivel de balance entre vida personal y laboral
> . 

propuesta de mejora: 
> . 


**yearsatcompany**  
Años en la empresa actual.
> .

propuesta de mejora:
> . 


**yearsincurrentrole**
> . Valores = array([nan, '13,0', '12,0', '11,0', '7,0', '6,0', '4,0', '3,0', '2,0',
       '1,0', '0,0'], dtype=object)

Tipo de dato = Object

propuesta de mejora:
> .  
# 1. Reemplazar la "," por "."
df["yearsincurrentrole"] = df["yearsincurrentrole"].str.replace(',', '.')
# 2. Convertir a numérico (los errores se vuelven NaN)
df["yearsincurrentrole"] = pd.to_numeric(df["yearsincurrentrole"], errors='coerce')
# 3. Rellenar los vacíos con 0
df["yearsincurrentrole"] = df["yearsincurrentrole"].fillna(0)
# 4. Ahora sí, pasar a entero sin miedo
df["yearsincurrentrole"] = df["yearsincurrentrole"].astype(int)
  

**yearssincelastpromotion**
> . Valores = [15, 11,  5,  2,  4,  7,  0,  1, 13, 14,  8, 12,  3,  6, 10,  9]

Tipo de dato = float

propuesta de mejora:
> . En principio nada


**yearswithcurrmanager**
> . Valores = [15,  9,  6,  8,  7, 11, 10, 12,  4,  0,  5, 17,  2, 14,  1, 13,  3, 16]

Tipo de dato = float

propuesta de mejora:
> . En principio nada


**sameasmonthlyincome**  
> . Valores = Datos tipo objeto, con simbolo en "Español" para los decimales y además incluido en el dato el simbolo $

propuesta de mejora:
> .  Cambiar la "," por ".", eliminar también el simbolo "$". Por último cambiar el dato str en float

df["sameasmonthlyincome"] = df["sameasmonthlyincome"].str.replace(',', '.')
df["sameasmonthlyincome"] = df["sameasmonthlyincome"].str.replace('$', '', regex=False)
df["sameasmonthlyincome"] = df["sameasmonthlyincome"].astype(float)



**datebirth**  
Año de nacimiento del empleado
> . Valores = [1972, 1971, 1981, 1976, 1977, 1975, 1964, 1982, 1967, 1985, 1968,
       1983, 1965, 1988, 1978, 1990, 1987, 1989, 1970, 1980, 1963, 1991,
       1986, 1974, 1984, 1973, 1979, 1993, 1994, 1992, 1969, 1966, 1996,
       1995, 1997, 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005]

Tipo de dato = float

propuesta de mejora:
> . En principio nada


**salary**  
Salario anual calculado para el empleado
> . Valores = Datos tipo objeto, con simbolo en "Español" para los decimales y además incluido en el dato el simbolo $

propuesta de mejora:
> . Cambiar la "," por ".", eliminar también el simbolo "$". Por último cambiar el dato str en float

df["salary"] = df["salary"].str.replace(',', '.')
df["salary"] = df["salary"].str.replace('$', '', regex=False)
df["salary"] = df["salary"].astype(float)


**roledepartament**  
Combinación de rol y departamento.
> . df["roledepartament"].value_counts().sum() el resultado es 312 nombres distintos pero hay muchos que son lo mismo pero cambiando mayusculas y minusculas

propuesta de mejora:

> .df["roledepartament"].str.lower()
    
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


**numberchildren**  
Número de hijos del empleado
> . Valores = [nan]

propuesta de mejora:
> . Posible columna a eliminar


**remotework**  
Empleado trabaja de forma remota Si/No
> . Valores =[ 'Yes', '1', 'False', '0', 'True']

Todos son str aunque haya número de por medio. Quizás el 0 signifique Si/Yes y el 1 signifique No. También es posible que el True sea igual a Si/Yes y el False sea No
propuesta de mejora:
> . unificar datos