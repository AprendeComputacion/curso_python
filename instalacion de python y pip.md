# Instalación de Python y pip

Guía completa para instalar Python y pip en Ubuntu.

## Instalación de Python en Ubuntu

### ¿Python ya está instalado?

En la mayoría de las distribuciones modernas de Ubuntu, Python 3 viene preinstalado. Sin embargo, es importante notar que el comando `python` puede no estar disponible directamente. Esto se debe a que las versiones recientes de Ubuntu solo incluyen `python3` por defecto.

### Verificar la instalación

Para verificar si Python está instalado en tu sistema, ejecuta:

```bash
python3 --version
```

Esto debería mostrar algo como:
```
Python 3.10.12
```

Si intentas usar `python` (sin el 3):
```bash
python --version
```

Es posible que obtengas un error como:
```
Command 'python' not found, but can be installed with:
sudo apt install python-is-python3
```

### Instalar Python 3

Si Python 3 no está instalado en tu sistema, puedes instalarlo con:

```bash
sudo apt update
sudo apt install python3
```

### Crear alias para usar `python` en lugar de `python3`

#### ¿Qué es un alias?

Un alias es un atajo que puedes crear en tu terminal para ejecutar un comando usando un nombre diferente. En este caso, queremos que al escribir `python` se ejecute `python3`.

#### Alias para Bash

Si usas Bash (el shell por defecto en Ubuntu), edita el archivo `~/.bashrc`:

```bash
# Abre el archivo con tu editor favorito
nano ~/.bashrc

# Agrega esta línea al final del archivo:
alias python='python3'

# Guarda y cierra el archivo
# Luego recarga la configuración:
source ~/.bashrc
```

O puedes hacerlo directamente con un comando:

```bash
echo "alias python='python3'" >> ~/.bashrc
source ~/.bashrc
```

#### Alias para Zsh

Si usas Zsh (común en macOS y cada vez más popular en Linux), edita el archivo `~/.zshrc`:

```bash
# Abre el archivo con tu editor favorito
nano ~/.zshrc

# Agrega esta línea al final del archivo:
alias python='python3'

# Guarda y cierra el archivo
# Luego recarga la configuración:
source ~/.zshrc
```

O puedes hacerlo directamente con un comando:

```bash
echo "alias python='python3'" >> ~/.zshrc
source ~/.zshrc
```

#### Verificar el alias

Después de configurar el alias, verifica que funcione:

```bash
python --version
```

Ahora debería mostrar la versión de Python 3.

### Alternativa: Instalar python-is-python3

Ubuntu ofrece un paquete que crea el enlace `python` para que apunte a `python3`:

```bash
sudo apt update
sudo apt install python-is-python3
```

Esto hace que el comando `python` esté disponible en todo el sistema sin necesidad de configurar aliases.

## Instalación y uso de pip

### ¿Qué es pip?

**pip** (Package Installer for Python) es el gestor de paquetes estándar para Python. Te permite instalar y administrar librerías y dependencias adicionales que no vienen incluidas en la biblioteca estándar de Python.

Con pip puedes:
- Instalar paquetes desde el Python Package Index (PyPI)
- Desinstalar paquetes
- Actualizar paquetes
- Listar paquetes instalados
- Y mucho más

### Verificar si pip está instalado

Para verificar si pip está instalado, ejecuta:

```bash
pip3 --version
```

o

```bash
python3 -m pip --version
```

### Instalar pip

Si pip no está instalado, puedes instalarlo con:

```bash
sudo apt update
sudo apt install python3-pip
```

### Alias para pip

Al igual que con Python, puede que quieras crear un alias para usar `pip` en lugar de `pip3`:

**Para Bash:**
```bash
echo "alias pip='pip3'" >> ~/.bashrc
source ~/.bashrc
```

**Para Zsh:**
```bash
echo "alias pip='pip3'" >> ~/.zshrc
source ~/.zshrc
```

### Instalar paquetes con pip

#### Sintaxis básica

```bash
pip3 install nombre_del_paquete
```

O si configuraste el alias:

```bash
pip install nombre_del_paquete
```

#### Ejemplos prácticos

**1. Instalar requests (para hacer peticiones HTTP):**
```bash
pip3 install requests
```

**2. Instalar numpy (para cálculos numéricos):**
```bash
pip3 install numpy
```

**3. Instalar pandas (para análisis de datos):**
```bash
pip3 install pandas
```

**4. Instalar una versión específica:**
```bash
pip3 install requests==2.28.0
```

**5. Instalar múltiples paquetes a la vez:**
```bash
pip3 install requests numpy pandas
```

**6. Instalar desde un archivo requirements.txt:**
```bash
pip3 install -r requirements.txt
```

### Comandos útiles de pip

**Listar paquetes instalados:**
```bash
pip3 list
```

**Mostrar información de un paquete:**
```bash
pip3 show nombre_del_paquete
```

**Actualizar un paquete:**
```bash
pip3 install --upgrade nombre_del_paquete
```

**Desinstalar un paquete:**
```bash
pip3 uninstall nombre_del_paquete
```

**Buscar paquetes:**

El comando `pip search` fue eliminado en pip 21.0. Para buscar paquetes, puedes:
- Visitar directamente [PyPI.org](https://pypi.org/) y usar su buscador
- Usar la búsqueda de Google: `site:pypi.org nombre_del_paquete`

### Buenas prácticas

1. **Usar entornos virtuales:** Es recomendable usar entornos virtuales para cada proyecto para evitar conflictos entre dependencias:
   ```bash
   python3 -m venv mi_entorno
   source mi_entorno/bin/activate
   ```

2. **Mantener pip actualizado:**
   ```bash
   pip3 install --upgrade pip
   ```

3. **Usar requirements.txt:** Para proyectos, es buena práctica mantener un archivo `requirements.txt` con todas las dependencias:
   ```bash
   # Generar requirements.txt
   pip3 freeze > requirements.txt
   ```

## Resumen de comandos rápidos

```bash
# Verificar versiones
python3 --version
pip3 --version

# Instalar Python y pip
sudo apt update
sudo apt install python3 python3-pip

# Crear aliases (Bash)
echo "alias python='python3'" >> ~/.bashrc
echo "alias pip='pip3'" >> ~/.bashrc
source ~/.bashrc

# Crear aliases (Zsh)
echo "alias python='python3'" >> ~/.zshrc
echo "alias pip='pip3'" >> ~/.zshrc
source ~/.zshrc

# Instalar paquetes
pip3 install nombre_del_paquete

# Listar paquetes instalados
pip3 list
```

## Recursos adicionales

- [Documentación oficial de Python](https://docs.python.org/es/)
- [Documentación oficial de pip](https://pip.pypa.io/en/stable/)
- [Python Package Index (PyPI)](https://pypi.org/)