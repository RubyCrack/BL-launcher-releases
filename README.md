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
  <img src="https://img.shields.io/badge/Versión-v3.7.7_Estable-success?style=flat-square" alt="Versión Estable" />
  <a href="../../releases">
    <img src="https://img.shields.io/badge/Canal_Beta-v3.8.0--beta-orange?style=flat-square" alt="Canal Beta" />
  </a>
  <img src="https://img.shields.io/badge/Plataforma-Android%209.0%2B%20(API%2028)-3DDC84?style=flat-square&logo=android&logoColor=white" alt="Android 9.0+" />
  <img src="https://img.shields.io/badge/Hardware-AC8257%20%2F%20Jancar-C23B22?style=flat-square" alt="Hardware Objetivo" />
  <img src="https://img.shields.io/badge/Canal-Oficial_OTA-orange?style=flat-square" alt="Canal OTA" />
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/Licencia-GPLv3-blue.svg?style=flat-square" alt="Licencia GPLv3" />
  </a>
  <a href="PRIVACY.md">
    <img src="https://img.shields.io/badge/Privacidad-Documentada-green.svg?style=flat-square" alt="Información de privacidad" />
  </a>
  <a href="https://github.com/RubyCrack/BL-launcher">
    <img src="https://img.shields.io/badge/Código_Fuente-GitHub-181717?style=flat-square&logo=github&logoColor=white" alt="Código Fuente en GitHub" />
  </a>
</p>

---

## 📥 Descarga e Instalación

### Método 1: Actualización Automática OTA (Recomendado)
Si ya tienes instalada cualquier versión de **BlackBird Launcher**:
1. Conecta la autorradio a una red Wi-Fi o punto de acceso móvil.
2. Abre **Ajustes ➔ Sistema ➔ Actualización** en BlackBird Launcher.
3. Elige tu canal preferido:
   * **Estable:** Recibe exclusivamente versiones definitivas y consolidadas para el día a día.
   * **Beta:** Recibe versiones preliminares (*pre-releases*) con las últimas características antes de su despliegue general.
4. Pulsa **COMPROBAR**: la aplicación detectará automáticamente la versión más reciente en este repositorio, verificará su integridad criptográfica (SHA-256) y te guiará para instalarla directamente en pantalla.

* **Reanudación ante cortes de contacto:** Si el motor se apaga o se pierde la cobertura 4G/Wi-Fi durante la descarga, el archivo parcial no se pierde. Al volver a encender el coche, la descarga se restaura en pausa y reanuda exactamente desde el último byte descargado mediante cabeceras HTTP `Range`.

> [!IMPORTANT]
> **Seguridad en Marcha:** Por normativa de seguridad HMI, las operaciones de actualización y confirmación de instalación requieren que el vehículo se encuentre completamente detenido.

---

### Método 2: Instalación Manual por APK
1. Descarga el paquete `app-release.apk` de la versión más reciente desde la sección [Releases](../../releases/latest).
2. Copia el archivo a una memoria USB (formateada en FAT32 o NTFS) o descárgalo directamente desde el navegador de la autorradio.
3. Conecta el USB a la pantalla, abre el explorador de archivos nativo y pulsa sobre el APK para instalarlo (habilita *«Instalar aplicaciones de fuentes desconocidas»* si el sistema lo solicita).
4. Pulsa el botón físico o táctil **HOME** de la consola y selecciona **BlackBird** como aplicación de inicio predeterminada (*«Siempre»*).

---

## 🚗 Matriz de Compatibilidad de Hardware

| Componente / Subsistema | Nivel de Compatibilidad | Especificaciones Técnicas |
| :--- | :---: | :--- |
| **Android Base** | **Nativo** | Compatible desde Android 9.0 (API 28) hasta Android 12.0. |
| **SoC Objetivo** | **Nativo** | Optimizado específicamente para procesadores MediaTek AC8257, Autochips y Jancar. |
| **Arquitecturas CPU** | **Nativo** | Compatible con ARM64 (`arm64-v8a`) y ARMv7 (`armeabi-v7a`). |
| **Resoluciones HMI** | **Nativo** | Formatos panorámicos de automoción (1024×600 y 1280×720) a 160 dpi. |
| **Radio FM/AM Física** | **Soportado** | Control directo del chip sintonizador de la placa base vía interfaz Binder IPC. |
| **Bluetooth OEM** | **Soportado** | Manos libres y streaming mediante el servicio de audio del fabricante. |
| **Bus CAN Nativo** | **Soportado** | Lectura pasiva de telemetría (odómetro, combustible), marcha atrás e iluminación. |
| **Posicionamiento GNSS** | **Nativo** | Fusión satelital continua con amortiguación de fluctuaciones y auto-recuperación de proveedores. |
| **Telemetría Torque / OBD-II** | **Soportado** | Lectura de parámetros de motor en tiempo real mediante adaptadores ELM327 (Bluetooth y USB). |

