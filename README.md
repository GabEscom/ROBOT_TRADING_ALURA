# Robot Trading | Challenge | Python | Alura 
<br>
<ul align = center>
<img src=https://github.com/GabEscom/ROBOT_TRADING_ALURA/assets/147789340/623df2f5-a451-4718-88da-833edbd3b15d>
<br>
<img src="https://img.shields.io/badge/Python-f7e172?style=flat&logo=python" alt="Python Badge">
<img src="https://img.shields.io/badge/Pandas-e00484?style=flat&logo=pandas" alt="Pandas Badge"/>
</ul>

## Descripción 📜
Este programa en Python es capaz de tomar decisiones de compra y venta de Bitcoin en tiempo real. ¿Interesante, verdad?

### Configuración del entorno 🖥️
Para comenzar, puedes usar cualquier entorno de Python, asegurándote de que sea la versión 3.X. El entorno base es Jupyter Notebook. También necesitarás instalar algunas librerías de Python esenciales para este proyecto, como:
- Pandas
- Numpy
- Matplotlib
- Yfinance
- Time
- BeautifulSoup
- Request

### Obtención de datos 💾
Se crea la función importar_base_bitcoin() para la obtención de datos.

El Robot Trading utiliza la biblioteca yfinance de Python como fuente de datos para obtener el histórico de precios del Bitcoin en dólares BTC-USD de los últimos 7 días en intervalos de 5 minutos, este histórico e guarda en el dataframe df_bitcoin

Más información de como instalar y usar la biblioteca --> (https://pypi.org/project/yfinance/)

También se crea una funcion llamada extraer_tendencias() para realizar web scraping y obtener el valor actual del bitcoin y su tendencia en la última hora.

Utilizando la biblioteca BeautifulSoup se realiza Web Scraping en la página (https://coinmarketcap.com/) para extraer el precio actual del Bitcoin BTC en dólares USD y la variación de su precio en la última hora 1h % . El precio se convierte atipo float y guarda en la variable llamada precio_actual. Finalmete, en la variable tendencia se guarda el valor de 'baja'si la variación del precio es negativa, sino, guarda el valor de 'alta'.

### Limpieza de datos 🧹
Se crea la función llamada limpieza_datos(), dentro de ella, se utilizan los atributos Datetime, Close y Volume de una copia del dataframe df_bitcoin para realizar los siguientes pasos.

1. Sólo se mantienen indices únicos.
2. Se eliminan valores nulos la columna Close .
3. Se filtran los registros de la base que tienen un Volume de transacción mayor a 0.
4 Se identifican e liminan los outliers en el precio del Bitcoin (columna Close), utilizando un gráfico de boxplot para identificarlos visualmente.
5. Se filtran únicamente los registros cuyo precio(Close) se encuentren entre el 1er cuartil(Q1) y el 3er cuartil(Q3) del boxplot.
6. Finalmente, se calcula el precio promedio(Close) de esta selección y se guarda en la variable media_bitcoin.

### Toma de decisiones ⚖
Se crea una función llamada tomar_decisiones(). dentro de ella se define la variable global algoritmo_decision con el valor resultante del siguiente criterio de decisión:
- Si el precio actual es mayor/igual que el precio promedio y la tendencia es de baja, entonces guarda el valor ‘Vender’.
- Si el precio actual es menor que el precio promedio y la tendencia es de alta, entonces guarda el valor ‘Comprar’.
- Si ninguna de las 2 condiciones anteriores se cumple, entonces guarda el valor 'Esperar'

### Visualización 📊
Se crea una funcion visualizacion(), para mostrar los datos en una gráfica de lineas:

1. Se adiciona una nueva columna (Promedio) al dataframe original df_bitcoiny con el valor de nuestra variable media_bitcoin.
2. Se configura el tamaño del gráfico en una proporción de 16x5.
3. Se adiciona un título al gráfico.
4. Usando el método plot() se dibuja una línea en el gráfico, con los datos del índice y la columna Close de la base df_bitcoin.
5. Usando el método plot() se dibuja una línea en el gráfico, con los datos del índice y la columna Promedio de la base df_bitcoin.
6. Usando el método annotate() se muestra un mensaje dentro del gráfico con la decisión calculada del algoritmo.
7. Finalmente, usando el método show() se muestra en pantalla el gráfico que acabamos de configurar.

### Automatización ⚙
Finalmente con el uso de un loop infinito ppermanentemente y con intervalos de 5minutos, se ejecutan las funciones que se han construído en los pasos 2 al 5.
Con el método 'clear_output()', se borran los resultados de la pantalla antes de imprimir un nuevo gráfico, y así evitar tener más de un gráfico en la pantalla, impórtalo de la siguiente forma: from IPython.display import clear_output.
También se utiliza la biblioteca ‘time’ y su método time.sleep(300) para interrumpir la ejecución del código cada 300 segundos o 5 minutos.

### CRUDE ROBOT TRADING ⛽
Adicinalmente se ha creado el Crude Robot Trading para la toma de decisiones de compra y venta de petróleo crudo.

El Crude Robot Trading tambiel utiliza la biblioteca yfinance de Python como fuente de datos para obtener el histórico de precios del petróleo crudo en dólares por barril USD-BBL de los últimos 7 días en intervalos de 15 minutos, este histórico e guarda en el dataframe df_cl.

Utilizando la biblioteca BeautifulSoup se realiza Web Scraping en la página (https://investing.com/) para extraer el precio actual del petróleo crudo en dólares USD y la variación de su precio en el último día. El precio se convierte atipo float y guarda en la variable llamada precio_actual al igual que el. Finalmete, en la variable tendencia se guarda el valor de 'bajada'si la variación del precio es negativa, sino, guarda el valor de 'subida'.

El resto de los pasos se repite.
