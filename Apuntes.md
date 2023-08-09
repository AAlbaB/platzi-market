# Crear un proyecto en Spring

1. Descargar el proyecto inicial, modificando los datos que necesitamos: [Spring Initializr](https://start.spring.io/)
2. Después se debe abrir el proyecto descargado con el IDE, en este caso se usó "IntelliJ IDEA" y en las configuraciones se usó: grandle
3. Para los properties se pueden modificar estos atributos: [Documentación Properties](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html)
4. Las implementaciones nuevas se colocan en el archivo "build.gradle", se coloca el grupo y el nombre, para finalizar se da en el botón flotante de "Load Grandle Changes". Las dependencias se pueden mirar: [Maven Repository](https://mvnrepository.com/)
5. Para este proyecto se usó "Spring Data" y "Postgresql". La de postgres, se coloca como runtimeOnly
6. Se debe crear la base de datos en Postgres, dentro de la raíz del proyecto se encuentra los archivos .sql para crear las tablas iniciales
7. Se crea las entidades de base de datos en la carpeta persistence/entity, para tener en cuenta:
   - Siempre se debe colocar la notación **@Entity**, para dar a entender a JAVA que esta clase mapea una tabla en BD
   - La notación **@Table**, para colocar el nombre real de la tabla en BD
   - La notación **@Column**, para colocar el nombre real de la columna en BD
   - La notación **@Id**, es para asignar que es la llave primaria de la tabla y **@GeneratedValue**, que se generará automáticamente
   - Para generar los getter and setter, clic derecho, "Generete", "Getter and Setter", seleccionarlos todos y Ok.
   - La notación **@EmbeddedId**, se utiliza para clave primaria compuesta y está dada por otra clase 
   - La notación **@ManyToOne**, relación de muchos a uno
   - La notación **@JoinColumn**, para unir las tablas por él, id
   - La notación **@OneToMany**, relación de uno a muchos
   - La notación **@Repository**, para decirle a Spring que esa clase interactúa con BD
   - La notación **@Component**, para indicar que es un componente de Spring
8. En este proyecto se usó "Crud Repository", para la creación CRUD de las entidades mediante interfaces, se crean en "persistence.crud"
9. Se utilizó también "Query Methods" para las consultas en BD, más info: [Query Methods](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods), se crean en persistence
10. Para implementar el patron "Data Mapper", lo usamos con "Map Struct": [Mapstruct](https://mapstruct.org/documentation/installation/), se debe colocar en el build.gradle e instalar el Plugin “MapStruct Support”
11. En la carpeta "domain", se crea las clases para el patrón de data mapper
12. Se crea el repositorio en "domain.repository", esto se hace con el fin de que lo creado en persistence no se comunique directamente con la API, sino con el dominio
13. Se hace los mapeadores en "persistence.mapper", los que traducen las clases del dominio y persistencia
    - Se coloca la notación **@Mapper** para indicar al proyecto que es un mapper, se coloca el "componentModel" en spring y se coloca "uses" cuando ya se está usando otra mapper interno, ejemplo: categoria en product
    - La notación **@Mappings** se colocan los **@Mappings**, se coloca desde donde hasta donde se va a llevar
    - La notación **@InheritInverseConfiguration** es para indicarle que se hará el mapeo contrario al mappings anterior
    - Si no quiero mapear algo colocamos **@Mapping(target = "Campo a ignorar", ignore = true)**
14. Ahora orientamos los "Repository" (Los que están en persistence) al dominio "ProductoRepository". Le colocamos el "implements ProductRepository"
    - En este punto se heredan los métodos del dominio, y se deben ajustar a lo que piden el dominio
    - La notación **@Override** significa que viene heredado de la implementación del dominio
    - Se pueden ir borrando los métodos iniciales e ir dejando solo los heredados
    - Al terminar el "ProductoRepository" queda enfocado al dominio en lugar de la tabla puntual
    - Esto evita que el proyecto se acople a una BD puntual, por ejemplo si se utiliza otro tipo de base de datos, solo se tendría que crear otro tipo mapper que convierta "Product" en la nueva colección
15. Debemos colocar la notación **@Autowired** (En los Repository de persistence) cuando se inicializa el mapper y el Crud repository en "ProductoRepository" de la persistencia. Se le da a entender a Spring que los objetos que reciban esta notación les debe crear las instancias, con esto ya no tenemos que crear objetos manualmente. Se debe tener cuidado de autowired, el objeto a inyectar es un objeto de spring, o sea, que tenga el componenteModel en spring. Con esto se finaliza los repositorios.
16. Ahora crearemos los servicios en "domain.service", como clases:
    - Se le debe colocar la notación **@Service**
    - Se implementa la interfaz
17. Creamos los controladores de REST en "web.controller", como clases:
    - Se le debe colocar la notación **@RestController**, para indicar que esta clase será el controlador de una API REST
    - También la notación **@RequestMapping**, para indicar que petición o path va a aceptar las peticiones que se le hagan
    - Los métodos deben tener las notaciones para ser accedidos: **@GetMapping**, para tipo get
    - La notación **@PathVariable**, para pasarle una variable desde la petición
    - La notación **@PostMapping**, para peticiones tipo post
    - La notación **@RequestBody**, para indicarle que vendrá algo por medio del body
    - La notación **@DeleteMapping**, para peticiones tipo delete
18. Para documentar nuestra API con Swagger, primero debemos añadir la dependencia en "build.grandle", buscamos: "SpringFox Swagger2" y "SpringFox Swagger UI", se agregaron:
    - implementation 'io.springfox:springfox-swagger2:3.0.0'
    - implementation 'io.springfox:springfox-swagger-ui:3.0.0'
    - implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.1.0'
    - springdoc.swagger-ui.path=/swagger-ui.html, se agrego en el application.properties
19. Creamos la clase de Java "SwaggerConfig" en "web.config", dentro de los controladores podemos colocar las notaciones **@Operation**, **@ApiResponse** y **@ApiParam**, para dar más detalle. Ver (https://springdoc.org/ Revisar más a fondo estas implementaciones y notaciones)
20. La documentación queda en: http://localhost:8090/platzi-market/api/swagger-ui/index.html
21. Para desplegar nuestra aplicación por comandos:
    - Vamos a "build.grandle" y cambiamos el número de versión que vayamos a usar y actualizamos los cambios de gradle (Botón flotante)
    - Al lado derecho damos en gradle, en la aplicación, Tasks, build y doble clic en bootJar, con esto generamos nuestra aplicación autocontenida
    - Al terminar el proceso se crea la aplicación en: "platzi-market\build\libs"
    - Para ejecutar la app, desde Bash estando en la carpeta de la app (Apuntando en PDN): `java -jar -Dspring.profiles.active=pdn build/libs/platzi-market-1.0.jar`
22. Para el despliegue en Heroku (Revisar en las demás):
    - En el archivo: "application-pdn.properties", se colocan las variables de entorno asignadas para el puerto y la BD (Se dejaron comentadas)
    - Se creó el archivo "system.properties" en la raíz del proyecto para indicar la versión de Java a ejecutar
    - Se creó el archivo "Procfile" en la raíz del proyecto para indicar el perfil a ejecutar

## Update
- En el paso 14, al implementar los repositorios del dominio, aparece una sugerencia de implementar los métodos de esa interfaz. Pero es importante colocar la notación: **@Repository**
- Luego hacemos el crud en "Persistence.crud". Ya con el crud creado, se le coloca en el repository con la notación **@Autowired** y se termina el código de los métodos