# Proyecto SQL con PostgreSQL y pgAdmin

Este proyecto proporciona un entorno de desarrollo completo para trabajar con bases de datos PostgreSQL utilizando Docker Compose, incluyendo pgAdmin como interfaz de administración web.

## 🚀 Componentes del Proyecto

### Base de Datos PostgreSQL

- **Imagen**: `postgres:15.3`
- **Puerto**: `5432`
- **Base de datos**: `course-db`
- **Usuario**: `alumno`
- **Contraseña**: `123456`

### pgAdmin (Interfaz Web)

- **Imagen**: `dpage/pgadmin4`
- **Puerto**: `8080`
- **Email**: `alumno@google.com`
- **Contraseña**: `123456`

## 📋 Prerrequisitos

- [Docker](https://www.docker.com/get-started) instalado
- [Docker Compose](https://docs.docker.com/compose/install/) instalado

## 🛠️ Instalación y Uso

### 1. Clonar o descargar el proyecto

```bash
git clone <tu-repositorio>
cd SQL
```

### 2. Levantar los servicios

```bash
docker-compose up -d
```

### 3. Verificar que los contenedores están ejecutándose

```bash
docker-compose ps
```

### 4. Acceder a pgAdmin

1. Abrir navegador web
2. Ir a: `http://localhost:8080`
3. Iniciar sesión con:
   - **Email**: `alumno@google.com`
   - **Contraseña**: `123456`

### 5. Conectar pgAdmin a PostgreSQL

Una vez dentro de pgAdmin:

1. Click derecho en "Servers" → "Register" → "Server"
2. En la pestaña "General":
   - **Name**: `course-db` (o el nombre que prefieras)
3. En la pestaña "Connection":
   - **Host name/address**: `myDB` (nombre del servicio en Docker)
   - **Port**: `5432`
   - **Username**: `alumno`
   - **Password**: `123456`
4. Click "Save"

## 🗄️ Estructura del Proyecto

```
SQL/
├── docker-compose.yml          # Configuración de Docker Compose
├── .gitignore                  # Archivos a ignorar en Git
├── README.md                   # Este archivo
├── postgres/                   # Datos persistentes de PostgreSQL (ignorado en Git)
└── pgadmin/                    # Datos persistentes de pgAdmin (ignorado en Git)
```

## 🔧 Comandos Útiles

### Gestión de Contenedores

```bash
# Levantar servicios
docker-compose up -d

# Ver logs
docker-compose logs

# Ver logs de un servicio específico
docker-compose logs myDB
docker-compose logs pdAdmin

# Parar servicios
docker-compose stop

# Parar y eliminar contenedores
docker-compose down

# Parar y eliminar contenedores + volúmenes (¡CUIDADO: elimina datos!)
docker-compose down -v
```

### Conexión Directa a PostgreSQL

```bash
# Conectar via psql desde línea de comandos
docker exec -it my-database psql -U alumno -d course-db

# Backup de la base de datos
docker exec my-database pg_dump -U alumno course-db > backup.sql

# Restaurar backup
docker exec -i my-database psql -U alumno course-db < backup.sql
```

## 🌐 URLs de Acceso

- **pgAdmin**: http://localhost:8080
- **PostgreSQL**: localhost:5432 (para conexiones desde aplicaciones externas)

## 📁 Persistencia de Datos

Los datos se almacenan en carpetas locales que se montan como volúmenes:

- `./postgres/`: Datos de la base de datos PostgreSQL
- `./pgadmin/`: Configuraciones y sesiones de pgAdmin

**Nota**: Estas carpetas están incluidas en `.gitignore` para evitar subir datos sensibles al repositorio.

## ⚠️ Consideraciones de Seguridad

**Para desarrollo local únicamente**. En producción:

- Cambiar las contraseñas por defecto
- Usar variables de entorno para credenciales
- Configurar SSL/TLS
- Restringir acceso a puertos

## 🤝 Contribuir

1. Fork el proyecto
2. Crear una rama para tu feature (`git checkout -b feature/nueva-funcionalidad`)
3. Commit tus cambios (`git commit -am 'Agregar nueva funcionalidad'`)
4. Push a la rama (`git push origin feature/nueva-funcionalidad`)
5. Crear un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para detalles.

---

**¡Happy coding! 🎉**
