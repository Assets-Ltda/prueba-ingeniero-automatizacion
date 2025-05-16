# 📄 Instrucciones - Prueba Técnica

Bienvenido/a a la prueba técnica para el cargo de **Ingeniero/a en Automatización y Procesos** en **Assets**. Esta prueba evalúa tus conocimientos en SQL, modelado de datos y pensamiento analítico aplicado a operaciones reales de una empresa de cobranza.

---

## 🏗️ 1. Contexto general

Trabajarás con una base de datos de prueba que simula la estructura y datos de Assets. Contiene información de clientes, carteras, metas mensuales/semanales y un cubo de gestiones mensuales (uno por RUT).

### Tablas incluidas:
- `clientes`
- `carteras`
- `gestores`
- `gestores_cartera_mes`
- `meses`
- `semanas`
- `metas_mes`
- `metas_semanales`
- `cubo`

Puedes revisar el archivo [`setup.md`](./setup.md) para ver instrucciones de instalación, creación de base de datos, carga de datos y queries de prueba.

---

## 📊 2. Objetivo

El objetivo es escribir consultas SQL que respondan preguntas típicas del área de operaciones y reporting en una empresa de cobranza.

---

## 🧪 3. Preguntas

### Pregunta 1 - Análisis por tipo de gestión

Escribe una consulta que agrupe por `estado_codigo` en la tabla `cubo` y muestre:
- `detalle_codigo`
- `clasificacion`
- Cantidad de RUTs con ese código
- Monto total (suma de `monto`)
- Recupero total (suma de `abonos`)
- Saldo total (suma de `saldo`)

Ordena los resultados por `recupero total` descendente.

---

### Pregunta 2 - Reporte mensual de cartera

Dado el mes "VA2505", escribe una sola consulta que muestre:
- Nombre del cliente
- Alias de la cartera
- Meta mensual (`valor_meta`)
- Meta semana 1 a semana 4 (campos separados)
- Recupero total (suma de abonos desde `cubo`)
- Porcentaje recuperado (`recupero / valor_meta * 100`)
---

### Pregunta 3 - Ranking de gestores

Para cada gestor en mayo 2025, genera un ranking de desempeño que incluya:
- Nombre del gestor
- Mes
- % Recuperado vs. meta
- Categoría de desempeño:
  - "Excede" si ≥110%
  - "Cumple" si entre 90% y 109.9%
  - "No cumple" si <90%
- Total de RUTs gestionados

Ordena por mes y porcentaje recuperado descendente.

---

### Pregunta 4 - Nuevos requerimientos de negocio 📐

Actualmente, las metas se asignan a nivel de cartera. Sin embargo, el equipo de operaciones ha solicitado un cambio: **ahora las metas se definirán por subcartera**, es decir, por el campo `subcartera` presente en la tabla `cubo`.

**¿Cómo modificarías el modelo de datos para implementar este nuevo requerimiento?**

- Puedes agregar, modificar o eliminar tablas y relaciones.
- Justifica las decisiones de modelado.
- Considera cómo migrarías los datos históricos para que el sistema siga funcionando sin perder trazabilidad.

Se valora especialmente la capacidad de mantener integridad, flexibilidad y simplicidad en la solución propuesta.

---

### Pregunta 5 - Automatización de ingreso de semanas vía interfaz web

Crea una interfaz web simple (puedes usar solo HTML, CSS y JavaScript o cualquier framework si prefieres) que permita al usuario cargar las semanas de un mes específico en la base de datos PostgreSQL existente.

### Requerimientos funcionales:
- La UI debe recibir el mes como entrada (formato: año y mes).
- Al enviar el formulario:
  - Crear un nuevo mes en la tabla `meses` con:
    - `codigo`: con el formato `VA<YYMM>` (ejemplo: mayo 2025 → `VA2505`).
    - `fecha_inicio`: primer día del mes ingresado.
  - Crear las **4 semanas** correspondientes a ese mes usando el siguiente algoritmo:
    - La **semana 4** debe terminar el **último día del mes**.
    - Las **semanas 2, 3 y 4** deben tener exactamente **7 días**.
    - La **semana 1** debe comenzar el primer día del mes y terminar justo antes de la semana 2.
    - Cada semana debe tener correctamente calculada la cantidad de **días hábiles** (puedes asumir que solo se validará en el año 2025).
    - Puedes usar cualquier mecanismo para conocer los feriados (archivo local, array embebido, conexión a api externa, etc.).
    - Los sábados son días hábiles, los domingos no.

### Requerimientos técnicos:
- La aplicación **no debe duplicar semanas** ya existentes en la base.
- La interfaz debe dar feedback claro al usuario (éxito o errores).
- Puedes usar cualquier stack tecnológico, mientras se conecte correctamente a la base PostgreSQL ya creada.
- Debe incluir instrucciones claras sobre cómo ejecutar tu código.

Se evaluará:
- Claridad de la UI
- Correcta implementación del algoritmo de creación de semanas
- Manejo de errores
- Documentación y facilidad de ejecución

---

### Pregunta Bonus 💥 - Datos masivos

Crea un script en Python que genere al menos 500 registros falsos para la tabla `cubo`. El script debe:
- Usar `Faker` para nombres, comunas, calles
- Generar RUTs aleatorios
- Asignar aleatoriamente carteras y gestores existentes
- Insertar los registros en la base PostgreSQL

Puedes usar librerías como `faker`, `psycopg2` o `sqlalchemy`. Asegúrate de no romper las claves externas 😅

---

## 📝 Entrega

- Por favor entrega tus consultas SQL y el script Python (si haces la pregunta bonus) en un repositorio o carpeta compartida.
- Si necesitas agregar comentarios o supuestos, hazlo como comentarios dentro del código SQL o Python.

---

¡Buena suerte y a brillar! ✨