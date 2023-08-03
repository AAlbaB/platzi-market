# Crear un proyecto en Spring

1. Descargar el proyecto inicial, modificando los datos que necesitamos: [Spring Initializr](https://start.spring.io/)
2. Despúes se debe abrir el proyecto descargado con el IDE, en este caso se uso "IntelliJ IDEA" y en las configuraciones se uso: grandle
3. Para los properties se pueden modificar estos atributos: [Documentación Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)
4. Las implementaciones nuevas se colocan en el archivo "build.gradle", se coloca el grupo y el nombre, para finalizar se da en el botón flotante de "Load Grandle Changes". Las dependencias se pueden mirar: [Maven Repository](https://mvnrepository.com/)
5. Para este proyecto se uso "Spring Data" y "Postgresql". La de postgres, se coloca como runtimeOnly
6. Se debe crear la base de datos en Postgres, dentro de la raíz del proyecto se encuentra los archivos .sql para crear las tablas iniciales
7. 