# Política de Privacidad — BlackBird Launcher (BL-Launcher)

*Última actualización: 23 de septiembre de 2026*  
*Aplicable a: BlackBird Launcher (versiones 3.x y superiores)*  
*Conforme al Reglamento General de Protección de Datos de la Unión Europea (RGPD / GDPR - Reglamento UE 2016/679) y a la Ley Orgánica 3/2018 (LOPDGDD).*

---

## 1. Responsable del Tratamiento

El responsable del desarrollo y mantenimiento de **BlackBird Launcher** (en adelante, "la Aplicación") es Rubén (`RubyCrack`).
* **Repositorio de código:** [RubyCrack/BL-launcher](https://github.com/RubyCrack/BL-launcher)
* **Repositorio de distribución y releases:** [RubyCrack/BL-launcher-releases](https://github.com/RubyCrack/BL-launcher-releases)
* **Canal de contacto y soporte:** Mediante incidencias públicas o privadas en el repositorio oficial de GitHub (`https://github.com/RubyCrack/BL-launcher/issues`).

---

## 2. Principio Rector: Privacidad por Diseño y Almacenamiento Cero

BlackBird Launcher es un entorno de inicio (*launcher*) para sistemas de infoentretenimiento y pantallas de automoción (*Head Units*) basadas en Android 9.0 o superior.

La arquitectura de la Aplicación ha sido diseñada bajo el principio de **privacidad por diseño y por defecto** (*Privacy by Design and by Default*):
* **No requiere registro ni creación de cuenta de usuario.**
* **No dispone de servidores propios ni bases de datos en la nube** para recopilar información de los usuarios.
* **No incluye herramientas de telemetría invasiva, analítica de terceros ni redes publicitarias** (no contiene Google Firebase Analytics, Google Crashlytics, Facebook SDK, AdMob ni similares).
* Todos los ajustes de personalización, perfiles de conductor y configuraciones se almacenan **única y exclusivamente en la memoria local del dispositivo**.

---

## 3. Permisos del Dispositivo y Finalidad del Tratamiento

Para poder operar como lanzador del sistema e interactuar con el hardware del vehículo, la Aplicación solicita determinados permisos en Android. Cada uno de ellos se utiliza estrictamente para las funciones descritas:

### A. Ubicación (`ACCESS_FINE_LOCATION` y `ACCESS_COARSE_LOCATION`)
* **Finalidad principal (Local):** Cálculo en tiempo real de la velocidad satelital del vehículo (velocímetro analógico y digital en el salpicadero) mediante fusión de sensores GNSS. Este procesamiento se realiza íntegramente en la CPU del dispositivo.
* **Finalidad secundaria (Consultas a servicios externos):**
  1. **Previsión meteorológica:** Envío de las coordenadas geográficas (latitud y longitud) a la API pública de **Open-Meteo** para obtener temperatura, estado del cielo y previsión.
  2. **Avisador de cinemómetros (radares):** Envío de un radio de coordenadas geográficas a la API pública de **Overpass (OpenStreetMap)** para descargar la posición de los radares fijos de la zona.
* **Garantía de privacidad:** **En ningún caso se guardan historiales de ruta, trayectos realizados, paradas o patrones de movimiento.** Las coordenadas se descartan de la memoria RAM tras completar la consulta.

### B. Micrófono / Entrada de Audio (`RECORD_AUDIO`)
* **Finalidad:** Alimentar de forma visual el **espectro gráfico de ondas / ecualizador visual** del salpicadero mientras se reproduce música.
* **Garantía de privacidad:**
  * El flujo de audio se procesa en tiempo real mediante transformadas de Fourier (FFT) en memoria volátil para obtener barras de amplitud gráfica.
  * **La Aplicación NUNCA graba, almacena, comprime ni transmite voz o sonido.** No se genera ningún archivo de audio en el almacenamiento ni se envía muestra alguna a través de la red.

### C. Almacenamiento y Archivos Multimedia (`READ_EXTERNAL_STORAGE`, `WRITE_EXTERNAL_STORAGE`, `READ_MEDIA_IMAGES`)
* **Finalidad:** Permitir al usuario seleccionar fondos de pantalla personalizados de su almacenamiento local/USB y leer carátulas e información ID3 de pistas de música almacenadas en el vehículo.
* **Garantía de privacidad:** La Aplicación no lee ni indexa archivos personales ajenos a las carpetas explícitamente configuradas por el usuario.

### D. Aplicaciones Instaladas y Estadísticas de Uso (`QUERY_ALL_PACKAGES`, `PACKAGE_USAGE_STATS`)
* **Finalidad:** Función esencial de cualquier *launcher*: enumerar las aplicaciones instaladas en el sistema para generar el cajón de aplicaciones (*App Drawer*), permitir accesos directos rápidos y detectar qué aplicación multimedia está en primer plano.
* **Garantía de privacidad:** La lista de aplicaciones instaladas reside en la memoria local y jamás se transmite fuera del dispositivo.

### E. Bluetooth (`BLUETOOTH`, `BLUETOOTH_CONNECT`, `BLUETOOTH_ADMIN`)
* **Finalidad:** Conexión con el chip manos libres y audio A2DP del vehículo para mostrar el título de la canción en reproducción y el estado de la conexión.
* **Garantía de privacidad:** Los identificadores de hardware (como direcciones MAC) y nombres de agenda telefónica son anonimizados u ofuscados en cualquier traza interna de depuración.

### F. Acceso a Internet y Estado de Red (`INTERNET`, `ACCESS_NETWORK_STATE`)
* **Finalidad:** Permitir las consultas a los servicios meteorológicos, descarga de radares y comprobación de actualizaciones de la aplicación.

---

## 4. Transferencias de Datos a Terceros (Servicios Externos)

Al utilizar funciones que requieren conexión a Internet, la Aplicación interactúa con los siguientes servicios de terceros. Al realizar una petición HTTP, el servidor de destino recibe técnicamente la dirección IP pública del dispositivo y las cabeceras estándar de red:

| Servicio | Proveedor | Finalidad | Datos enviados | Política de privacidad del tercero |
| :--- | :--- | :--- | :--- | :--- |
| **Open-Meteo** | Open-Meteo GmbH (Alemania / UE) | Previsión del tiempo | Latitud y longitud aproximadas | [Política de Open-Meteo](https://open-meteo.com/en/features#privacy) |
| **Overpass API** | OpenStreetMap Foundation (Reino Unido / UE) | Nodos de radares fijos | Coordenadas de búsqueda / Bounding box | [Política de OSMF](https://wiki.osmfoundation.org/wiki/Privacy_Policy) |
| **GitHub Releases API** | GitHub, Inc. / Microsoft (EE. UU.) | Comprobación de actualizaciones OTA | Solicitud HTTP GET estándar de versión | [Política de GitHub](https://docs.github.com/es/site-policy/privacy-policies/github-general-privacy-statement) |

*Ninguno de estos servicios recibe datos de identificación personal, nombres, cuentas de correo o identificadores de hardware del vehículo.*

---

## 5. Base Jurídica del Tratamiento (RGPD)

El tratamiento de los datos técnicos descritos se fundamenta en:
* **Ejecución de la relación contractual o de uso (Art. 6.1.b RGPD):** Necesario para que la aplicación preste las funciones solicitadas por el usuario (mostrar velocidad, tiempo y aplicaciones).
* **Consentimiento expreso del usuario (Art. 6.1.a RGPD):** Otorgado mediante el diálogo de permisos del sistema operativo Android para el acceso al GPS, audio y almacenamiento.

---

## 6. Derechos del Usuario (Derechos ARCO / RGPD)

De conformidad con los artículos 15 a 22 del RGPD, el usuario ostenta los derechos de acceso, rectificación, supresión, limitación del tratamiento y portabilidad.

**Nota práctica sobre el ejercicio de derechos:** Dado que BlackBird Launcher **no almacena ningún dato personal en servidores externos ni perfiles de usuario**, el ejercicio de sus derechos de supresión y revocación de datos se materializa de forma inmediata y autónoma por el propio usuario:
1. Revocando los permisos concedidos desde los Ajustes del sistema de Android (`Ajustes > Aplicaciones > BlackBird Launcher > Permisos`).
2. Borrando los datos y la memoria caché de la aplicación (`Ajustes > Aplicaciones > BlackBird Launcher > Almacenamiento > Borrar datos`).
3. Desinstalando la Aplicación del dispositivo.

---

## 7. Cambios en esta Política

Cualquier modificación futura de esta política se publicará en los repositorios oficiales de GitHub indicados en el encabezado. Se recomienda revisar el documento periódicamente o al instalar actualizaciones importantes.

---

## English Summary (Non-binding Convenience Translation)

* **Zero Cloud Storage:** BlackBird Launcher does not run any private servers or user databases. All settings and driver profiles remain on your vehicle's head unit.
* **No Tracking / No Analytics:** No Firebase, Google Analytics, telemetry SDKs, or advertising networks are included.
* **Location Data:** GPS coordinates are processed locally for the speedometer and sent transiently to Open-Meteo (weather) and Overpass API (OSM speed cameras). No travel history or location breadcrumbs are saved.
* **Audio Visualizer:** The `RECORD_AUDIO` permission is solely used to compute real-time visual waveform spectrum bars on the dashboard. No voice or audio is ever recorded, stored, or streamed.
* **OTA Updates:** Automated update checks query the public GitHub API for the latest release.
