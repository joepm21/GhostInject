# 👻 GhostInject

<p align="center">
  <img src="assets/ghostinject-banner.png" alt="GhostInject Banner" width="850">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Tool-GhostInject-00ffd5?style=for-the-badge&logo=linux&logoColor=white" alt="GhostInject">
  <img src="https://img.shields.io/badge/Platform-Linux%20x86__64-111111?style=for-the-badge&logo=linux&logoColor=white" alt="Linux">
  <img src="https://img.shields.io/badge/GUI-PyQt5-00aa88?style=for-the-badge&logo=qt&logoColor=white" alt="PyQt5">
  <img src="https://img.shields.io/badge/Engine-sqlmap-red?style=for-the-badge" alt="sqlmap">
</p>

**GhostInject** es una herramienta gráfica para Linux orientada a pruebas controladas de **SQL Injection** mediante `sqlmap`. Su objetivo es facilitar el flujo de trabajo de un pentester al permitir configurar objetivos, cookies, headers, proxy, tamper scripts, nivel de prueba, riesgo, técnicas de inyección y acciones rápidas desde una interfaz profesional.

> ⚠️ **Uso autorizado únicamente:** esta herramienta debe utilizarse solo en laboratorios, CTFs, entornos propios o sistemas donde tengas permiso explícito para realizar pruebas de seguridad.

---

## ✨ Características principales

- Interfaz gráfica tipo pentester basada en **PyQt5**.
- Ejecución de pruebas SQLi usando `sqlmap` como motor principal.
- Soporte para URL directa o archivo de request HTTP exportado desde Burp Suite.
- Parámetro vulnerable configurable con `-p`.
- Soporte para cookies, User-Agent personalizado y headers manuales.
- Configuración de `level`, `risk`, `threads`, DBMS y técnicas de inyección.
- Opciones rápidas: `--batch`, `--random-agent`, `--forms`, `--crawl=2` y `--fresh-queries`.
- Soporte para proxy HTTP/S, ideal para Burp Suite o ZAP.
- Soporte para tamper scripts de `sqlmap`.
- Campo de argumentos extra para opciones avanzadas.
- Vista previa del comando generado antes de ejecutarlo.
- Consola en vivo para visualizar la salida de `sqlmap`.
- Botones rápidos para enumerar bases de datos, banner, tablas, columnas y dump de tablas.
- Opción para guardar evidencia/salida en archivo `.txt`.
- Botón para detener el proceso en ejecución.
- Botón para limpiar todos los campos y reiniciar el flujo de trabajo.

---

## 🧩 Requisitos

GhostInject se distribuye como binario Linux, por lo que no necesitas ejecutar el script Python original. Sin embargo, el binario utiliza `sqlmap` instalado en el sistema.

### Sistema recomendado

- Linux x86_64
- Kali Linux, Debian, Ubuntu o derivados
- Entorno gráfico activo: X11/Wayland
- `sqlmap` instalado y disponible en el `PATH`

### Instalar sqlmap

```bash
sudo apt update
sudo apt install -y sqlmap
```

Verifica que `sqlmap` esté disponible:

```bash
which sqlmap
sqlmap --version
```

---

## 🚀 Instalación

Clona el repositorio:

```bash
git clone https://github.com/joepm21/GhostInject.git
cd GhostInject
```

Asigna permisos de ejecución al binario:

```bash
chmod +x GhostInject
```

Ejecuta la herramienta:

```bash
./GhostInject
```

Instalación opcional como comando global:

```bash
sudo cp GhostInject /usr/local/bin/ghostinject
sudo chmod +x /usr/local/bin/ghostinject
```

Luego podrás ejecutarlo con:

```bash
ghostinject
```

---

## 🖥️ Uso básico

1. Ejecuta GhostInject.
2. Confirma que el objetivo cuenta con autorización para pruebas de seguridad.
3. Ingresa una **URL objetivo** o selecciona un **request file** exportado desde Burp Suite.
4. Configura el parámetro a probar, cookies, headers o User-Agent si aplica.
5. Ajusta las opciones de escaneo: level, risk, threads, DBMS, técnica y proxy.
6. Presiona **Preview Command** para revisar el comando generado.
7. Ejecuta una acción rápida:
   - **Test Injection**
   - **Enumerate DBs**
   - **DB Banner**
   - **Tables**
   - **Columns**
   - **Dump Table**
