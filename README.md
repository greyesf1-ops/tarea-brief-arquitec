# tarea-brief-arquitec
## 🚀 Guía de Ejecución de la Demo

Siga estos pasos para levantar el entorno de microservicios y verificar la comunicación orientada a eventos.

### 📋 Prerrequisitos
* **Docker Desktop** instalado y en ejecución.
* **Docker Compose** (incluido en Docker Desktop).

### 🛠️ Paso 1: Levantar la Infraestructura
Desde la terminal, en la raíz del proyecto, ejecute el siguiente comando para construir y levantar los contenedores en segundo plano:

```bash
docker compose up -d

```
### 🚀 Guía de Ejecución y Monitoreo

Siga estos pasos para validar el flujo de datos entre los microservicios una vez que el entorno esté configurado:

1. **Verificar el Estado de los Servicios** Asegúrese de que los contenedores estén en ejecución (estado `Running`) en Docker Desktop o mediante la terminal:
   * `kafka_broker` (Puerto 9092)
   * `erp_producer`
   * `inventory_consumer`

2. **Monitorear la Transmisión en Tiempo Real** Para comprobar que el **ERP** está enviando órdenes y el **Inventario** las recibe correctamente, ejecute el siguiente comando para ver los logs:
   ```bash
   docker logs -f inventory_consumer

   ```
   **Enlace a el Repo**
    https://github.com/greyesf1-ops/tarea-brief-arquitec.git

   **Enlace video** 
   https://drive.google.com/drive/folders/1qwRUGK7rNyHop-0CfeotZBM-yySG3OWk?usp=sharing
