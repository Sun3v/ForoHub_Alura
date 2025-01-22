# ForoHub - Desafío Alura LATAM

ForoHub es una aplicación desarrollada como parte del desafío **Alura LATAM**, cuyo objetivo es construir una plataforma para la gestión y autenticación de usuarios en un foro de discusión. Este proyecto incluye funcionalidades como la creación de usuarios, autenticación mediante tokens JWT y un backend robusto con Spring Boot.

---

## 🚀 Tecnologías utilizadas

- **Java 21** con GraalVM
- **Spring Boot 3.4.0**
  - Spring Data JPA
  - Spring Security
  - Spring Web
- **Hibernate** (ORM)
- **Flyway** (migraciones de base de datos)
- **MySQL 8.0**
- **JWT (JSON Web Tokens)**

---

## ⚙️ Configuración del proyecto

### Requisitos previos

Asegúrate de tener instalados los siguientes programas:

- [Java 21 con GraalVM](https://www.graalvm.org/)
- [MySQL 8.0](https://dev.mysql.com/downloads/mysql/)
- [Maven](https://maven.apache.org/)
- [Postman](https://www.postman.com/) (opcional para pruebas de API)

### Pasos de configuración

1. **Clonar el repositorio:**
   ```bash
   git clone https://github.com/Sun3v/ForoHub_Alura.git
   ```

2. **Crear la base de datos:**

   Ejecuta el siguiente comando en tu servidor MySQL para crear la base de datos:
   ```sql
   CREATE DATABASE forohub;
   ```

3. **Configurar credenciales:**

   Actualiza el archivo `src/main/resources/application.properties` con las credenciales de tu base de datos:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost/${DB_NAME}
   spring.datasource.username=${DB_USER}
   spring.datasource.password=${DB_PASSWORD}
   spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

   spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect
   spring.jpa.open-in-view=false
   spring.jpa.show-sql=false
   spring.jpa.properties.hibernate.format_sql=false

   api.security.secret=${JWT_SECRET}
   ```
   Configura cada parámetro de acuerdo con las necesidades específicas del cliente.

4. **Ejecutar el proyecto:**

   Usa Maven para iniciar la aplicación:
   ```bash
   mvn spring-boot:run
   ```

   La aplicación estará disponible en `http://localhost:8080`.

---

## 🌐 Endpoints principales

### Autenticación

#### `POST /login`
Este endpoint autentica un usuario y devuelve un token JWT.

- **Ejemplo de request:**
  ```bash
  curl -X POST http://localhost:8080/login \
  -H "Content-Type: application/json" \
  -d '{
    "login": "usuario_ejemplo",
    "clave": "123456"
  }'
  ```
- **Ejemplo de respuesta (200 OK):**
  ```json
  {
    "jwToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
  ```

---

### Temas del foro

#### `POST /topicos`
Este endpoint permite crear un nuevo tema en el foro.

- **Ejemplo de request:**
  ```bash
  curl -X POST http://localhost:8080/topicos \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <TOKEN_JWT>" \
  -d '{
    "titulo": "Introducción a Java",
    "mensaje": "Este es un mensaje de prueba que cumple con los requisitos mínimos y máximos de longitud.",
    "status": "Activo",
    "autor": "Cesar Martinez",
    "curso": "Desarrollo de Software"
  }'
  ```

- **Ejemplo de respuesta (201 Created):**
  ```json
  {
    "id": 1,
    "titulo": "Introducción a Java",
    "mensaje": "Este es un mensaje de prueba que cumple con los requisitos mínimos y máximos de longitud.",
    "fechaCreacion": "2025-01-21T19:50:40.3927781",
    "status": "Activo",
    "autor": "Cesar Martinez",
    "curso": "Desarrollo de Software"
  }
  ```

#### `GET /topicos`
Este endpoint devuelve una lista con todos los temas del foro.

- **Ejemplo de request:**
  ```bash
  curl -X GET http://localhost:8080/topicos \
  -H "Authorization: Bearer <TOKEN_JWT>"
  ```

- **Ejemplo de respuesta (200 OK):**
  ```json
  [
    {
      "id": 1,
      "titulo": "Introducción a Java",
      "mensaje": "Este es un mensaje de prueba que cumple con los requisitos mínimos y máximos de longitud.",
      "fechaCreacion": "2025-01-21T19:50:40.3927781",
      "status": "Activo",
      "autor": "Cesar Martinez",
      "curso": "Desarrollo de Software"
    }
  ]
  ```

---

## 🗂 Estructura del proyecto

El proyecto sigue la siguiente organización de directorios:

- **`src/main/java/com/foroHub`**
  - `domain`: Contiene las entidades del modelo.
  - `repository`: Repositorios de JPA.
  - `controller`: Controladores REST.
  - `service`: Lógica de negocio.
  - `config`: Configuraciones de seguridad y JWT.

---

## 🛠 Funcionalidades destacadas

1. **Autenticación JWT:** Gestión de usuarios y generación de tokens JWT para acceso seguro.
2. **Persistencia con JPA:** Uso de Hibernate para interactuar con la base de datos.
3. **Migraciones con Flyway:** Gestión del esquema de la base de datos.
4. **Endpoints RESTful:** Diseño de API para operaciones CRUD.

---

## 🧪 Pruebas

Puedes realizar pruebas de los endpoints utilizando herramientas como:

- **Postman**
- **curl**
- **Insomnia**

Recuerda incluir el token JWT en el encabezado `Authorization` para los endpoints protegidos.

---