8. Guarda la salida como evidencia con **Save Output**.

Ejemplo de URL de laboratorio:

```text
https://example.com/item.php?id=1
```

---

## ⚙️ Opciones soportadas

GhostInject genera comandos de `sqlmap` usando las siguientes opciones según la configuración seleccionada en la GUI:

```bash
-u <URL>
-r <REQUEST_FILE>
-p <PARAMETER>
--cookie <COOKIE>
--user-agent <USER_AGENT>
--headers <HEADERS>
--level <1-5>
--risk <1-3>
--threads <N>
--dbms <DBMS>
--technique <B|E|U|S|T|Q>
--batch
--random-agent
--forms
--crawl=2
--fresh-queries
--proxy <PROXY>
--tamper <TAMPER_SCRIPT>
--output-dir <DIRECTORY>
```

También permite agregar argumentos extra para casos avanzados, por ejemplo:

```bash
--delay=1 --timeout=20 --retries=2
```

---

## 🧪 Acciones rápidas

| Acción | Descripción |
|---|---|
| **Test Injection** | Ejecuta una prueba base contra el objetivo configurado. |
| **Enumerate DBs** | Enumera bases de datos disponibles usando `--dbs`. |
| **DB Banner** | Obtiene el banner del motor de base de datos con `--banner`. |
| **Tables** | Enumera tablas de una base de datos específica con `-D <db> --tables`. |
| **Columns** | Enumera columnas de una tabla con `-D <db> -T <table> --columns`. |
| **Dump Table** | Extrae información de una tabla con `-D <db> -T <table> --dump`. |
| **Preview Command** | Muestra el comando completo antes de ejecutarlo. |
| **Save Output** | Guarda la salida de consola como evidencia. |
| **Clear All** | Limpia campos, consola, preview y notas. |
| **Stop** | Detiene el proceso de `sqlmap` en ejecución. |

---

## 🧾 Uso con request de Burp Suite

Puedes capturar una petición HTTP desde Burp Suite y guardarla como archivo `.txt`, `.req` o `.http`. Luego, desde GhostInject, selecciona el archivo en **Request file**.

Ejemplo de flujo:

```text
Burp Suite → Intercept → Send to Repeater → Save item/request → cargar en GhostInject
```

Esto es útil cuando el objetivo requiere cookies, tokens, headers personalizados o una petición POST completa.

---

## 🔐 Uso responsable

GhostInject fue creado con fines educativos y profesionales para:

- Laboratorios de pentesting.
- CTFs.
- Auditorías autorizadas.
- Validación de controles de seguridad.
- Demostraciones técnicas en entornos controlados.

No utilices esta herramienta contra sistemas de terceros sin autorización. El uso indebido puede ser ilegal y queda bajo responsabilidad exclusiva del usuario.

---

## 🛠️ Solución de problemas

### `sqlmap was not found`

Instala `sqlmap` y valida que esté en el `PATH`:

```bash
sudo apt install -y sqlmap
which sqlmap
```

### `Permission denied`

Asigna permisos de ejecución:

```bash
chmod +x GhostInject
```

### Error de entorno gráfico o Qt

Ejecuta GhostInject desde un entorno de escritorio Linux. Si lo usas por SSH, habilita X11 forwarding:

```bash
ssh -X usuario@host
./GhostInject
```

En Debian/Ubuntu, si aparece un error relacionado con `xcb`, instala dependencias gráficas comunes:

```bash
sudo apt install -y libxcb-cursor0 libxkbcommon-x11-0 libxcb-xinerama0
```

### Error de GLIBC

Si el sistema muestra un error como `GLIBC_x.xx not found`, ejecuta el binario en una distribución más reciente o recompila el proyecto en la misma versión de Linux donde será utilizado.

---

## 📂 Estructura sugerida del repositorio

```text
GhostInject/
├── GhostInject
├── README.md
├── LICENSE
└── assets/
    └── ghostinject-banner.png
```

## 👤 Autor

Desarrollado por **Gh0s7m4n**.

GitHub: [joepm21](https://github.com/joepm21)

---
## ⭐ Apoya el proyecto

Si esta herramienta te resulta útil, puedes apoyar el repositorio dejando una ⭐ en GitHub y compartiéndola con la comunidad de ciberseguridad.
