Kathleen Abigail Argueta Gómez
20245083
Desarrollo de Aplicaciones Móviles

Bitácora de Errores - Verificación de Entorno Flutter

Error 1: Carencia de dependencias de compilación

Síntoma:
 Al ejecutar flutter run, el compilador arrojó el mensaje literal Error: Unable to find suitable Visual Studio toolchain. Adicionalmente, la ejecución de flutter doctor evidenció la falta de Android SDK y la carga de trabajo de C++ en Visual Studio.  
Causa identificada:
 El entorno local carece de las herramientas de compilación subyacentes necesarias para construir binarios nativos para Windows y Android. 
 
Solución aplicada:
Para evitar un bloqueo en el flujo de desarrollo y cumplir con las tareas de interfaz, se redirigió el objetivo de compilación hacia la web seleccionando Edge (web), aprovechando la capacidad multiplataforma del framework. 

Verificación: Se comprobó la resolución del problema al observar la aplicación renderizándose correctamente en el navegador Microsoft Edge, permitiendo realizar exitosamente pruebas de estado mediante Hot Reload y Hot Restart.

Error 2: Colisión de procesos en directorio de caché

Síntoma:
La terminal arrojó múltiples excepciones de tipo PathNotFoundException: Directory listing failed al buscar directorios en .dart_tool\chrome-device\, seguido de advertencias Failed to remove al intentar ejecutar flutter clean.  

Causa identificada:
El servicio de sincronización en la nube (OneDrive) ejecutó bloqueos de lectura/escritura sobre los archivos temporales y efímeros generados por Flutter, impidiendo que el motor liberara o sobrescribiera la caché de compilación.  

Solución aplicada:
Se identificó que los procesos en segundo plano mantenían secuestrado el directorio. La mitigación consistió en aislar el entorno de desarrollo de las carpetas sincronizadas en tiempo real y limpiar el hilo de ejecución para liberar los recursos bloqueados.  

Verificación:
Se logró recuperar la capacidad de compilar y enlazar los cambios de código, inyectando la lógica de incremento de dos en dos y el botón de reinicio al estado del contador.

Declaración de uso de Inteligencia Artificial

Durante el desarrollo de esta sesión, utilicé la IA como herramienta de apoyo técnico y tutoría para superar bloqueos de configuración y comprender los conceptos de estado en Flutter, asegurándome de entender cada línea y proceso aplicado. El apoyo se centró en las siguientes áreas:

1. Diagnóstico y alternativas de entorno: Ante el error de compilación por la falta de Visual Studio toolchain, la IA me explicó que la causa raíz era la ausencia de las dependencias nativas de C++. En lugar de obligarme a detener el trabajo, me orientó estratégicamente para compilar el proyecto en Edge (web) y así poder continuar con la guía.  
   
2. Asistencia conceptual (Regla de la IA): Para la tarea de hacer que el botón incrementara de dos en dos, la IA no me entregó el código directamente. Me explicó cómo funciona el operador ++ internamente, lo que me permitió deducir por mi cuenta el uso del operador matemático += 2 para modificar el estado del contador.  
   
3. Resolución de conflictos de directorios: Cuando enfrenté el error PathNotFoundException al ejecutar flutter clean, la IA analizó el log y diagnosticó una colisión de procesos de lectura/escritura ocasionada por la sincronización en tiempo real de OneDrive. Me guió paso a paso para limpiar los procesos bloqueados y aislar el entorno de desarrollo.
   
4. Estructuración de redacción técnica: Me apoyó en la redacción de la bitácora de errores. La IA me ayudó a transformar los mensajes de la consola en diagnósticos técnicos precisos y profesionales, elevando la calidad de la documentación.