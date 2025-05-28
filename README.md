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
al final tendrás tu archivo de configuración `Microsoft.PowerShell_profile.ps1` como:

```powershell
oh-my-posh init pwsh --config "C:\Users\jose0\OneDrive\Documentos\Terminal Theme\1_shell.omp.json" | Invoke-Expression

Import-Module Terminal-Icons
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

¡Listo! Ya tienes un entorno PowerShell visualmente enriquecido y totalmente personalizado con Oh My Posh.

---

## Nota sobre los íconos en la terminal de VSCode

Por defecto, la terminal integrada de VSCode utiliza el tema predeterminado, por lo que es posible que los íconos de Oh My Posh **no se muestren correctamente**. Para que los íconos aparezcan en la terminal de VSCode, debes cambiar la fuente de la terminal por una Nerd Font, como **CaskaydiaCove Nerd Font** que instalaste previamente.

### Pasos para cambiar la fuente de la terminal en VSCode:

1. Abre VSCode.
2. Ve a **Archivo > Preferencias > Configuración** (o usa `Ctrl + ,`).
3. En la barra de búsqueda escribe: `terminal.integrated.fontFamily`.
4. En el campo correspondiente a la configuración, escribe el nombre exacto de la fuente Nerd Font que instalaste, por ejemplo:
5. Cierra y vuelve a abrir la terminal integrada (`Ctrl + ``) para que los cambios se apliquen.

Después de este cambio, los íconos deberían mostrarse correctamente en la terminal integrada de VSCode.

---

### Video de referencia

Para más detalles y una guía visual sobre cómo personalizar la terminal de Windows y la terminal integrada en VSCode, puedes ver este video:

[![Customize Windows Terminal and VS Code Terminal](https://img.youtube.com/vi/FUwEh8vh9mw/hqdefault.jpg)](https://www.youtube.com/watch?v=FUwEh8vh9mw)
