
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

![Oh My Posh en VSCode](https://github.com/Jose-Escamilla/oh-my-posh-config/blob/master/terminal_vscode.png?raw=true)

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

![Terminal personalizada con Oh My Posh](https://github.com/Jose-Escamilla/oh-my-posh-config/blob/master/terminal.png?raw=true)

---

## Nota sobre los íconos en la terminal de VSCode

Por defecto, la terminal integrada de VSCode utiliza el tema predeterminado, por lo que es posible que los íconos de Oh My Posh **no se muestren correctamente**. Para que los íconos aparezcan en la terminal de VSCode, debes cambiar la fuente de la terminal por una Nerd Font, como **CaskaydiaCove Nerd Font** o **MesloLGS NF** que instalaste previamente.

### Pasos para cambiar la fuente de la terminal en VSCode:

1. Abre VSCode.
2. Ve a **Archivo > Preferencias > Configuración** (o usa `Ctrl + ,`).
3. En la barra de búsqueda escribe: `terminal.integrated.fontFamily`.
4. En el campo correspondiente a la configuración, escribe el nombre exacto de la fuente Nerd Font que instalaste, por ejemplo:
   ```
   CaskaydiaCove Nerd Font
   ```
  > ⚠ Yo use la fuente: MesloLGS NF
5. Cierra y vuelve a abrir la terminal integrada (`Ctrl + ``) para que los cambios se apliquen.

Después de este cambio, los íconos deberían mostrarse correctamente en la terminal integrada de VSCode.

---

# Respaldo: Solución de problemas y configuración avanzada de PowerShell

Durante la configuración de Oh My Posh en PowerShell, se aplicaron las siguientes soluciones y mejoras para garantizar un entorno funcional y visualmente enriquecido:

### Problemas encontrados

- Error al importar el módulo PSReadLine versión 2.3.6 (no estaba instalado).
- Conflictos por módulos duplicados o versiones no compatibles.
- Los íconos no se visualizaban correctamente en la terminal (aparecían caracteres extraños o cuadros).
- Inicialización incompleta o conflictiva de módulos en perfiles de PowerShell.

### Soluciones aplicadas

- Se eliminó la restricción de versión específica en la importación de PSReadLine, usando simplemente:

```powershell
Import-Module PSReadLine -Force
```

- Se consolidó el perfil de PowerShell (`Microsoft.PowerShell_profile.ps1`) para cargar en orden:
  - Oh My Posh con el tema personalizado.
  - PSReadLine (sin versión fija).
  - Terminal-Icons para los íconos en listados.
  - Autocompletado de Chocolatey.
  - Inicialización de Conda si está instalado.

- Se instaló y configuró la fuente **MesloLGS NF** (Nerd Font), necesaria para mostrar correctamente los íconos en la terminal.

### Perfil final recomendado

Abre tu perfil usando:
```powershell
notepad $PROFILE
```
y luego pega lo siguiente: 

```powershell
# =========================
# Perfil personalizado de PowerShell de José Escamilla
# =========================

# Activar tema de terminal con Oh My Posh
oh-my-posh init pwsh --config "C:\Users\jose0\OneDrive\Documentos\Terminal Theme\1_shell.omp.json" | Invoke-Expression

# Mejoras visuales y autocompletado
Import-Module PSReadLine -Force
Import-Module Terminal-Icons

# Autocompletado para Chocolatey
$ChocolateyProfile = "$env:ChocolateyInstall\helpers\chocolateyProfile.psm1"
if (Test-Path $ChocolateyProfile) {
    Import-Module $ChocolateyProfile
}

# Activar Conda si está instalado
#region conda initialize
# !! Contents within this block are managed by 'conda init' !!
if (Test-Path "C:\Users\jose0\anaconda3\Scripts\conda.exe") {
    (& "C:\Users\jose0\anaconda3\Scripts\conda.exe" "shell.powershell" "hook") | Out-String | ? { $_ } | Invoke-Expression
}
#endregion
```

### Resultado

- La terminal PowerShell carga sin errores.
- Oh My Posh muestra el prompt con colores e íconos.
- Los listados de archivos (`ls`, `Get-ChildItem`) muestran íconos.
- Compatible con Conda y Chocolatey para autocompletado.
- Íconos visibles en la terminal de Windows y en VSCode tras configurar la fuente Nerd Font.

---

¡Listo! Ahora tienes todo el proceso documentado y la configuración recomendada para una terminal PowerShell moderna y funcional.
