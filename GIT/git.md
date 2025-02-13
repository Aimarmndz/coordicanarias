# Instalación y Uso de Git en Linux, Windows y macOS

## Instalación de Git

### En Linux

#### Ubuntu / Linux Mint
```sh
sudo apt update
sudo apt install git
```
> **Nota:**
> - `sudo apt update`: Actualiza la lista de paquetes disponibles.
> - `sudo apt install git`: Instala Git desde los repositorios oficiales.

### En Windows

1. Descarga el instalador desde: [https://git-scm.com/download/win](https://git-scm.com/download/win)
2. Ejecuta el instalador y sigue las instrucciones.
3. Durante la instalación, elige la opción para agregar Git al PATH.

### En macOS

#### Instalación con Homebrew
```sh
brew install git
```
> **Nota:**
> - `brew install git`: Instala Git utilizando Homebrew, un gestor de paquetes para macOS.

## Verificación de la Instalación
```sh
git --version
```
> **Nota:**
> - `git --version`: Muestra la versión de Git instalada en el sistema.

## Configuración Inicial de Git

Establecer nombre y correo:
```sh
git config --global user.name "Tu Nombre"
git config --global user.email "tuemail@example.com"
```
> **Nota:**
> - `git config --global user.name`: Define el nombre de usuario para todos los repositorios.
> - `git config --global user.email`: Define el correo asociado a Git.

Verificar configuración:
```sh
git config --list
```
> **Nota:**
> - `git config --list`: Muestra la configuración actual de Git.

## Crear y Subir un Repositorio a GitHub

1. **Crear un nuevo repositorio local:**
```sh
git init mi-repositorio
cd mi-repositorio
```
> **Nota:**
> - `git init mi-repositorio`: Inicializa un nuevo repositorio local en la carpeta `mi-repositorio`.

2. **Crear un archivo README.md:**
```sh
echo "# Mi Proyecto" > README.md
```
3. **Añadir los archivos al repositorio:**
```sh
git add .
```
4. **Confirmar los cambios:**
```sh
git commit -m "Primer commit"
```
5. **Conectar con GitHub:**
```sh
git remote add origin https://github.com/tuusuario/mi-repositorio.git
```
6. **Subir el repositorio a GitHub:**
```sh
git push -u origin main
```

## Colaboración en un Repositorio

### Clonar un Repositorio
```sh
git clone https://github.com/usuario/repositorio.git
```

### Crear y Gestionar Ramas

#### Crear una nueva rama:
```sh
git branch nueva-rama
```

#### Cambiar a una rama existente:
```sh
git switch nueva-rama
```

#### Fusionar ramas (Merge)
```sh
git checkout main
git merge nueva-rama
```

#### Rebasing
```sh
git checkout feature-branch
git rebase main
```

### Enviar cambios al repositorio remoto
```sh
git push origin nueva-rama
```

### Hacer un Pull Request en GitHub
1. Subir la rama al repositorio remoto.
2. Ir a GitHub y abrir una "Pull Request" desde la rama creada.
3. Esperar la revisión y aprobación.
4. Fusionar los cambios en la rama principal.

### Mantener el Repositorio Actualizado

#### Obtener los últimos cambios sin fusionar automáticamente:
```sh
git fetch
```

#### Obtener y fusionar cambios:
```sh
git pull
```

### Resolver Conflictos en Merge o Rebase
Si Git detecta conflictos:
```sh
git status
```
Editar los archivos en conflicto, luego:
```sh
git add archivo_conflictivo
git commit -m "Conflicto resuelto"
```

## Changelog

Formato sugerido:
```
## [Fecha] - [Versión]
### Añadido
- Descripción de lo nuevo

### Cambios
- Mejoras o modificaciones

### Eliminado
- Elementos eliminados
```

Ejemplo:
```
## [2025-02-13] - v1.0
### Añadido
- Instalación y configuración de Git

### Cambios
- Mejorado el proceso de subida a GitHub
```
