# 🧾 Assets DB Setup — PostgreSQL

Este proyecto contiene una base de datos de prueba para simular operaciones de cobranza y automatización interna en la empresa Assets. Incluye tablas de clientes, carteras, metas, gestores y un cubo de gestiones mensual.

## 🧰 Requisitos

- PostgreSQL instalado (versión recomendada: 13 o superior)
- psql o alguna GUI como DBeaver o pgAdmin
- Git (opcional)
- Opcional: Python 3 para cargar datos masivos con Faker

---

## 📦 1. Instalación de PostgreSQL

### Mac (usando Homebrew)

```bash
brew install postgresql
brew services start postgresql
```

### Ubuntu/Debian

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
```

### Windows

Descarga desde: https://www.postgresql.org/download/windows/  
(Escoge durante la instalación una contraseña para el usuario `postgres`)

---

## 🛠️ 2. Crear base de datos

Abre una terminal y ejecuta:

```bash
psql -U postgres
```

Dentro del prompt de psql:

```sql
CREATE DATABASE assets_db;
\q
```

---

## 📂 3. Cargar estructura y datos

Los archivos SQL están en la carpeta `db/` del repositorio.

- `db/schema.sql` — contiene la creación de todas las tablas
- `db/seeds.sql` — contiene los datos base para mayo 2025

Desde la raíz del proyecto, corre:

```bash
psql -U postgres -d assets_db -f db/schema.sql
psql -U postgres -d assets_db -f db/seeds.sql
psql -U postgres -d assets_db -f db/seeds_cubo.sql
```

O si estás usando alguna GUI (como pgAdmin o DBeaver), abre los archivos de `db/` y ejecútalos en orden.

---

## 🧪 4. Verifica que todo esté OK

```sql
-- Deberías ver los clientes:
SELECT * FROM clientes;

-- Ver carteras por cliente
SELECT c.codigo AS cartera, c.alias, cl.nombre AS cliente
FROM carteras c
JOIN clientes cl ON c.id_cliente = cl.id;

-- Probar el cubo
SELECT COUNT(*) FROM cubo;
```

---