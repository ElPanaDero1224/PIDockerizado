# Usa la imagen oficial de Python
FROM mcr.microsoft.com/mssql/server:2022-latest

# Establece variables de entorno necesarias para SQL Server
ENV SA_PASSWORD=UnaContraseñaMuyDifícil123!
ENV ACCEPT_EULA=Y

# Copia el script de inicialización
COPY ./init-db /docker-entrypoint-initdb.d

# Exponer el puerto de SQL Server
EXPOSE 1433

# Comando para iniciar SQL Server
CMD /opt/mssql/bin/sqlservr



FROM python:3.12-slim

# Establece el directorio de trabajo
WORKDIR /app

# Copia el archivo requirements.txt y lo instala



RUN apt-get update && apt-get install -y \
    unixodbc-dev \
    curl \
    apt-transport-https \
    gnupg \
    netcat-openbsd

RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list && \
    apt-get update && \
    ACCEPT_EULA=Y apt-get install -y msodbcsql17

# Copia el contenido del directorio actual en el contenedor
COPY . .

RUN pip install --no-cache-dir -r requirements.txt





# Exponer el puerto que tu aplicación usa
EXPOSE 5000

# Comando para iniciar tu aplicación
CMD ["python", "app.py"]