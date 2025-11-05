# Introducción a uv (Astral)

## ¿Qué es uv?

**uv** es un gestor de paquetes y entornos virtuales extremadamente rápido para Python, desarrollado por Astral (los creadores de Ruff). Es una alternativa moderna a pip y venv que destaca por:

- **Velocidad:** Escrito en Rust, es 10-100x más rápido que pip
- **Todo en uno:** Gestiona tanto paquetes como entornos virtuales
- **Sin dependencias:** No requiere Python preinstalado para instalarse
- **Reproducibilidad:** Lockfiles automáticos que garantizan instalaciones consistentes

En resumen, uv reemplaza a pip, pip-tools y virtualenv con una única herramienta más rápida y confiable.

## Instalación

Instalar uv es muy sencillo. Solo necesitas ejecutar un comando:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Después de la instalación, cierra y vuelve a abrir tu terminal, o recarga tu configuración:

```bash
source $HOME/.cargo/env
```

Verifica la instalación:

```bash
uv --version
```

## Agregar dependencias

### uv add: Agregar dependencias al proyecto

El comando `uv add` se usa para **agregar nuevas dependencias** a tu proyecto. Este comando:

1. Añade la dependencia al archivo `pyproject.toml`
2. Actualiza el archivo `uv.lock` con las versiones exactas
3. Instala la dependencia en el entorno virtual activo

**Ejemplo:**

```bash
uv add requests
```

Esto agregará `requests` a tu proyecto y lo instalará automáticamente.

### uv sync: Sincronizar el entorno

El comando `uv sync` se usa para **sincronizar el entorno virtual** con las dependencias definidas en `pyproject.toml` y `uv.lock`. Este comando:

1. Lee las dependencias desde `pyproject.toml` y `uv.lock`
2. Instala todas las dependencias necesarias
3. Elimina paquetes que ya no están en la lista de dependencias

**Ejemplo:**

```bash
uv sync
```

### Diferencia entre uv add y uv sync

| Comando | Cuándo usarlo | Qué hace |
|---------|---------------|----------|
| `uv add` | Cuando quieres **agregar una nueva dependencia** | Modifica `pyproject.toml`, actualiza `uv.lock` e instala |
| `uv sync` | Cuando quieres **sincronizar** con los archivos existentes | Solo instala lo que está definido en los archivos, sin modificarlos |

**Analogía:**
- `uv add` es como agregar un ingrediente nuevo a tu receta
- `uv sync` es como preparar la receta exactamente como está escrita

## Archivos pyproject.toml y uv.lock

### pyproject.toml

Es el archivo de **configuración del proyecto**. Define:

- Metadatos del proyecto (nombre, versión, descripción)
- Dependencias del proyecto (con rangos de versiones permitidos)
- Configuración de herramientas

**Ejemplo:**

```toml
[project]
name = "mi-proyecto"
version = "0.1.0"
dependencies = [
    "requests>=2.28.0",
    "pandas>=2.0.0",
]
```

Este archivo define **la intención**: qué dependencias necesita el proyecto y qué versiones son aceptables.

### uv.lock

Es el archivo de **lockfile**. Contiene:

- Las versiones **exactas** de cada dependencia instalada
- Las dependencias transitivas (dependencias de tus dependencias)
- Hashes para verificar la integridad de los paquetes

**Ejemplo simplificado:**

```
requests==2.31.0
urllib3==2.1.0
charset-normalizer==3.3.2
...
```

Este archivo define **el estado exacto**: qué versiones específicas están instaladas en este momento.

### Diferencias clave

| pyproject.toml | uv.lock |
|----------------|---------|
| Define la **intención** | Define el **estado exacto** |
| Rangos de versiones (`>=2.0.0`) | Versiones específicas (`2.31.0`) |
| Editable manualmente | Generado automáticamente |
| Versionado en Git: **SÍ** | Versionado en Git: **SÍ** |
| Legible y conciso | Detallado y técnico |

**Ambos archivos deben estar en el control de versiones** para garantizar que todos los desarrolladores trabajen con las mismas dependencias.

## Ejercicio práctico

Vamos a crear un proyecto desde cero usando uv:

### 1. Crear un nuevo entorno virtual

```bash
# Crea un entorno virtual en la carpeta .venv
uv venv
```

Verás una salida similar a:
```
Using Python 3.10.12 interpreter at: /usr/bin/python3
Creating virtualenv at: .venv
```

### 2. Activar el entorno virtual

**En Linux/macOS:**
```bash
source .venv/bin/activate
```

**En Windows (PowerShell):**
```bash
.venv\Scripts\Activate.ps1
```

**En Windows (CMD):**
```bash
.venv\Scripts\activate.bat
```

Verás que tu prompt cambia para indicar que el entorno está activo:
```
(.venv) usuario@maquina:~/mi-proyecto$
```

### 3. Instalar una dependencia

```bash
# Instalar requests
uv pip install requests
```

**Nota:** Cuando estás dentro de un entorno virtual, puedes usar `uv pip install` en lugar de `uv add`. Para proyectos con `pyproject.toml`, usa `uv add`.

### 4. Listar dependencias instaladas

```bash
uv pip list
```

Verás algo como:
```
certifi        2024.2.2
charset-normalizer 3.3.2
idna           3.6
requests       2.31.0
urllib3        2.2.0
```

### 5. Verificar que funciona (opcional)

Crea un archivo de prueba:

```bash
cat > test_requests.py << 'EOF'
import requests
response = requests.get('https://api.github.com')
print(f"Status: {response.status_code}")
print(f"Requests instalado correctamente!")
EOF
```

Ejecuta el script:

```bash
python test_requests.py
```

### 6. Desactivar el entorno virtual

```bash
deactivate
```

Tu prompt volverá a la normalidad.

### 7. Borrar el entorno virtual

```bash
# Simplemente elimina la carpeta
rm -rf .venv
```

**En Windows:**
```bash
rmdir /s .venv
```

## Comandos útiles de uv

```bash
# Crear entorno virtual
uv venv

# Activar entorno (Linux/macOS)
source .venv/bin/activate

# Instalar dependencias (en entorno virtual)
uv pip install nombre_paquete

# Listar paquetes instalados
uv pip list

# Inicializar un proyecto con pyproject.toml
uv init

# Agregar dependencia al proyecto
uv add nombre_paquete

# Sincronizar dependencias
uv sync

# Ejecutar comando en el entorno sin activarlo
uv run python script.py

# Actualizar uv
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## Recursos adicionales

- [Documentación oficial de uv](https://docs.astral.sh/uv/)
- [Repositorio de GitHub](https://github.com/astral-sh/uv)
- [Anuncios de Astral](https://astral.sh/blog)
