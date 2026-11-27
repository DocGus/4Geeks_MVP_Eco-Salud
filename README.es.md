# SanArte — Eco-Salud

Plataforma web para la gestión de solicitudes, antecedentes médicos y procesos de revisión y validación dentro de un ecosistema de colaboración entre pacientes, estudiantes de ciencias de la salud y profesionales de la salud.

## 📚 Índice

- [Descripción](#descripción)
- [Funcionalidades principales](#funcionalidades-principales)
- [Roles del sistema](#roles-del-sistema)
- [Stack tecnológico](#stack-tecnológico)
- [Requisitos previos](#requisitos-previos)
- [Instalación local](#instalación-local)
- [Configuración de desarrollo local](#configuración-de-desarrollo-local)
- [Ejecutar la aplicación](#ejecutar-la-aplicación)
- [Scripts disponibles](#scripts-disponibles)
- [Base de datos](#base-de-datos)
- [Migraciones](#migraciones)
- [Variables de entorno](#variables-de-entorno)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Requerimientos de lógica de negocio](#requerimientos-de-lógica-de-negocio)
- [Requerimientos técnicos](#requerimientos-técnicos)
- [Desarrollo](#desarrollo)
- [Solución de problemas](#solución-de-problemas)
- [Seguridad](#seguridad)
- [Despliegue](#despliegue)
- [Roadmap técnico](#roadmap-técnico)
- [Autor](#autor)



## Descripción

**SanArte / Eco-Salud** es una aplicación web full-stack orientada a facilitar la recopilación, organización, revisión y validación de información relacionada con antecedentes médicos y procesos de atención colaborativa.

La plataforma contempla diferentes perfiles de usuario y flujos de trabajo que permiten dar seguimiento a solicitudes, documentación médica y procesos de revisión.

### Funcionalidades principales

- Gestión de usuarios y autenticación.
- Dashboards según el rol del usuario.
- Gestión de solicitudes entre pacientes, estudiantes y profesionales.
- Recopilación estructurada de antecedentes médicos.
- Gestión y revisión de información clínica.
- Seguimiento del progreso de solicitudes.
- Revisión y validación de expedientes.
- Manejo de archivos y snapshots de información.
- Confirmación de información por parte del paciente.

### Roles del sistema

- **Paciente:** proporciona información, realiza solicitudes y revisa o confirma su expediente.
- **Estudiante:** gestiona solicitudes asignadas y participa en la recopilación y organización de información.
- **Profesional de la salud:** revisa y valida la información y los expedientes.
- **Administrador:** supervisa la plataforma y gestiona usuarios y procesos.

---

## Stack tecnológico

### Frontend

- React 18
- JavaScript (JSX)
- Vite 4
- React Router DOM 6
- Bootstrap
- React Icons
- HTML2Canvas

### Backend

- Python
- Flask
- Flask-SQLAlchemy
- SQLAlchemy
- Flask-Migrate
- Alembic
- Flask-JWT-Extended
- Flask-CORS

### Base de datos

- SQLite para desarrollo local
- PostgreSQL para entornos configurados con PostgreSQL

### Herramientas

- Git
- Node.js
- npm
- Python virtual environments
- Vite
- Gunicorn

### Servicios opcionales

- Cloudinary para almacenamiento y gestión de archivos multimedia, según la configuración del entorno.

---

## Requisitos previos

Antes de instalar el proyecto, asegúrate de contar con:

| Tecnología | Versión recomendada |
|---|---|
| Git | Versión reciente |
| Python | 3.12 |
| Node.js | 20 o superior |
| npm | Incluido con Node.js |

La instalación y ejecución local documentada se ha probado en Ubuntu con Python 3.12 y Node.js 22.

---

## Instalación local

### 1. Clonar el repositorio

```bash
git clone https://github.com/DocGus/4Geeks_MVP_Eco-Salud.git
```

Entrar al directorio:

```bash
cd 4Geeks_MVP_Eco-Salud
```

### 2. Crear el entorno virtual de Python

```bash
python3 -m venv .venv
```

Activar el entorno virtual:

```bash
source .venv/bin/activate
```

Una vez activado, la terminal mostrará el prefijo `(.venv)`.

### 3. Instalar dependencias del backend

```bash
pip install -r requirements.txt
```

### 4. Configurar variables de entorno

Crear el archivo local de configuración:

```bash
cp .env.example .env
```

Edita `.env` y configura las variables correspondientes a tu entorno.

**No compartas ni subas el archivo `.env` al repositorio.**

### 5. Instalar dependencias del frontend

Desde la raíz del proyecto:

```bash
npm install
```

---

## Configuración de desarrollo local

Para desarrollo local puede utilizarse SQLite, evitando depender de una instancia externa de PostgreSQL.

La aplicación permite seleccionar SQLite mediante la variable:

```bash
FORCE_SQLITE=1
```

La creación automática del esquema en SQLite está controlada por:

```bash
AUTO_CREATE_SCHEMA=1
```

Para las pruebas locales, es posible definir una ruta específica para la base de datos mediante `SQLITE_PATH`.

Ejemplo de base de datos local aislada:

```bash
export FORCE_SQLITE=1
export SQLITE_PATH=/tmp/sanarte-test.db
export AUTO_CREATE_SCHEMA=1
```

> La ruta `/tmp` es apropiada para bases de prueba temporales. Para conservar los datos entre sesiones, utiliza una ruta persistente y asegúrate de que esté excluida del control de versiones.

---

## Ejecutar la aplicación

La aplicación utiliza dos servidores durante el desarrollo: Flask para el backend y Vite para el frontend.

### Terminal 1 — Backend Flask

Desde la raíz del proyecto:

```bash
source .venv/bin/activate
export FORCE_SQLITE=1
export AUTO_CREATE_SCHEMA=1
cd src
flask --app app run --debug
```

Backend disponible en:

**http://127.0.0.1:5000**

Para detener el servidor:

```text
Ctrl + C
```

### Terminal 2 — Frontend React / Vite

Abrir una segunda terminal y regresar a la raíz del proyecto:

```bash
cd 4Geeks_MVP_Eco-Salud
```

Activar el entorno virtual, si se desea mantener la misma sesión de trabajo:

```bash
source .venv/bin/activate
```

Arrancar Vite:

```bash
npm run start
```

Frontend disponible en:

**http://localhost:3000**

### URLs locales

| Servicio | URL |
|---|---|
| Frontend | http://localhost:3000 |
| Backend | http://127.0.0.1:5000 |

Ambos servidores deben permanecer activos mientras se utiliza la aplicación en desarrollo.

---

## Scripts disponibles

### Frontend

| Comando | Descripción |
|---|---|
| `npm run start` | Inicia Vite para desarrollo |
| `npm run dev` | Inicia Vite para desarrollo |
| `npm run build` | Genera el build de producción |
| `npm run preview` | Sirve localmente el build generado |
| `npm run lint` | Ejecuta ESLint |

---

## Base de datos

### SQLite

SQLite puede utilizarse para desarrollo local.

El proyecto permite configurar la base de datos mediante variables de entorno:

```env
FORCE_SQLITE=1
AUTO_CREATE_SCHEMA=1
```

Si no se especifica `SQLITE_PATH`, la aplicación utiliza su ruta SQLite predeterminada.

### PostgreSQL

Para los entornos que utilizan PostgreSQL, debe configurarse `DATABASE_URL` con la cadena de conexión correspondiente.

Ejemplo:

```env
DATABASE_URL=postgresql://usuario:contraseña@localhost:5432/nombre_db
```

No utilices credenciales reales en archivos versionados ni en documentación pública.

---

## Migraciones

El proyecto utiliza Flask-Migrate y Alembic para administrar cambios en la estructura de la base de datos.

Los comandos habituales son:

```bash
flask db migrate
```

Generar una migración a partir de cambios detectados en los modelos.

```bash
flask db upgrade
```

Aplicar las migraciones pendientes.

Antes de ejecutar migraciones sobre una base de datos existente, verifica siempre el entorno y la conexión activa.

---

## Variables de entorno

Las variables pueden variar según el entorno.

| Variable | Descripción |
|---|---|
| `DATABASE_URL` | Cadena de conexión de base de datos |
| `TEST_DB_URL` | Conexión utilizada para pruebas, si está configurada |
| `FORCE_SQLITE` | Fuerza el uso de SQLite (`1` para activar) |
| `SQLITE_PATH` | Ruta personalizada de la base SQLite |
| `AUTO_CREATE_SCHEMA` | Permite la creación automática del esquema SQLite |
| `FLASK_DEBUG` | Activa o desactiva el modo de desarrollo |
| `JWT_SECRET_KEY` | Clave de firma JWT |
| `FLASK_SECRET_KEY` / `FLASK_APP_KEY` | Claves utilizadas por Flask según la configuración |
| `CLOUDINARY_URL` | URL de configuración de Cloudinary |
| `CLOUDINARY_CLOUD_NAME` | Nombre del cloud de Cloudinary |
| `CLOUDINARY_API_KEY` | API Key de Cloudinary |
| `CLOUDINARY_API_SECRET` | API Secret de Cloudinary |
| `MIGRATE_ON_START` | Control de migración automática de datos legacy |
| `MIGRATE_FROM_URL` | Fuente de datos para migración legacy |
| `VITE_BACKEND_URL` | URL del backend consumida por el frontend |
| `VITE_BASENAME` | Base path del frontend |

---

## Estructura del proyecto

```text
4Geeks_MVP_Eco-Salud/
│
├── src/
│   ├── app.py
│   ├── wsgi.py
│   │
│   ├── api/
│   │   ├── models.py
│   │   ├── routes.py
│   │   ├── utils.py
│   │   ├── admin.py
│   │   └── commands.py
│   │
│   └── front/
│       ├── main.jsx
│       ├── routes.jsx
│       ├── store.js
│       ├── components/
│       └── pages/
│
├── migrations/
├── docs/
├── public/
├── requirements.txt
├── package.json
├── package-lock.json
├── Pipfile
├── Pipfile.lock
├── .env.example
├── render.yaml
├── Dockerfile.render
├── render_build.sh
└── README.md
```

---

## Requerimientos de lógica de negocio

Esta sección documenta las reglas, comportamientos, roles y procesos que definen el funcionamiento de SanArte / Eco-Salud. Su objetivo es mantener una referencia clara de las decisiones de negocio y de los flujos funcionales de la plataforma.

### Gestión de usuarios y roles

La plataforma contempla diferentes perfiles de usuario, cada uno con responsabilidades y permisos diferenciados dentro del ecosistema:

- **Paciente:** proporciona información, realiza solicitudes y participa en la revisión y confirmación de su información.
- **Estudiante:** participa en la gestión de solicitudes y en la recopilación y organización de información.
- **Profesional de la salud:** revisa y valida información y expedientes.
- **Administrador:** gestiona usuarios, supervisa la plataforma y participa en la administración de los procesos del sistema.

### Registro y administración de usuarios

- Cada usuario debe contar con un registro individual dentro de la plataforma.
- El correo electrónico debe ser único para identificar la cuenta.
- El usuario debe contar con un rol definido.
- El usuario puede tener un estado que determine su condición dentro de la plataforma, por ejemplo, pendiente de aprobación o aprobado.
- La asignación de roles y estados debe ser consistente con los permisos y procesos definidos para cada perfil.

### Inicialización de la administración de la plataforma

Para comenzar a operar y administrar la plataforma, se requiere contar con un usuario administrador.

El primer administrador permite iniciar las tareas de gestión y supervisión de usuarios y procesos desde las herramientas administrativas disponibles.

Durante las pruebas de desarrollo se realizó la creación del primer usuario administrador utilizando el panel Flask-Admin.

Consideraciones:

- El usuario administrador debe contar con el rol correspondiente.
- Su estado debe permitir el acceso a las funcionalidades administrativas.
- Su correo debe ser único.
- La creación de administradores debe realizarse de manera controlada.
- Las credenciales utilizadas en pruebas deben ser diferentes de las credenciales de producción.

### Consideraciones de negocio pendientes de consolidación

Esta sección se actualizará conforme se validen las reglas de negocio definitivas relacionadas con:

- Flujo de aprobación de usuarios.
- Permisos específicos por rol.
- Asignación y seguimiento de solicitudes.
- Validación y confirmación de expedientes.
- Transiciones entre estados de solicitudes.
- Restricciones de acceso a información.
- Reglas de colaboración entre pacientes, estudiantes y profesionales de la salud.

---

## Requerimientos técnicos

Esta sección documenta el comportamiento técnico de la aplicación, su arquitectura, configuración, componentes y los descubrimientos realizados durante el desarrollo y depuración.

### Arquitectura general

SanArte / Eco-Salud utiliza una arquitectura full-stack compuesta por:

- **Frontend:** React y Vite.
- **Backend:** Python y Flask.
- **Base de datos:** SQLite para pruebas locales y PostgreSQL para entornos configurados con este motor.
- **Administración:** Flask-Admin para la gestión de registros y usuarios.
- **Autenticación:** mecanismos implementados en el backend y manejo de tokens según la configuración del proyecto.

Durante el desarrollo local, frontend y backend se ejecutan de manera independiente.

### Backend y administración

El backend utiliza Flask para gestionar la aplicación, sus endpoints, configuración y componentes administrativos.

Flask-Admin permite acceder a una interfaz de administración para gestionar registros de los modelos configurados, incluidos los usuarios.

La ruta local del panel administrativo durante el desarrollo es:

`http://localhost:5000/admin/`

### Configuración de sesiones y SECRET_KEY

Flask requiere una clave secreta (`secret_key`) para determinadas funcionalidades relacionadas con sesiones y protección de información de sesión.

Durante las pruebas de creación de usuarios en Flask-Admin se identificó un problema de configuración:

- `app.py` configuraba la clave secreta de la aplicación.
- `api/admin.py`, durante la inicialización de Flask-Admin, sobrescribía dicha clave.
- La variable de entorno `FLASK_APP_KEY` podía existir con un valor vacío.
- Cuando la variable estaba vacía, la asignación podía dejar `app.secret_key` sin una clave válida.
- El registro del usuario podía guardarse en la base de datos, pero posteriormente Flask-Admin fallaba al intentar mostrar el mensaje de confirmación mediante el sistema de sesiones y mensajes Flash.

### Solución aplicada

Se eliminó la asignación redundante de `app.secret_key` dentro de la configuración de Flask-Admin.

La configuración principal de la clave secreta permanece bajo la responsabilidad de `app.py`, evitando que otro módulo sobrescriba accidentalmente la configuración de sesiones de Flask.

**Principio técnico aprendido:** la configuración central de la aplicación debe tener una única fuente de responsabilidad. Los módulos que integran funcionalidades adicionales no deben sobrescribir configuraciones globales sin una necesidad explícita.

### Base de datos para pruebas locales

Durante las pruebas de desarrollo se utilizó SQLite con una base de datos aislada:

`/tmp/sanarte-test.db`

Configuración utilizada:

```bash
export FORCE_SQLITE=1
export SQLITE_PATH=/tmp/sanarte-test.db
export AUTO_CREATE_SCHEMA=1
---

## Desarrollo

### Frontend

El frontend utiliza React y Vite.

Durante el desarrollo, Vite proporciona recarga automática de los cambios.

```bash
npm run start
```

### Backend

El backend utiliza Flask para exponer endpoints y gestionar la lógica de la aplicación.

```bash
source .venv/bin/activate
cd src
flask --app app run --debug
```

---

## Solución de problemas

### El frontend no carga

Verifica que Vite esté activo:

```bash
npm run start
```

Comprueba la dirección:

```text
http://localhost:3000
```

### El backend no carga

Verifica que el entorno virtual esté activado:

```bash
source .venv/bin/activate
```

Después inicia Flask:

```bash
cd src
flask --app app run --debug
```

### Error de conexión con la base de datos

Verifica:

- El valor de `DATABASE_URL`.
- La variable `FORCE_SQLITE`.
- La ruta configurada en `SQLITE_PATH`.
- Que la base de datos corresponda al entorno de desarrollo.

### Cambios de configuración no reflejados

Después de cambiar variables de entorno, detén y reinicia el servidor correspondiente.

---

## Seguridad

- No subir archivos `.env` al repositorio.
- No incluir claves JWT reales en el código.
- No publicar credenciales de PostgreSQL.
- No utilizar bases de datos de producción durante pruebas locales.
- Revisar la configuración de CORS antes de desplegar.
- Validar permisos y acceso a endpoints.
- Utilizar HTTPS en producción.
- Mantener copias de respaldo de la base de datos.
- Revisar los límites y validaciones de carga de archivos.

---

## Despliegue

El repositorio contiene archivos de configuración relacionados con despliegue, incluyendo:

- `render.yaml`
- `Dockerfile.render`
- `render_build.sh`
- `Procfile`

La configuración de producción debe utilizar variables de entorno seguras, una base de datos persistente y una estrategia de migraciones controlada.

La configuración de desarrollo local no debe utilizarse directamente como configuración de producción.

---

## Roadmap técnico

- [ ] Consolidar y documentar variables de entorno.
- [ ] Crear una guía de desarrollo ampliada.
- [ ] Implementar pruebas automatizadas del backend.
- [ ] Implementar pruebas End-to-End.
- [ ] Integrar CI/CD.
- [ ] Revisar validación de formularios y archivos.
- [ ] Mejorar observabilidad y logging.
- [ ] Documentar los endpoints de la API.
- [ ] Revisar configuración de seguridad de producción.
- [ ] Mejorar documentación de arquitectura.

---

## Autor

**Gustavo Andrés Santoyo Benavides — DocGus**

Proyecto desarrollado dentro de la iniciativa Eco-Salud, combinando experiencia clínica y desarrollo tecnológico para facilitar procesos de gestión y colaboración en salud.

---

> SanArte / Eco-Salud — Tecnología para conectar, organizar y facilitar procesos de salud.
