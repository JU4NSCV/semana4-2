
# 🚀 Instalación y Configuración de CouchDB en Ubuntu

Este repositorio contiene la documentación y guía paso a paso para la instalación de **Apache CouchDB** en un entorno Ubuntu (probado en Lenovo ThinkPad), cubriendo tanto la instalación tradicional como el despliegue mediante Docker.

---

## 📋 Requisitos Previos

- Sistema Operativo: Ubuntu 22.04 LTS o superior.
- Usuario con privilegios `sudo`.
- Docker instalado (para el método de contenedores).
- Conexión a internet.

---

## 🛠️ 1. Instalación Tradicional (Nativa)

La instalación nativa permite ejecutar CouchDB como un servicio del sistema.

### 📌 Pasos realizados:

#### 1. Actualización de repositorios
```bash
sudo apt update && sudo apt install -y curl apt-transport-https gnupg
````



#### 2. Configuración de llaves y repositorio oficial

Se añadió la llave GPG oficial de Apache CouchDB para garantizar la autenticidad de los paquetes.

#### 3. Instalación del paquete

```bash
sudo apt install -y couchdb
```

#### 4. Configuración del asistente

Durante la instalación:

* Se configuró el nodo como **standalone**.
* Se definió el usuario administrador.

📸 *Captura de pantalla sugerida*

---

## 🐳 2. Despliegue con Docker

Este método permite aislar la base de datos y facilitar su portabilidad.

### 📌 Comando de ejecución

```bash
docker run -d \
  --name mi-couchdb \
  -p 5984:5984 \
  -e COUCHDB_USER=admin \
  -e COUCHDB_PASSWORD=tu_password \
  -v ~/couchdb_data:/opt/couchdb/data \
  couchdb:latest
```

### 📌 Verificación de contenedores

```bash
docker ps
```

📸 *Captura de pantalla sugerida*

---

## 🌐 3. Administración vía Web (Fauxton)

CouchDB incluye una interfaz gráfica de administración llamada **Fauxton**.

### 🔗 Acceso:

```
http://localhost:5984/_utils/
```

### ✅ Funcionalidades probadas:

* Creación de bases de datos.
* Inserción de documentos JSON.
* Verificación del estado del nodo.

📸 *Captura de pantalla sugerida*

---

## 💻 4. Pruebas de Conexión (cURL)

Se verificó el acceso mediante la línea de comandos para asegurar que la API HTTP responde correctamente:

```bash
curl http://admin:tu_password@127.0.0.1:5984/
```

### 📌 Resultado esperado:

```json
{
  "couchdb": "Welcome",
  "version": "3.3.3",
  "features": [
    "access-ready",
    "partitioned",
    "pluggable-storage-engines",
    "reshard",
    "scheduler"
  ],
  "vendor": {
    "name": "The Apache Software Foundation"
  }
}
```

---

## 📝 Notas de Hardware (ThinkPad / Dual Boot)

Durante este proceso se realizaron ajustes en la BIOS de la Lenovo ThinkPad para permitir el arranque de Ubuntu sin conflictos con BitLocker de Windows:

* Desactivación de **Secure Boot** o registro de llaves MOK.
* Cambio de modo de almacenamiento a **AHCI** (si aplica).

---
