<p align="center">
  <img src="blackbird_design.png" alt="BlackBird Design" width="100%" />
</p>

# BlackBird Launcher — Releases & Distribution
### *Canal oficial de distribución de versiones compiladas (APK) y actualizaciones OTA para autorradios Android*

<p align="center">
  <a href="../../releases/latest">
    <img src="https://img.shields.io/badge/Descargar-Última_Versión_APK-007ACC?style=for-the-badge&logo=android&logoColor=white" alt="Descargar Última Versión" />
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Plataforma-Android%209.0%2B%20(API%2028)-3DDC84?style=flat-square&logo=android&logoColor=white" alt="Android 9.0+" />
  <img src="https://img.shields.io/badge/Hardware-AC8257%20%2F%20Jancar-C23B22?style=flat-square" alt="Hardware Objetivo" />
  <img src="https://img.shields.io/badge/Canal-Oficial_OTA-orange?style=flat-square" alt="Canal OTA" />
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/Licencia-GPLv3-blue.svg?style=flat-square" alt="Licencia GPLv3" />
  </a>
  <a href="PRIVACY.md">
    <img src="https://img.shields.io/badge/Privacidad-RGPD_Compliant-green.svg?style=flat-square" alt="Privacidad RGPD" />
  </a>
  <a href="https://github.com/RubyCrack/BL-launcher">
    <img src="https://img.shields.io/badge/Código_Fuente-GitHub-181717?style=flat-square&logo=github&logoColor=white" alt="Código Fuente en GitHub" />
  </a>
</p>

---

## 📥 Descarga e Instalación

### Método 1: Actualización Automática OTA (Recomendado)
Si ya tienes instalada una versión de **BlackBird Launcher**:
1. Conecta la autorradio o pantalla a una red Wi-Fi o datos móviles.
2. Abre **Ajustes ➔ Acerca de (o Actualización de Software)** en BlackBird Launcher.
3. Pulsa **COMPROBAR**: la aplicación detectará automáticamente si hay una nueva versión publicada en este repositorio y te guiará para descargarla e instalarla directamente en pantalla.

### Método 2: Instalación Manual por APK
1. Descarga el paquete `app-release.apk` de la versión más reciente desde la sección [Releases](../../releases/latest).
2. Copia el archivo a una memoria USB (formateada en FAT32 o NTFS) o descárgalo directamente desde el navegador web del coche.
3. Conecta el USB a la pantalla, abre el explorador de archivos nativo, pulsa sobre el APK e instala la aplicación (habilita la opción de *Instalar aplicaciones de fuentes desconocidas* si el sistema lo solicita).
4. Pulsa el botón **HOME** de la pantalla o del volante y selecciona **BlackBird** como aplicación de inicio predeterminada (*«Siempre»*).

---

## 🚗 Matriz de Compatibilidad de Hardware

| Componente / Subsistema | Nivel de Compatibilidad | Especificaciones Técnicas |
| :--- | :---: | :--- |
| **Android Base** | **Nativo** | Compatible con Android 9.0 (API 28) hasta Android 12.0. |
| **SoC Objetivo** | **Nativo** | Optimizado específicamente para plataformas MediaTek AC8257, Autochips y Jancar. |
| **Arquitecturas CPU** | **Nativo** | Compatible con ARM64 (`arm64-v8a`) y ARMv7 (`armeabi-v7a`). |
| **Radio FM/AM Física** | **Soportado** | Control directo del chip sintonizador de la placa base vía interfaz Binder IPC. |
| **Bluetooth OEM** | **Soportado** | Manos libres y streaming mediante el servicio de audio del fabricante. |
| **Bus CAN Nativo** | **Soportado** | Lectura pasiva de telemetría (odómetro, combustible), marcha atrás e iluminación. |
| **Posicionamiento GNSS** | **Nativo** | Velocímetro por satélite con interpolación inercial continua. |

---

## 🔒 Integridad Criptográfica (SHA-256)

Cada paquete APK publicado en las [Releases](../../releases/latest) incluye su correspondiente suma de verificación criptográfica (**SHA-256**). Se recomienda verificar la huella antes de instalar:

* **En macOS / Linux:**
  ```bash
  shasum -a 256 app-release.apk
  ```
* **En Windows (PowerShell):**
  ```powershell
  Get-FileHash app-release.apk -Algorithm SHA256
  ```

Compara el hash generado con el publicado en las notas de la versión para confirmar que el binario no ha sufrido corrupciones ni alteraciones.

---

## 📋 Registro de Versiones Reciente

### [v3.7.4 (Release Oficial)](../../releases/tag/v3.7.4)
* **Coordinador de Reanudación (`HomeResumeCoordinator`):** Sincronización atómica de perfiles al volver a primer plano y supresión síncrona en marcha atrás.
* **Telemetría de Velocidad:** Reconciliación de frescura al reanudar y distinción matemática entre 0 km/h y señal no disponible (`--`).
* **Privacidad Estricta en CAN y Bluetooth:** Anonimización de números de teléfono, contactos y exclusión de coordenadas GPS privadas en registros de diagnóstico.
* **Escuchador de Notificaciones:** Sistema de arrendamiento atómico (`NotificationListenerLease`) y filtrado ultrarrápido (<1 µs) de guiado (Maps/Waze).
* **Clima Resiliente:** Detección de saltos temporales del reloj (`ClockSanity`) y fusión inmutable CAN-Bus + API meteorológica.
* **Consumo Cero en Segundo Plano:** Suspensión síncrona de animaciones y liberación de capas GPU en pausa (0.0% CPU/GPU).

---

## ⚖️ Marco Legal, Privacidad y Seguridad Vial

El uso de los binarios distribuidos en este repositorio está sujeto a las siguientes condiciones y descargos:

| Documento | Descripción |
| :--- | :--- |
| **[TERMS.md](TERMS.md)** | **Términos de Uso y Seguridad Vial:** Prohibición estricta de manipular la pantalla en marcha, descargo sobre la naturaleza referencial del velocímetro GPS, advertencia de legalidad de avisadores de radares (OpenStreetMap) y exención de responsabilidad civil (*AS IS*). |
| **[PRIVACY.md](PRIVACY.md)** | **Política de Privacidad (RGPD / GDPR):** Declaración de ausencia de analítica o rastreadores de terceros (sin Firebase, sin AdMob). Tratamiento local de velocidad y audio FFT en memoria, y transferencias efímeras a Open-Meteo y Overpass. |
| **[LICENSE](LICENSE)** | **Licencia de Software:** Distribuido bajo la licencia [GNU General Public License v3.0 (GPLv3)](LICENSE). |
| **[ATTRIBUTIONS.md](ATTRIBUTIONS.md)** | **Atribuciones de Terceros:** Licencia de Bases de Datos Abiertas (ODbL) de © OpenStreetMap, datos de Open-Meteo, tipografía Montserrat (SIL OFL 1.1) y librerías de código abierto. |
| **[SECURITY.md](SECURITY.md)** | **Política de Seguridad:** Procedimiento para el reporte responsable de incidencias de seguridad a través de GitHub Security Advisories. |

---

<p align="center">
  <sub>BlackBird Launcher — Desarrollado por <a href="https://github.com/RubyCrack">RubyCrack</a> bajo licencia <a href="LICENSE">GPLv3</a>.<br>Código fuente completo disponible en <a href="https://github.com/RubyCrack/BL-launcher">RubyCrack/BL-launcher</a>.</sub>
</p>
