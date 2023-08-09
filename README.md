# Aplicación en Spring
- Se realizó con la versión de Java 17, Java SE 19
- Versión de Spring 3.1.2
- Gradle - Kotlin

Para su ejecución local:
1. Se debe instalar dependencias del "build.gradle"
2. La base de datos está local en: `postgresql://localhost:5432/platzi_market`, importante tener la base de datos y tablas creadas
3. Creamos la aplicación autocontenida: gradle, en la aplicación, Tasks, build y doble clic en bootJar
4. Al terminar el proceso se crea la aplicación en: `platzi-market\build\libs`
5. Para ejecutar la app, desde Bash estando en la carpeta de la app (Apuntando a PDN): `java -jar -Dspring.profiles.active=pdn build/libs/platzi-market-1.0.jar`
6. La documentación con Swagger se puede ver en: http://localhost:8090/platzi-market/api/swagger-ui/index.html