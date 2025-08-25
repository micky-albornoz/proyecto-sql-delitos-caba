# Análisis de la actividad delictiva en la Ciudad de Buenos Aires (2024)

### Descripción del proyecto

Este proyecto realiza un análisis exploratorio de datos (EDA) sobre los delitos registrados en la Ciudad Autónoma de Buenos Aires durante el año 2024. Utilizando un conjunto de datos público, se busca identificar patrones y tendencias clave en la actividad delictiva a través de consultas SQL y visualizaciones geoespaciales interactivas.

El entorno de desarrollo se configuró completamente en la nube utilizando **GitHub Codespaces**, lo que garantiza la total reproducibilidad del análisis.

**Tecnologías utilizadas:**

* **Lenguajes:** Python, SQL
* **Bases de Datos:** PostgreSQL
* **Librerías Principales:** Pandas (manipulación de datos), SQLAlchemy (conexión a la BD), `ipython-sql` (ejecución de SQL en notebook), Folium (visualización geoespacial), `python-dotenv` (manejo seguro de credenciales).
* **Entorno:** Jupyter Notebook en GitHub Codespaces.

### Dataset

El conjunto de datos utilizado es el de **"Delitos registrados por mes, barrio y tipo de delito"** correspondiente al año 2024, obtenido del portal de datos abiertos del Gobierno de la Ciudad de Buenos Aires: [data.buenosaires.gob.ar](https://data.buenosaires.gob.ar/).

El dataset contiene información detallada de cada incidente, incluyendo:

* Fecha y franja horaria.
* Tipo y subtipo de delito.
* Indicadores de uso de arma y/o moto.
* Ubicación geográfica precisa (barrio, comuna, latitud y longitud).

### Preguntas de análisis

Para guiar la exploración, se plantearon las siguientes preguntas, respondidas mediante consultas directas a la base de datos PostgreSQL:

1.  ¿Cuáles son los 10 barrios con la mayor cantidad de delitos registrados?
2.  ¿Cómo se distribuyen los delitos a lo largo de los días de la semana?
3.  ¿En qué franjas horarias se concentra la mayor actividad delictiva?
4.  ¿Cuáles son los subtipos de delito más comunes en la ciudad?
5.  ¿Qué porcentaje de los delitos involucra el uso de un arma?
6.  ¿En qué comunas es más frecuente el uso de motos para cometer delitos?
7.  ¿Cómo ha sido la evolución mensual de la cantidad de delitos durante el año?
8.  ¿Cuáles son los 5 delitos más frecuentes en la Comuna 1, una de las zonas con mayor actividad?
9.  ¿Cuál es la proporción entre Robos y Hurtos en la ciudad?
10. ¿Cuáles son los barrios con mayor actividad delictiva en horario nocturno (entre las 20:00 y las 06:00)?

### Principales hallazgos

Del análisis de los datos se desprenden las siguientes conclusiones clave:

* **Concentración geográfica:** Existe una alta concentración de delitos en barrios céntricos y de gran afluencia como Palermo, Balvanera y Recoleta, lo que se evidencia tanto en los conteos totales como en los mapas de calor.
* **Patrones temporales:** La actividad delictiva muestra picos durante los días de semana en horarios vespertinos (entre las 17:00 y las 20:00), coincidiendo con el fin de la jornada laboral. Los fines de semana presentan una dinámica diferente, con un aumento de incidentes en horarios nocturnos.
* **Tipología del delito:** El **"Hurto (sin violencia)"** es el subtipo de delito más reportado, seguido por el **"Robo (con violencia)"**. Esto sugiere que una gran parte de los incidentes son oportunistas y no necesariamente violentos.
* **Uso de medios:** Aunque el porcentaje de delitos con uso de arma es minoritario, su impacto es significativo. El uso de motos se concentra en comunas específicas, indicando un *modus operandi* particular en ciertas zonas.
* **Zonas críticas nocturnas:** El análisis nocturno revela que barrios como Palermo mantienen una alta tasa delictiva, probablemente asociada a su vida nocturna y zonas de ocio.

### Visualizaciones

Para complementar el análisis SQL, se generaron dos tipos de mapas interactivos utilizando la librería Folium:

1.  **Mapa de clústeres:** Permite explorar la distribución de los delitos de forma agrupada. Al hacer zoom, los clústeres se expanden para revelar la ubicación de incidentes individuales.
2.  **Mapa de calor (Heatmap):** Ofrece una visión clara e inmediata de las "zonas calientes" o áreas de mayor concentración de delitos en la ciudad, destacando visualmente las áreas que requieren mayor atención.

![Mapa de delitos clusters](https://github.com/micky-albornoz/proyecto-sql-delitos-caba/blob/main/images/mapa_delitos_clusters.png)
![Mapa de delitos calor](https://github.com/micky-albornoz/proyecto-sql-delitos-caba/blob/main/images/mapa_delitos_calor.png)

---

### ¿Cómo replicar este proyecto?

Puedes replicar este análisis utilizando **GitHub Codespaces** (recomendado) o configurando el entorno en tu máquina local (Debian/Ubuntu).

#### Opción 1: Usando GitHub Codespaces (Recomendado)

1.  **Abrir en Codespaces:** Haz clic en el botón `Code` en la página principal del repositorio y selecciona `Create a codespace on main`. Esto abrirá un entorno de desarrollo completo en tu navegador.

2.  **Configurar la Base de datos:** Abre una terminal dentro de Codespaces (`Ctrl+Shift+ñ` o `Terminal > New Terminal`) y ejecuta los siguientes comandos para crear la base de datos y el usuario:
    ```bash
    # Acceder a la consola de PostgreSQL
    sudo -u postgres psql

    # Dentro de psql, ejecuta los siguientes comandos SQL:
    CREATE DATABASE delitos_db;
    CREATE USER user_delitos WITH PASSWORD 'tu_contraseña_segura';
    GRANT ALL PRIVILEGES ON DATABASE delitos_db TO user_delitos;

    # Salir de psql
    \q
    ```

3.  **Crear el archivo de entorno:** En la raíz del proyecto, crea un archivo llamado `.env` y añade tus credenciales. **Este archivo no debe ser subido a GitHub.**
    ```env
    DB_USER="user_delitos"
    DB_PASSWORD="tu_contraseña_segura"
    ```

4.  **Ejecutar el Notebook:** Abre el archivo `analisis_delitos.ipynb` y ejecuta todas las celdas en orden. El entorno de Codespaces ya habrá instalado las dependencias de Python del archivo `requirements.txt`.

#### Opción 2: Configuración local (Debian/Ubuntu)

1.  **Clonar el repositorio:**
    ```bash
    git clone [https://github.com/micky-albornoz/proyecto-sql-delitos-caba.git](https://github.com/micky-albornoz/proyecto-sql-delitos-caba.git)
    cd proyecto-sql-delitos-caba
    ```

2.  **Instalar PostgreSQL:**
    ```bash
    sudo apt-get update
    sudo apt-get install -y postgresql postgresql-contrib
    sudo service postgresql start
    ```

3.  **Configurar la Base de Datos:**
    ```bash
    # Acceder como superusuario de postgres y abrir la consola psql
    sudo -u postgres psql
    ```
    Una vez dentro de la consola `psql`, ejecuta los siguientes comandos:
    ```sql
    CREATE DATABASE delitos_db;
    CREATE USER user_delitos WITH PASSWORD 'tu_contraseña_segura';
    GRANT ALL PRIVILEGES ON DATABASE delitos_db TO user_delitos;
    \q
    ```

4.  **Instalar dependencias de Python:** (Se recomienda usar un entorno virtual)
    ```bash
    # Crear y activar un entorno virtual
    python3 -m venv venv
    source venv/bin/activate

    # Instalar todas las librerías desde el archivo de requerimientos
    pip install -r requirements.txt
    ```

5.  **Configurar credenciales:** Crea un archivo `.env` en la raíz del proyecto con el siguiente contenido:
    ```env
    DB_USER="user_delitos"
    DB_PASSWORD="tu_contraseña_segura"
    ```

6.  **Ejecutar el Notebook:** Inicia Jupyter Notebook y abre el archivo `analisis_delitos.ipynb`.
    ```bash
    jupyter notebook
    ```
