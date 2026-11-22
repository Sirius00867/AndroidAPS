# Paso 2 · Compilar e instalar la 4.0.0

Compila la 4.0.0 con el mismo método que usaste la primera vez. La wiki distingue cuatro:

| Método original | Qué hacer para la 4.0.0 |
| --- | --- |
| Navegador, **AAPS Builder** | En tu repositorio privado (normalmente `my-aaps`), abre la página *Build AAPS*, elige la versión 4.0.0 y descarga la app desde GitHub. No hay fork que sincronizar. |
| Navegador, **fork + archivo de preparación** | Ejecutas el workflow **AAPS-CI** en tu fork (`AndroidAPS` en tu cuenta) y el APK aparece en tu Google Drive. Sigue la página oficial [Update with a browser (fork)](https://androidaps.readthedocs.io/en/latest/Maintenance/UpdateBrowserBuild.html). |
| **Android Studio** | Sigue la página oficial [Update with Android Studio](https://androidaps.readthedocs.io/en/latest/Maintenance/UpdateComputerBuild.html). |
| **Línea de comandos** | Usa las mismas instrucciones que en tu primera compilación por línea de comandos, pero trae los cambios nuevos con `git`. |

En el código, la etiqueta `4.0.0` apunta al commit `f77abd9b82` (merge de la PR #5448) y declara `appVersion = "4.0.0"`. La compilación usa Java 21 (`JavaVersion.VERSION_21`) y Gradle 9.8.2; si compilas en local y ves un error de JVM de Gradle, revisa que Android Studio use un JDK 21.

## Firma: el punto que más problemas da

Firma la 4.0.0 con **el mismo keystore y el mismo alias** que la versión instalada. Android solo deja instalar encima si la firma coincide, y es la única forma de conservar la base de datos y los ajustes. Si la firma no coincide, Android te obligará a desinstalar, y eso borra todo lo que hay en la app.

## Instalación

- Instala el APK nuevo **encima** de la versión actual. **No desinstales** primero. La propia wiki lo resume así: para no perder el historial, actualiza siempre, nunca desinstales y reinstales.
- Si usas reloj, actualiza también la app de Wear con el APK de la misma compilación. La app del reloj se ha reescrito; consulta la página "AAPS for Wear OS" de la wiki si algo no conecta.

## Verificación de desarrolladores de Android

Google está introduciendo una verificación que, en la mayoría de teléfonos, bloquea instalar apps de desarrolladores no registrados, también desde un archivo APK como el de AAPS. Según la página oficial [Android developer verification](https://androidaps.readthedocs.io/en/latest/SettingUpAaps/TransferringAndInstallingAaps.html#android-developer-verification):

- Compilar AAPS no cambia, y tu keystore tampoco.
- La app ya instalada sigue funcionando: la comprobación solo ocurre al instalar o actualizar.
- Desde el 30-09-2026 se aplica en Brasil, Indonesia, Singapur y Tailandia. Google indica que esta primera fase no cubre la instalación directa de un APK.
- En el resto del mundo, España incluida, no cambia nada antes de 2027.

La wiki recomienda preparar ya un método de instalación gratuito, para no descubrir el bloqueo el día que una actualización falle. Con ordenador, el método es ADB: con el teléfono conectado por USB y la depuración USB activada, `adb install -r <nombre-del-apk>.apk` actualiza AAPS conservando todos sus datos y ajustes. Los pasos completos están en la página enlazada.

Siguiente: [Paso 3 · Comprobar e importar](03-verificar-e-importar.md)
