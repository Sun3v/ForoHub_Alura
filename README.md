```markdown
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

### 1. Requisitos previos
Asegúrate de tener instalados:
- [Java 21 con GraalVM](https://www.graalvm.org/)
- [MySQL 8.0](https://dev.mysql.com/downloads/mysql/)
- [Maven](https://maven.apache.org/)
- [Postman](https://www.postman.com/) (opcional para pruebas de API)

### 2. Clonar el repositorio
Clona este proyecto en tu máquina local:
```bash
git clone https://github.com/Sun3v/ForoHub_Alura.git
```

### 3. Configurar la base de datos
1. Crea una base de datos llamada `forohub` en MySQL:
   ```sql
   CREATE DATABASE forohub;
   ```
2. Configura las credenciales de acceso en el archivo `src/main/resources/application.properties`:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/forohub
   spring.datasource.username=tu_usuario
   spring.datasource.password=tu_contraseña
   spring.jpa.hibernate.ddl-auto=none
   spring.flyway.baseline-on-migrate=true
   ```

### 4. Ejecutar las migraciones
Las migraciones de base de datos están gestionadas con Flyway y se aplicarán automáticamente al iniciar la aplicación.

### 5. Ejecutar la aplicación
Ejecuta el proyecto con Maven:
```bash
mvn spring-boot:run
```

La aplicación estará disponible en `http://localhost:8080`.

---

## 🌐 Endpoints principales y requests

### Autenticación
#### `POST /login`
Autentica un usuario y devuelve un token JWT.

- **Request**:
  ```bash
  curl -X POST http://localhost:8080/login \
  -H "Content-Type: application/json" \
  -d '{
    "login": "usuario_ejemplo",
    "clave": "123456"
  }'
  ```
- **Respuesta (200 OK)**:
  ```json
  {
    "jwToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
  ```

---

### Temas del foro
#### `POST /topicos`
Crea un nuevo tema en el foro.

- **Request**:
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
- **Respuesta (201 Created)**:
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
Obtiene una lista de todos los temas del foro. (Requiere autenticación)

- **Request**:
  ```bash
  curl -X GET http://localhost:8080/topicos \
  -H "Authorization: Bearer <TOKEN_JWT>"
  ```

- **Respuesta (200 OK)**:
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

- `src/main/java/com/foroHub`:
  - `domain`: Contiene las entidades del modelo.
  - `repository`: Repositorios de JPA.
  - `controller`: Controladores REST.
  - `service`: Lógica de negocio.
  - `config`: Configuraciones de seguridad y JWT.

---

## 🛠 Funcionalidades destacadas

1. **Autenticación JWT**: Gestión de usuarios y generación de tokens JWT para acceso seguro.
2. **Persistencia con JPA**: Uso de Hibernate para interactuar con la base de datos.
3. **Migraciones con Flyway**: Gestión del esquema de la base de datos.
4. **Endpoints RESTful**: Diseño de API para operaciones CRUD.

---

## 🧪 Pruebas

Puedes realizar pruebas de los endpoints utilizando **Postman**, **curl** o cualquier otra herramienta para pruebas de API. Recuerda incluir el token JWT en el encabezado de las peticiones protegidas.

---
```
