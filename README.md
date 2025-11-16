# Spring Boot Minimal + MySQL Docker

## 🚀 Ejecución rápida

1. Levantar la base de datos MySQL con Docker Compose:

```bash
docker compose up -d
```

2. Ejecutar la aplicación Spring Boot en tu IDE (por ejemplo, IntelliJ IDEA o Eclipse).

Accede a la aplicación en: [http://localhost:8080](http://localhost:8080)

Base de datos MySQL en el puerto **3306** con usuario `spring` / password `spring`.

- Usuario `root` con password `root`

```sql
mysql -h 127.0.0.1 -u spring -p
```

- Detener la base de datos:

```bash
docker compose down
```

- Logs de MySQL:

```bash
docker compose logs -f mysql
```

- Verificar con curl:

```bash
curl http://localhost:8080/api/clientes
```

## 🧹 Limpieza de contenedores

Para purgar y limpiar los contenedores, imágenes y volúmenes no utilizados:

- Detener y eliminar contenedores del proyecto:

```bash
docker compose down -v
```

- Purgar contenedores detenidos:

```bash
docker container prune -f
```

- Purgar imágenes no utilizadas:

```bash
docker image prune -a -f
```

- Purgar volúmenes no utilizados:

```bash
docker volume prune -f
```

- Limpieza completa del sistema Docker:

```bash
docker system prune -a -f
```

## 🔄 Cambiar el nombre de la base de datos

Para cambiar el nombre de la base de datos (por defecto `pedidosdb`):

1. **Actualizar `docker-compose.yml`**:
   - Cambia el valor de `MYSQL_DATABASE` en el servicio `mysql` al nuevo nombre, por ejemplo `MYSQL_DATABASE: nuevadb`.

2. **Actualizar `src/main/resources/application.properties`**:
   - Cambia la URL en `spring.datasource.url` para usar el nuevo nombre, por ejemplo `jdbc:mysql://localhost:3306/nuevadb?useSSL=false&allowPublicKeyRetrieval=true&createDatabaseIfNotExist=true`.

3. **Actualizar el script de inicialización `mysql/init/01-init.sql`**:
   - Cambia `CREATE DATABASE IF NOT EXISTS pedidosdb;` a `CREATE DATABASE IF NOT EXISTS nuevadb;`.
   - Cambia `USE pedidosdb;` a `USE nuevadb;`.

4. **Reiniciar los contenedores**:
   - Detén y elimina los contenedores existentes: `docker compose down -v`.
   - Levanta nuevamente: `docker compose up -d`.

Nota: Si ya hay datos en la base de datos, asegúrate de hacer una copia de seguridad antes de cambiar el nombre, ya que esto creará una nueva base de datos.
