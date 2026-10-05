# 🛡️ Laboratorio de Kali Linux en el Navegador

Entorno oficial de **Kali Linux** con interfaz gráfica completa (XFCE), herramientas de auditoría de seguridad preinstaladas (**Burp Suite**, **Wordlists**, utilidades de red) y soporte completo para túneles VPN, ejecutado al 100% en la nube sin costo.

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/ivse-dah/laboratorio-ciberseguridad)

*(Tip: Haz **Ctrl + Clic** o clic con la rueda del ratón en el botón para abrirlo en una pestaña nueva).*

---

## 🚀 Cómo iniciar el laboratorio

1. Haz clic en el botón superior **Open in GitHub Codespaces** (inicia sesión con tu cuenta de GitHub si no lo has hecho)[cite: 13].
2. Si te aparece una ventana de confirmación, pulsa el botón verde **Create codespace**[cite: 13].
3. **Paciencia durante la creación inicial (Aprox. 10 minutos):**  
   GitHub descargará y compilará la imagen completa de Kali Linux con todas las herramientas y temas visuales oficiales. Puedes seguir el proceso en consola; no cierres la ventana.
4. Al finalizar la carga, **el escritorio se abrirá en una nueva pestaña**:
   * Si no se abre sola, entra a la pestaña inferior **Puertos** (*Ports*) dentro de VS Code y haz clic en el icono del **globo terráqueo** en la fila del puerto `6080`[cite: 13].
   * En la pantalla de bienvenida, pulsa el botón **Connect**[cite: 13].
   * **Contraseña de acceso:** `kali123`[cite: 13]
   * **Usuario en terminal:** `kali` (contraseña sudo: `kali`)[cite: 13].

---

## 🌐 Conexión a la VPN (TryHackMe / Hack The Box / Laboratorio)

### Paso 1: Descargar y renombrar el archivo
Abre el navegador **Firefox** dentro de tu Kali en la nube, entra a la plataforma y descarga tu paquete VPN. Para evitar problemas con nombres largos, renombra el archivo descargado como **`vpn.ovpn`** dentro de la carpeta `Downloads`.

### Paso 2: Conectar el túnel
Abre una terminal en Kali (icono negro en la barra superior) y ejecuta:

```bash
sudo openvpn ~/Downloads/vpn.ovpn

### Paso 3: Verificar la conexión
Abre una **segunda pestaña** en la terminal y envía una prueba de ping a la red del laboratorio:

```bash
ping -c 4 192.168.128.1

## 🛑 Cómo finalizar la práctica (¡Muy importante!)

Cada cuenta gratuita de GitHub cuenta con **60 horas al mes**. Este entorno funciona como un **laboratorio desechable**: para no malgastar los 30 minutos de inactividad que tarda el sistema en suspenderse automáticamente y evitar errores en sesiones futuras, elimina la máquina en cuanto termines la clase:

1. Entra directamente a este enlace: **[https://github.com/codespaces](https://github.com/codespaces)**.
2. Busca tu máquina activa bajo el repositorio `laboratorio-ciberseguridad`.
3. Haz clic en el menú de los tres puntos (**`...`**) a la derecha y selecciona **Delete** (Eliminar).