> [!NOTE]
> **Aviso de Rendimiento y Plataforma de Validación:**
> BlackBird Launcher está calibrado, perfilado y probado exhaustivamente en bancos de pruebas reales con hardware **MediaTek AC8257 / Jancar en Android 9.0 (API 28)**. Aunque la aplicación es técnicamente compatible con otros sistemas Android (hasta Android 12), **el rendimiento óptimo (cadencia calibrada a 30 FPS con aguja amortiguada por delta de tiempo, bajo consumo de CPU y protección térmica activa en tres fases) y la integración directa de hardware (control del sintonizador analógico por IPC, decodificación pasiva de bus CAN y sincronización LED de consola)** solo pueden garantizarse en el hardware objetivo de referencia. En autorradios con otros procesadores (como Allwinner, Rockchip o Unisoc) o ROMs personalizadas de otros fabricantes, el comportamiento, la compatibilidad con el bus CAN y la fluidez pueden variar significativamente.

---

## 🔒 Integridad Criptográfica (SHA-256)

El actualizador OTA comprueba automáticamente el hash criptográfico de cada archivo antes de ofrecer su instalación. Si descargas manualmente, puedes verificar el **SHA-256** del APK frente al publicado en las notas de la release:

* **En macOS / Linux:**
  ```bash
  shasum -a 256 app-release.apk
  ```
* **En Windows (PowerShell):**
  ```powershell
  Get-FileHash app-release.apk -Algorithm SHA256
  ```

---

## 📋 Registro de Versiones Reciente

### [v3.7.7 (Release Oficial)](../../releases/tag/v3.7.7)
* **Telemetría y Diagnóstico OBD-II Integrado:** Integración completa con adaptadores ELM327 (Bluetooth y USB), lectura de parámetros en vivo (temperatura de refrigerante, carga de motor, admisión, voltaje, presión MAP y acelerador) con reconexión automática ante cortes de encendido.
* **Blindaje de Ciclo de Vida y Reposo:** Aislamiento transaccional ante cortes de alimentación (`powerRevision`), eliminación de hilos zombi de radio FM y purga de llamadas de reproducción al apagar el contacto.
* **Ergonomía HMI en Ajustes:** Reorganización en pestañas laterales temáticas inspiradas en CarPlay, soporte para 9 identidades cromáticas completas y controles de brillo desacoplados.
* **Validación Masiva:** Certificada con más de 2.710 pruebas unitarias y de integración superadas (0 fallos).

### [v3.7.6 "Jazz" (Release Oficial)](../../releases/tag/v3.7.6)
* **Rediseño Integral de Multimedia:** Efecto de vinilo giratorio en capa hardware dedicada (`LAYER_TYPE_HARDWARE`), halo dinámico de carátula desacoplado y compatibilidad con carátulas de alta resolución sin fugas de memoria.
* **Navegador Visual de Listas Spotify:** Explorador táctil de playlists, vista de cola y persistencia segura de tokens sin sobrecoste de CPU.
* **Superficies Neutras de 16dp:** Estandarización de radios de esquina, elevación de contraste diurno (`#CCFFFFFF`) y protección del velocímetro contra tintes de alerta.

### [v3.7.5 (Release Oficial)](../../releases/tag/v3.7.5)
* **Motor de Radares Headless:** Detección de cinemómetros continua en segundo plano unificada para todos los cuadros (Classic, Card y Performance), sin depender de Google Maps ni consumir memoria de vídeo.
* **Aguja Analógica Amortiguada:** Interpolación cinemática fluida mediante animador finito por delta de tiempo, eliminando tirones entre tramas de señal GPS y CAN.
* **Actualizador OTA Integrado:** Comprobación, descarga reanudable con soporte HTTP Range, verificación SHA-256 y selector táctil de canales (**Estable** vs **Beta**).
* **Tipografía Inter y Estética CarPlay:** Estandarización de la tipografía **Inter** (Regular, Medium, Bold), esquinas redondeadas uniformes a 16dp y elevación de contraste diurno (`#CCFFFFFF`).

---

## ⚖️ Marco Legal, Privacidad y Seguridad Vial

Esta distribución incluye la licencia, la información de privacidad y los avisos siguientes:

| Documento | Descripción |
| :--- | :--- |
| **[TERMS.md](TERMS.md)** | **Aviso de Uso y Seguridad Vial:** Reglas de atención al volante, límites de velocidad y radares, y condiciones de la licencia GPLv3 en la medida permitida por la ley. |
| **[PRIVACY.md](PRIVACY.md)** | **Información de Privacidad:** Almacenamiento local, permisos, diagnósticos y consultas a Open-Meteo, Overpass, Google Maps y GitHub. |
| **[LICENSE](LICENSE)** | **Licencia de Software:** Distribuido bajo la licencia [GNU General Public License v3.0 (GPLv3)](LICENSE). |
| **[ATTRIBUTIONS.md](ATTRIBUTIONS.md)** | **Atribuciones de Terceros:** Licencia de Bases de Datos Abiertas (ODbL) de © OpenStreetMap, datos de Open-Meteo, tipografía Inter (SIL OFL 1.1) de Rasmus Andersson, alias de compatibilidad Montserrat y librerías de código abierto. |
| **[SECURITY.md](SECURITY.md)** | **Política de Seguridad:** Procedimiento para el reporte responsable de incidencias de seguridad a través de GitHub Security Advisories. |

---

<p align="center">
  <sub>BlackBird Launcher — Desarrollado por <a href="https://github.com/RubyCrack">RubyCrack</a> bajo licencia <a href="LICENSE">GPLv3</a>.<br>Código fuente completo disponible en <a href="https://github.com/RubyCrack/BL-launcher">RubyCrack/BL-launcher</a>.</sub>
</p>
