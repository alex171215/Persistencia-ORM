# Bitácora de Despliegue y Persistencia

## 1. URL Pública del Servicio en Render
*Por favor, reemplaza "XXXX" con el identificador único que Render le asignó a tu servicio:*
`https://nestjs-productos-api-XXXX.onrender.com/swagger`

---

## 2. Persistencia de Datos tras Reinicio del Servicio (Paso 8)

**¿Por qué los datos sobrevivieron al reinicio?**

En prácticas anteriores guardábamos los productos en memoria (en un arreglo dentro de Node.js). La memoria RAM de un proceso de Node es volátil: cuando el servicio se detiene o se reinicia (por ejemplo, cuando Render apaga el servicio por inactividad o por un nuevo despliegue), toda esa memoria se limpia y el arreglo desaparece.

Sin embargo, al integrar **PostgreSQL**, hemos desacoplado los datos de la aplicación. 
- El proceso de **Node.js** ahora solo actúa como un intermediario (cliente) que recibe peticiones web.
- La **Base de Datos (PostgreSQL)** es un servidor/proceso totalmente independiente con su propio almacenamiento persistente en disco (volumen físico).

Cuando el servicio de Node se reinicia, solo se reinicia el intermediario. La base de datos en Postgres sigue intacta en su propio servidor de Render. Al volver a encenderse Node, simplemente se reconecta a la base de datos y vuelve a consultar los registros que estaban guardados de forma segura en el disco.

---

## 3. Declaración de uso de IA (Paso 9)
- **Herramienta(s):** Antigravity AI (Gemini 3.1 Pro / 3.6 Flash)
- **Nivel de uso:** Nivel 2–3 (Borrador / Revisor)
- **Qué se le pidió:**
  - Diagnóstico y resolución de errores de conexión (`SASL: client password must be a string`) y configuración de ESM en tests de Jest.
  - Explicación sobre qué SQL generan los métodos de TypeORM Repository y las alternativas a `synchronize: true` para producción.
  - Creación del archivo de infraestructura `render.yaml` (Blueprint) y explicación de los conceptos de Docker y Render.
- **Qué se modificó/verificó manualmente:**
  - Verificación del archivo `.env` y de los archivos `.yaml` de GitHub Actions y Render.
  - Comprobación del funcionamiento del CRUD completo interactuando manualmente mediante Docker (`docker exec`) y la plataforma Swagger en local.
