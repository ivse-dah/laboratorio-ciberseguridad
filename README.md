# 🛡️ Laboratorio de Kali Linux en el Navegador

Entorno oficial de **Kali Linux** con interfaz gráfica completa (XFCE), herramientas de auditoría de seguridad preinstaladas (**Burp Suite**, **Wordlists**, suite de pruebas de red) y soporte completo para túneles VPN, ejecutado al 100% en la nube sin costo.

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/TU-USUARIO/laboratorio-ciberseguridad)

*(Tip: Haz **Ctrl + Clic** o clic con la rueda del ratón en el botón para abrirlo en una pestaña nueva).*

---

## 🚀 Cómo iniciar el laboratorio

1. Haz clic en el botón superior **Open in GitHub Codespaces** (inicia sesión con tu cuenta de GitHub si no lo has hecho).
2. Si te aparece una ventana de confirmación, pulsa el botón verde **Create codespace**.
3. **Paciencia durante la creación inicial (Aprox. 8 a 10 minutos):**  
   GitHub descargará y compilará la imagen completa de Kali Linux con todas las herramientas y temas visuales oficiales. Puedes ver el avance en la consola; no cierres la ventana.
4. Una vez cargado el entorno de VS Code, **el escritorio se abrirá automáticamente en una nueva pestaña**:
   * Si no se abre por sí sola, ve a la pestaña inferior **Puertos** (*Ports*) dentro de VS Code y haz clic en el icono del **globo terráqueo** en la fila del puerto `6080`.
   * En la pantalla de bienvenida, haz clic en el botón **Connect**.
   * **Contraseña de acceso:** `kali123`
   * **Usuario en terminal:** `kali` (contraseña para `sudo`: `kali`).

---

## 🌐 Conexión a la VPN (TryHackMe / Hack The Box / Laboratorio)

Para conectar tu máquina en la nube a las redes de práctica mediante OpenVPN:

### Paso 1: Descargar el archivo de configuración
Abre el navegador **Firefox** dentro de tu Kali en la nube, entra a la plataforma de práctica y descarga tu archivo de acceso VPN.

### Paso 2: Conectar el túnel
Abre una terminal en Kali (icono negro en la barra superior) y ejecuta:

```bash
sudo openvpn ~/Downloads/*.ovpn
