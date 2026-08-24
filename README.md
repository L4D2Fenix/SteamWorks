SteamWorks
==========

Exposing SteamWorks functions to SourcePawn.
____________________________________________

# SteamWorks

Exposing SteamWorks functions to SourcePawn.

## Installation / Instalación

### Instrucciones de Instalación (Español)

1. Ve a la sección de **Releases** de este repositorio y descarga el paquete correspondiente a tu sistema operativo (**Linux** o **Windows**).
2. Extrae el contenido del archivo `.zip`.
3. Copia las carpetas en tu servidor de juego respetando la estructura de SourceMod:

   - Coloca la extensión (`SteamWorks.ext.so` o `SteamWorks.ext.dll`) en:
     `addons/sourcemod/extensions/`
   - Coloca el archivo de inclusión opcional (`SteamWorks.inc`) en:
     `addons/sourcemod/scripting/include/`

4. Reinicia tu servidor o ejecuta el siguiente comando en la consola del servidor para cargar la extensión al vuelo:

   ```text
   sm exts load SteamWorks.ext
   ```

5. Verifica que la extensión se haya cargado correctamente ejecutando:

   ```text
   sm exts list
   ```

   Deberías ver **SteamWorks** en la lista con estado `Loaded`.

### Installation Instructions (English)

1. Navigate to the **Releases** section of this repository and download the archive matching your operating system (**Linux** or **Windows**).
2. Extract the contents of the `.zip` file.
3. Upload the extracted files to your game server following the standard SourceMod directory structure:

   - Place the binary (`SteamWorks.ext.so` or `SteamWorks.ext.dll`) into:
     `addons/sourcemod/extensions/`
   - Place the optional include file (`SteamWorks.inc`) into:
     `addons/sourcemod/scripting/include/`

4. Restart your game server or load the extension dynamically using the server console:

   ```text
   sm exts load SteamWorks.ext
   ```

5. Verify the installation by running:

   ```text
   sm exts list
   ```

   You should see **SteamWorks** listed with status `Loaded`.

## Usage & Development / Uso y Desarrollo

### Para Desarrolladores de Plugins (Español)

Para compilar plugins de SourceMod que utilicen SteamWorks, asegúrate de incluir el archivo de cabecera en tu código fuente `.sp`:

```sourcepawn
#include <sourcemod>
#include <SteamWorks>

public Plugin myinfo =
{
    name = "SteamWorks Test Plugin",
    author = "Community Developer",
    description = "Ejemplo de uso de SteamWorks 1.2.4+",
    version = "1.0.0",
    url = ""
};

public void OnPluginStart()
{
    if (SteamWorks_IsLoaded())
    {
        PrintToServer("[SteamWorks] La extensión está cargada y lista para usarse.");
    }
}
```

#### Nota sobre `SteamWorks_ForceHeartbeat()`

En esta versión (**v1.2.4+**), la llamada `SteamWorks_ForceHeartbeat()` está marcada como obsoleta (`@deprecated`).

Los SDKs modernos de Steam gestionan los *heartbeats* hacia el **Master Server** de forma automática. Ejecutar esta función es totalmente seguro y mantiene la compatibilidad con plugins antiguos, pero internamente realiza una operación vacía (*no-op*).

### For Plugin Developers (English)

To compile SourceMod plugins using SteamWorks, include the header files at the top of your `.sp` source script:

```sourcepawn
#include <sourcemod>
#include <SteamWorks>

public Plugin myinfo =
{
    name = "SteamWorks Test Plugin",
    author = "Community Developer",
    description = "SteamWorks 1.2.4+ usage example",
    version = "1.0.0",
    url = ""
};

public void OnPluginStart()
{
    if (SteamWorks_IsLoaded())
    {
        PrintToServer("[SteamWorks] Extension is loaded and ready for use.");
    }
}
```

#### Note Regarding `SteamWorks_ForceHeartbeat()`

In this release (**v1.2.4+**), `SteamWorks_ForceHeartbeat()` has been marked as `@deprecated`.

Modern Steam SDKs handle **Master Server heartbeats** automatically. Calling this native remains safe for backwards compatibility, but it internally performs a no-op.
