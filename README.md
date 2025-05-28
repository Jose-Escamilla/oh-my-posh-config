# oh-my-posh-config
Configuración personalizada de Oh My Posh en Windows

# Guía paso a paso para instalar y configurar Oh My Posh en Windows con PowerShell

Esta guía te ayudará a instalar y configurar Oh My Posh en PowerShell sobre Windows, incluyendo temas personalizados, fuentes e iconos para una experiencia enriquecida en la terminal.

---

## Paso 1: Instalar Oh My Posh

Ejecuta este comando en PowerShell para instalar Oh My Posh:

```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget
```

---

## Paso 2: Instalar una fuente Nerd Font

Visita [https://www.nerdfonts.com/font-downloads](https://www.nerdfonts.com/font-downloads) y descarga la fuente **CaskaydiaCove Nerd Font**.

Una vez descargada, haz clic derecho y selecciona **Instalar para todos los usuarios**.

---

## Paso 3: Editar el perfil de PowerShell

Abre tu perfil con este comando:

```powershell
notepad $PROFILE
```

Si no existe, PowerShell lo creará automáticamente.

---

## Paso 4: Probar Oh My Posh

Puedes probar si Oh My Posh funciona ejecutando en la terminal:

```powershell
oh-my-posh --init --shell pwsh --config "C:\Ruta\al\tema.omp.json" | Invoke-Expression
```

(Sustituye la ruta por la de tu archivo de tema personalizado.)

---

## Paso 5: Elegir tema personalizado

1. Crea una carpeta llamada `Terminal Theme` en tu carpeta de **Documentos**.
2. Copia tu tema personalizado, por ejemplo `1_shell.omp.json`, dentro de esa carpeta.
3. Abre de nuevo tu perfil:

```powershell
notepad $PROFILE
```

4. Añade esta línea al final del archivo:

```powershell
oh-my-posh init pwsh --config "C:\Users\jose0\OneDrive\Documentos\Terminal Theme\1_shell.omp.json" | Invoke-Expression
```

Guarda y cierra el archivo.

---

## Paso 6: Instalar íconos en la terminal

Ejecuta el siguiente comando para instalar el módulo de íconos:

```powershell
Install-Module -Name Terminal-Icons -Repository PSGallery
```

Para verificar que se instaló correctamente:

```powershell
Get-Module -ListAvailable Terminal-Icons
```

Luego abre de nuevo tu perfil:

```powershell
notepad $PROFILE
```

y añade esta línea al final:

```powershell
Import-Module Terminal-Icons
```

---

## Paso 7: Añadir configuración a VSCode

Abre `settings.json` desde VSCode (usa `Ctrl + Shift + P` > "Preferences: Open Settings (JSON)") y añade o modifica esta línea:

```json
"terminal.integrated.cwd": "${fileDirname}"
```

Si Oh My Posh no aparece en la terminal de VSCode, vuelve a instalarlo con:

```powershell
winget install JanDeDobbeleer.OhMyPosh -s winget
```

---

## Paso 8: Tema personalizado con bloques alineados a la izquierda

Se modificó el archivo `1_shell.omp.json` para que todos los bloques (usuario, hora, uso de memoria, ruta actual, etc.) aparezcan juntos y alineados a la izquierda.

### Ejemplo visual:

```
 jose0 on Sunday at 11:39 PM
0.336s  MEM: 31% (4/15GB)
 home  AppData  Roaming  Code  User
```

De esta manera, todo el contenido se muestra de forma ordenada y clara en la parte superior izquierda de la terminal.

---

¡Listo! Ya tienes un entorno PowerShell visualmente enriquecido y totalmente personalizado con Oh My Posh.
