# Crear un proyecto en Spring

1. Descargar el proyecto inicial, modificando los datos que necesitamos: [Spring Initializr](https://start.spring.io/)
2. Despúes se debe abrir el proyecto descargado con el IDE, en este caso se uso "IntelliJ IDEA" y en las configuraciones se uso: grandle
3. Para los properties se pueden modificar estos atributos: [Documentación Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)
4. Las implementaciones nuevas se colocan en el archivo "build.gradle", se coloca el grupo y el nombre, para finalizar se da en el botón flotante de "Load Grandle Changes". Las dependencias se pueden mirar: [Maven Repository](https://mvnrepository.com/)
5. Para este proyecto se uso "Spring Data" y "Postgresql". La de postgres, se coloca como runtimeOnly
6. Se debe crear la base de datos en Postgres, dentro de la raíz del proyecto se encuentra los archivos .sql para crear las tablas iniciales
7. Se crea las entidades de base de datos en la carpeta persistence/entity, para tener en cuenta:
   - Siempre se debe colocar la notación **@Entity**, para dar a entender a JAVA que esta clase mapea una tabla en BD
   - La notació **@Table**, para colocar el nombre real de la tabla en BD
   - La notación **@Column**, para colocar el nombre real de la columna en BD
   - La notación **@ID**, es para asignar que es la llave primaria de la tabla y **@GeneratedValue**, que se generará automaticamente
   - Para generar los getter and setter, clic derecho, Generete, "Getter and Setter", seleccionarlos todos y Ok.
   - La notación **@EmbeddedId**, se utiliza para clave primaria compuesta y esta dada por otra clase 
   - La notación **@ManyToOne**, relación de muchos a uno
   - La notación **@JoinColumn**, para unir las tablas por el id
   - La notación **@OneToMany**, relación de uno a muchos
   - La notación **@Repository**, para decirle a Spring que esa clase interactua con BD
   - La notación **@Component**, para indicar que es un componente de Spring
8. En este proyecto se uso "Crud Repository", para la creación CRUD de las entidades mediante interfaces
9. Se utilizó también "Query Methods" para las consultas en BD, mas info: [Query Methods](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods)
10. 