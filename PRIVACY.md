# Información de privacidad — BlackBird Launcher

*Última actualización: 23 de septiembre de 2026*  
*Aplicable a: BlackBird Launcher 3.x*

Este documento describe el tratamiento observado en la versión indicada. No afirma una certificación de conformidad con el RGPD. Los permisos de Android autorizan acceso técnico al dispositivo; por sí solos no constituyen consentimiento para todos los tratamientos.

## 1. Responsable y contacto

El proyecto lo mantiene Rubén (`RubyCrack`): [código fuente](https://github.com/RubyCrack/BL-launcher) y [descargas](https://github.com/RubyCrack/BL-launcher-releases). Las incidencias generales pueden comunicarse en [GitHub Issues](https://github.com/RubyCrack/BL-launcher/issues). **Las incidencias son públicas: no publiques allí ubicaciones, registros ni otros datos personales.** Actualmente no se publica un canal privado para solicitudes relativas a datos personales; esta vía de contacto sigue pendiente de habilitarse.

## 2. Datos que procesa y conserva la aplicación

BlackBird Launcher no exige cuenta, no usa un servidor propio de perfiles y no integra Firebase Analytics, Crashlytics ni publicidad. Esto no significa que todo el tratamiento sea efímero ni que los servicios de terceros carezcan de registros.

| Función | Datos y conservación local |
| :--- | :--- |
| Perfiles y ajustes | Preferencias locales, incluidas coordenadas predeterminadas si el usuario las configura. Permanecen hasta que se cambian o se borran los datos de la aplicación. |
| Velocidad y telemetría | Lecturas GPS, CAN u OBD para mostrar el estado del vehículo. El cálculo ordinario se realiza en el dispositivo. |
| Radares | Caché privada `radar_cache.json` con hasta cuatro zonas de consulta: coordenadas del centro, fecha de descarga y radares cercanos. No es un registro continuo de cada trayecto. Se reemplazan las zonas más antiguas al añadir otras; el archivo puede permanecer hasta borrar los datos de la aplicación. |
| Tiempo | Caché en preferencias con temperatura, estado, ciudad y momento de la última consulta. No guarda las coordenadas GPS de cada consulta en esa caché, aunque pueden existir coordenadas configuradas en el perfil. |
| Diagnóstico | Los registros CAN pueden iniciarse automáticamente según el ajuste, que actualmente está activado por defecto. Se guardan en almacenamiento privado con cuotas de archivos; los informes de fallos también se guardan localmente. Los textos de errores o diagnósticos pueden contener información contextual: revísalos antes de compartirlos. |
| Exportaciones | Un registro exportado por el usuario a Descargas, USB u otra ubicación deja de depender del almacenamiento privado de la app. Borrar o desinstalar la app no garantiza borrar esas copias. |

Los registros CAN se limitan por número de archivos; los informes de fallo conservan hasta diez archivos. No se promete un plazo temporal único de eliminación para los archivos locales. Borrar los datos de la aplicación elimina sus archivos privados y preferencias; las copias exportadas deben borrarse por separado.

## 3. Permisos y funciones

- **Ubicación (`ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION`):** velocímetro, mapa, tiempo y aviso de radares. Una consulta de tiempo o radares puede enviar ubicación a un tercero; el mapa usa Google Maps SDK cuando se abre.
- **Audio (`RECORD_AUDIO`):** el visualizador de radio puede analizar mediante FFT la salida de audio que Android permite capturar durante la reproducción. La implementación no crea archivos de voz o sonido ni envía muestras de audio a un servidor. Según el dispositivo y la sesión de audio, la señal capturada puede incluir audio audible de otras aplicaciones; el permiso no se usa para una función de grabación de micrófono.
- **Almacenamiento e imágenes:** selección de fondos y acceso a contenido multimedia usado por las funciones de la app. Android puede conceder un alcance de lectura mayor que una sola carpeta; la aplicación no declara un escaneo general de archivos personales.
- **Aplicaciones y estadísticas de uso:** selección de apps, accesos directos e identificación de la app multimedia activa. La lista se procesa localmente.
- **Acceso a notificaciones:** si el usuario habilita el servicio de escucha, la app puede recibir notificaciones del sistema. Usa datos de apps de navegación compatibles para mostrar indicaciones; el servicio también recibe metadatos técnicos de las notificaciones antes de filtrarlas.
- **Bluetooth y sesiones multimedia:** estado de conexión y metadatos de reproducción para la interfaz. Los registros diagnósticos tratan de ocultar números, contactos e identificadores; revisa cualquier exportación antes de compartirla.
- **Internet:** consultas de tiempo y radares, mapa y comprobación/descarga de actualizaciones.

## 4. Servicios externos

Las solicitudes de red revelan al destino la dirección IP y datos técnicos de conexión. Una IP o unas coordenadas pueden constituir datos personales según el contexto. La app no controla la conservación que hagan los proveedores.

| Servicio | Uso y datos enviados o recogidos | Información del proveedor |
| :--- | :--- | :--- |
| [Open-Meteo](https://open-meteo.com/en/terms) — Suiza | La petición meteorológica incluye latitud y longitud con seis decimales. Open-Meteo indica que sus registros técnicos pueden contener coordenadas y que los elimina tras 90 días. | [Términos y privacidad](https://open-meteo.com/en/terms) |
| [Overpass API](https://wiki.openstreetmap.org/wiki/Overpass_API) — instancia `overpass-api.de`, operada por FOSSGIS | La consulta de radares incluye el centro de búsqueda con latitud y longitud y un radio de 10 km. OpenStreetMap Foundation licencia los datos; no opera esta instancia. | [Instancias Overpass](https://wiki.openstreetmap.org/wiki/Overpass_API) |
| [Google Maps SDK](https://developers.google.com/maps/documentation/android-sdk/play-data-disclosure) | Se usa cuando se muestra el mapa. Google informa de recogida automática de IP, identificador del dispositivo, metadatos y métricas de fallo por el SDK; pueden aplicarse otros tratamientos de Google Maps. | [Información del SDK](https://developers.google.com/maps/documentation/android-sdk/play-data-disclosure) y [privacidad de Google](https://policies.google.com/privacy) |
| Geocodificación de Android | La resolución de ciudad a partir de coordenadas usa `Geocoder`. Según el dispositivo, este servicio puede usar red y un proveedor del sistema. | [Documentación Android](https://developer.android.com/reference/android/location/Geocoder) |
| [GitHub Releases](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement) — EE. UU. | Petición de versión y descarga de APK al comprobar o instalar actualizaciones; GitHub recibe IP y datos técnicos de la petición. | [Privacidad de GitHub](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement) |

La app no envía deliberadamente nombres, correo o identificadores del vehículo a Open-Meteo u Overpass. Esto no convierte en anónimos la IP o la ubicación transmitidas.

## 5. Base jurídica y derechos

El permiso de Android es un control de acceso, no una base jurídica universal del artículo 6 del RGPD. La base aplicable debe evaluarse por finalidad y por servicio antes de presentar este documento como declaración completa de conformidad. En particular, el acceso a ubicación y las consultas externas requieren información clara y control efectivo para el usuario.

Cuando corresponda el RGPD, pueden ejercerse los derechos de acceso, rectificación, supresión, oposición, limitación y portabilidad, así como presentar una reclamación ante la autoridad de protección de datos competente. Revocar permisos, borrar datos o desinstalar la aplicación detiene o elimina tratamientos locales futuros, pero no borra automáticamente registros ya conservados por terceros ni copias exportadas. Consulta también las políticas de los proveedores indicados arriba.

## 6. Cambios

Las versiones nuevas de esta información se publicarán en los repositorios del proyecto. Las condiciones de los servicios externos pueden cambiar independientemente.

## English summary

BlackBird Launcher does not require an account or run its own profile server. It keeps settings, optional configured coordinates, weather data, up to four radar query zones and local diagnostic files on the device. Weather and radar requests send precise location to external providers. Google Maps SDK and Android Geocoder may process additional technical or location data when used. Android permissions alone are not a blanket GDPR consent. Uninstalling the app does not delete third-party logs or files the user exported.
