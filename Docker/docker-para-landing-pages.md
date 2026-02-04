# Docker para Landing Pages (Guía práctica)

Este repositorio contiene una **guía práctica y paso a paso** para aprender Docker usando un caso real: **levantar una Landing Page HTML/CSS/JS** en Fedora Linux.

La idea es que puedas **clonar este repo**, seguir la guía y usarla como referencia rápida en tus proyectos.

---

## 🎯 Objetivo

* Aprender Docker desde cero
* Levantar una landing page sin XAMPP
* Ver cambios en tiempo real durante el desarrollo
* Entender la diferencia entre desarrollo y producción

---

## 🧠 Conceptos básicos

### ¿Qué es Docker?

Docker permite ejecutar aplicaciones dentro de **contenedores**, sin instalarlas directamente en tu sistema.

Piensa en Docker como una forma limpia y controlada de correr servidores como Nginx o Apache.

---

### Imagen vs Contenedor

| Concepto   | Explicación                          |
| ---------- | ------------------------------------ |
| Imagen     | Plantilla inmutable (foto congelada) |
| Contenedor | Imagen en ejecución                  |

Ejemplo:

* Imagen: `nginx:alpine`
* Contenedor: Nginx corriendo en tu PC

---

## 📁 Estructura recomendada del proyecto

```
landing/
├── index.html
├── about.html
├── contact.html
├── assets/
│   ├── css/
│   ├── js/
│   └── images/
```

---

## 🛠️ Requisitos

* Fedora Linux
* Docker instalado y funcionando
* Proyecto HTML/CSS/JS

Verificar Docker:

```bash
docker --version
docker ps
```

---

## 🚀 Opción 1: Docker para DESARROLLO (recomendada)

Este modo permite **ver los cambios al instante**, sin reconstruir imágenes.

### Levantar el servidor

Ejecuta desde la carpeta del proyecto:

```bash
docker run -d \
-p 8080:80 \
-v $(pwd):/usr/share/nginx/html \
--name landing \
nginx:alpine
```

### Abrir en el navegador

```
http://localhost:8080
```

Desde otra PC (misma red):

```
http://TU_IP:8080
```

---

## 🏗️ Opción 2: Docker para PRODUCCIÓN

Este modo crea una imagen final con los archivos incluidos.

### Dockerfile

```Dockerfile
FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
COPY . /usr/share/nginx/html
EXPOSE 80
```

### Construir imagen

```bash
docker build -t page_cybersecurity .
```

### Ejecutar contenedor

```bash
docker run -d -p 8080:80 --name landing page_cybersecurity
```

---

## 🌐 Acceso desde otra PC

1. Obtener IP:

```bash
ip a
```

2. Abrir puerto (si aplica):

```bash
sudo firewall-cmd --add-port=8080/tcp --permanent
sudo firewall-cmd --reload
```

3. Acceder desde el navegador:

```
http://TU_IP:8080
```

---

## 📌 Comandos básicos de Docker

| Acción               | Comando                      |
| -------------------- | ---------------------------- |
| Ver contenedores     | `docker ps`                  |
| Ver imágenes         | `docker images`              |
| Detener contenedor   | `docker stop landing`        |
| Eliminar contenedor  | `docker rm -f landing`       |
| Logs                 | `docker logs landing`        |
| Entrar al contenedor | `docker exec -it landing sh` |

---

## ⚠️ Problemas comunes

### No se ven los cambios

Usa volumen (`-v $(pwd)`) en desarrollo.

---

### Error de permisos Docker

```bash
sudo usermod -aG docker $USER
```

Cerrar sesión y volver a entrar.

---

### No abre desde otra PC

* Verifica IP correcta
* Revisa firewall
* Confirma que estén en la misma red

---

## 📈 Flujo recomendado de aprendizaje

1. Desarrollo con volumen
2. Entender imágenes y contenedores
3. Build para producción
4. Docker Compose
5. Deploy en VPS

---

## 🧠 Idea clave

> Docker no es complicado.
> Solo automatiza cosas que ya hacías a mano.

---

## ✍️ Autor

Guía creada como material de aprendizaje práctico para desarrollo web y despliegue con Docker.

---

🚀 Happy Dockering

