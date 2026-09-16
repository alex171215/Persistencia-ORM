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


