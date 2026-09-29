<p align="center">
  <img src="docs/images/blackbird_design.png" alt="BlackBird Design" width="100%" />
</p>

# BlackBird Launcher
### *Entorno de inicio automotriz de alto rendimiento para sistemas de infoentretenimiento Android*

<p align="center">
  <a href="../../releases/latest">
    <img src="https://img.shields.io/badge/Release-v3.7.5-007ACC?style=flat-square&logo=android&logoColor=white" alt="Versión 3.7.5" />
  </a>
  <img src="https://img.shields.io/badge/Platform-Android%209.0%2B%20(API%2028)-3DDC84?style=flat-square&logo=android&logoColor=white" alt="Android 9.0+" />
  <img src="https://img.shields.io/badge/Target_Hardware-AC8257%20%2F%20Jancar-C23B22?style=flat-square" alt="Hardware Objetivo" />
  <img src="https://img.shields.io/badge/Language-Kotlin%201.9-7F52FF?style=flat-square&logo=kotlin&logoColor=white" alt="Kotlin" />
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/License-GPLv3-blue.svg?style=flat-square" alt="Licencia GPLv3" />
  </a>
  <a href="docs/PRIVACY.md">
    <img src="https://img.shields.io/badge/Privacy-Documentada-green.svg?style=flat-square" alt="Información de privacidad" />
  </a>
</p>

---

## Visión General

**BlackBird Launcher** es un entorno de inicio de alto rendimiento y bajo consumo diseñado específicamente para sistemas de infoentretenimiento (*Head Units*) basados en Android 9+. Construido bajo los principios de diseño de interfaces persona-máquina (**HMI automotriz**), prioriza la mínima distracción al volante, tiempos de respuesta instantáneos y un control directo de la capa de hardware del vehículo: **decodificación pasiva de bus CAN, control de sintonizador físico FM/AM y enlace Bluetooth nativo**.

El sistema sustituye las interfaces genéricas de fábrica por un entorno unificado con gestión multiusuario, instrumentación animada continua y fluida, cartografía vectorial estabilizada, avisos de cinemómetros sin mapa activo, telemetría del vehículo y actualizador OTA integrado.

---

## Pilares de Arquitectura e Ingeniería

### 1. Gestión Multiusuario y Arranque Determinado
* **Perfiles Aislados:** Cada conductor dispone de preferencias persistidas independientemente (fuentes de medios, emisoras de radio, estilo de instrumentación, disposición de widgets y mapeo de aplicaciones).
* **Arranque Secuencial Rápido (`MainActivity`):** Pasarela pura de selección de perfil sin cargas de red ni geocodificadores bloqueantes. Incluye temporizador configurable para inicio automático sin intervención táctil.
* **Sincronización Atómica en Reanudación (`HomeResumeCoordinator`):** Resuelve condiciones de carrera al alternar entre aplicaciones y sincroniza perfiles en memoria y disco antes de activar controladores pesados.

| Selección de Perfil (`MainActivity`) | Administración de Conductores (`AdminActivity`) |
| :---: | :---: |
| ![Selección de Perfil](docs/images/screen_main_profiles.png) | ![Administración de Perfiles](docs/images/screen_admin_profiles.png) |
| *Visualización de reloj, clima, velocímetro y cuenta atrás de inicio* | *Gestión de conductores, asignación de launcher por usuario y auto-arranque* |

---

### 2. Salpicaderos Especializados de Conducción
BlackBird incorpora tres interfaces de instrumentos alternables en caliente según el tipo de trayecto:

| Salpicadero por Tarjetas (*Card Dashboard*) | Salpicadero Clásico (*Classic Dashboard*) |
| :---: | :---: |
| ![Modo Tarjetas](docs/images/dashboard_tarjetas.png) | ![Modo Clásico](docs/images/dashboard_clasico.png) |
| *Cartografía vectorial en vivo, auto-zoom estabilizado (EMA), carátula dinámica y widget de seguridad en ruta* | *Instrumentación analógica deportiva con aguja de movimiento continuo, lectura digital inmediata, brújula y dock rápido* |

<p align="center">
  <b>Salpicadero de Rendimiento (<i>Performance Dashboard</i>)</b><br>
  <img src="docs/images/dashboard_rendimiento.png" alt="Modo Rendimiento" width="92%" /><br>
  <i>Telemetría de motor en tiempo real (Presión de turbo, temperatura de refrigerante, carga motor, admisión, voltaje, aceite, mariposa y MAP) junto a ordenador de a bordo con compensación de reposo</i>
</p>

---

### 3. Detección Universal de Cinemómetros (`Headless Radar Runtime`)
* **Independencia del Motor Gráfico:** La detección opera mediante un runtime desacoplado (`RadarRuntimeController`) unificado para todos los salpicaderos, procesando coordenadas, rumbo y relevancia angular sin requerir una vista de mapa activa ni consumir memoria de vídeo (VRAM).
* **Semántica Estricta (`SafeRouteView`):** Máquina de estados tipada que distingue formalmente entre ausencia de datos (`UNAVAILABLE`), búsqueda activa (`SEARCHING`), datos en caché (`STALE_CACHE`) y zona despejada (`READY`), eliminando falsos positivos de vía libre.
* **Optimización de Red y Particionado:** Consulta geográfica optimizada a nodos físicos de OpenStreetMap a 10 km con reducción del 70% en transferencia de datos y latencia inferior a 0,6 segundos, indexados mediante celdas espaciales de 0.01°.
* **Resiliencia en Ruta:** Retención automática de datos de zona ante pérdidas de cobertura, deduplicación atómica de entregas y aviso inmediato ante pérdida de señal GPS (>15s).

---

### 4. Integración Directa de Hardware Automotriz (OEM)
* **Bus CAN Pasivo:** Monitorización pasiva y segura del estado del vehículo (nivel de combustible, odómetro, autonomía y velocidad satelital sincronizada).
* **Control Físico de Radio FM/AM:** Comunicación por IPC con el sintonizador analógico de la placa base (`JancarRadioClient`), prescindiendo de transmisiones de datos por red.
* **Sincronización de Iluminación de Consola:** Control en tiempo real del bus de iluminación para sincronizar la tonalidad de la botonera física de la consola con la paleta activa.
* **Prioridad Absoluta en Marcha Atrás:** Detección síncrona de marcha atrás en el microcontrolador (`JancarMcuEventMonitor`), suprimiendo el renderizado de mapas y efectos gráficos para priorizar la fluidez de la cámara de aparcamiento.

---

### 5. Eficiencia Térmica y Ciclo de Vida en Segundo Plano
* **Menos trabajo gráfico en pausa:** Suspensión síncrona de animadores continuos, ondas de radio, rotación de vinilo y fondos dinámicos al minimizar la aplicación.
* **Filtrado Rápido de Notificaciones (<1 µs):** Descarte temprano de eventos del sistema ajenos a aplicaciones de navegación (Google Maps y Waze) para eliminar pausas del Garbage Collector.
* **Protección ante Desajustes Horarios (`ClockSanity`):** Detección y omisión de marcas temporales futuras tras arranques en frío o desconexiones de batería antes de sincronizar satélites GPS.
* **Scroll Fluido sin Bloqueos de I/O:** Caché de paleta de temas en memoria (`WifiAdapter`) para garantizar desplazamientos fluidos en listas sin lecturas a disco por celda.

---

### 6. Actualizaciones OTA Integradas en la App (`OtaUpdater`)
* **Gestión Directa en Pantalla:** Comprobación, descarga reanudable con soporte de cabeceras HTTP `Range` e instalación guiada de nuevas versiones directamente desde **Ajustes ➔ Sistema ➔ Actualización** sin depender de memorias USB.
* **Canales Seleccionables (Estable vs. Beta):** Selector táctil que permite optar por versiones definitivas oficiales o probar compilaciones preliminares de forma segura.
* **Seguridad Criptográfica:** Verificación estricta de suma SHA-256 contrastada contra la API de GitHub Releases, comprobación de firma APK y coincidencia de `versionCode` antes de ofrecer la instalación.

---

## Ajustes y Ergonomía HMI

El diseño de la interfaz adopta los principios de claridad y baja distracción inspirados en CarPlay:

* **Tipografía Moderna Inter:** Migración integral a la familia tipográfica **Inter** (Regular, Medium, Bold) en todos los salpicaderos, widgets y menús, garantizando lectura nítida a gran distancia y con ángulos de visión exigentes.
* **Superficies Neutras y Radios de 16dp:** Tarjetas con esquinas redondeadas uniformes a 16dp (`bg_settings_card.xml`, `bg_toggle_container.xml`, `bg_zoom_btn.xml`), eliminando anidamientos visuales innecesarios.
* **Elevación de Contraste Diurno:** Texto secundario elevado a `#CCFFFFFF` (80% blanco) y optimización de contraste en seekbars, interruptores y botones de acción en modo claro.
* **Esquemas Cromáticos y Temas:** Nueve identidades cromáticas completas, incluyendo los nuevos **Sport Red** y **Cyber Purple** con mapas vectoriales JSON dedicados.
* **Seguridad HMI en Datos de Conducción:** El velocímetro digital (`txtVelocidad`, `txtKmh`) queda protegido contra el tinte rojo en el tema Sport Red, manteniéndose en blanco puro para reservar el color rojo exclusivamente a alertas críticas.
* **Acabado Gráfico Realzado («Glassmorphism Lite»):** Acabado visual satinado de alta gama con acento dinámico de carátula seguro (WCAG AA) y preservación de tonos térmicos del clima.

| Configuración de Salpicadero | Paletas Cromáticas y Modos |
| :---: | :---: |
| ![Ajustes de Inicio](docs/images/settings_screen.png) | ![Temas Visuales](docs/images/settings_tema.png) |
| *Selección de estilo visual, calidad gráfica y salpicaderos* | *Esquemas cromáticos adaptativos, temas diurnos y nocturnos* |

| Sincronización LED de Botonera | Mapeo de Acciones Rápidas |
| :---: | :---: |
| ![Iluminación LED](docs/images/settings_iluminacion.png) | ![Mapeo de Aplicaciones](docs/images/settings_funciones.png) |
| *Control por tramas de iluminación física del salpicadero* | *Asignación de accesos directos para navegación, llamadas y multimedia* |

<p align="center">
  <b>Cajón de Aplicaciones con Identidad Canónica (64 bits)</b><br>
  <img src="docs/images/app_drawer.png" alt="Cajón de Aplicaciones" width="85%" /><br>
  <i>Resolución inequívoca de aplicaciones del sistema OEM que comparten paquete mediante hashes combinados de componente</i>
</p>

---

## Matriz de Compatibilidad de Plataforma

| Capa / Componente | Nivel de Soporte | Especificaciones Técnicas |
| :--- | :---: | :--- |
| **Sistema Operativo** | **Nativo** | Android 9.0 (API 28) hasta Android 12.0. |
| **Plataforma SoC** | **Nativo** | MediaTek AC8257 / Autochips / Jancar. |
| **Arquitectura CPU** | **Nativo** | ARM64 (aarch64) y ARMv7 (armeabi-v7a). |
| **Radio FM/AM Física** | **Soportado** | Sintonizador analógico integrado vía interfaz IPC Binder. |
| **Bluetooth Manos Libres** | **Soportado** | Stack de audio y llamadas OEM con anonimización de diagnósticos. |
| **Bus CAN Nativo** | **Soportado** | Decodificador CAN compatible con emisión estructurada. |
| **Servicios de Cartografía** | **Soportado** | Google Maps SDK con soporte de estilos vectoriales personalizados diurnos/nocturnos. |
| **Posicionamiento GNSS** | **Nativo** | Fusión sensorial satelital con auto-recuperación de proveedores y filtro EMA. |
| **Telemetría Torque / OBD-II**| **Opcional** | Conexión con adaptadores ELM327 (Bluetooth/USB) para parámetros de motor. |

> [!NOTE]
> **Aviso de Rendimiento y Plataforma de Validación:**
> BlackBird Launcher ha sido probado y ajustado en bancos reales sobre hardware **MediaTek AC8257 / Autochips / Jancar bajo Android 9.0 (API 28)**. Aunque técnicamente es compatible e instalable en otros dispositivos Android (hasta versión 12.0), **un comportamiento equilibrado (movimiento fluido en la instrumentación, respuesta ágil y consumo contenido de recursos)** así como la **integración directa de bajo nivel (sintonizador FM/AM físico por IPC Binder, decodificación pasiva de tramas CAN y sincronización LED de consola)** solo pueden asegurarse en esta plataforma de referencia, que es donde se han llevado a cabo las pruebas de desarrollo. En autorradios con procesadores o arquitecturas distintas (como Allwinner, Rockchip o Unisoc) o capas de personalización propietarias de otros fabricantes, el rendimiento, la fluidez y las funciones dependientes del hardware del vehículo pueden variar.

---

## Privacidad y Seguridad de Datos

BlackBird Launcher aplica políticas estrictas de privacidad por diseño en entornos automotrices:
* **Minimización de ubicación en diagnósticos:** El registro CAN omite coordenadas GPS absolutas. La caché local de radares conserva hasta cuatro centros de consulta; consulta la [información de privacidad](docs/PRIVACY.md).
* **Ofuscación de Identificadores:** El número de bastidor (VIN) se procesa exclusivamente como indicador booleano de presencia. Los nombres de agenda, números de teléfono y direcciones MAC de Bluetooth se anonimizan en trazas del sistema.
* **Operación 100% Desconectada:** El velocímetro por satélite, la radio analógica, la reproducción local y la telemetría operan de forma autónoma sin requerir conectividad de datos activa.

---

## Entorno de Desarrollo y Verificación

El proyecto sigue una metodología de desarrollo dirigida por contratos (*Contract-Driven Development*), verificando la estabilidad de cada componente mediante pruebas unitarias y de integración que superan las **1.950 pruebas automatizadas** (1.957 tests en verde):

```bash
# Compilación de la variante de desarrollo
./gradlew assembleDebug

# Ejecución de la suite completa de pruebas unitarias y de contrato
./gradlew testDebugUnitTest

# Verificación de compilación de código fuente Kotlin
./gradlew compileDebugKotlin
```

---

## Documentación Técnica

Para información detallada sobre la arquitectura interna, modelos de memoria, protocolos de bus CAN y directrices de ingeniería:
* [Arquitectura y Guías Técnicas](docs/README.md)
* [Notas Técnicas de la Versión v3.7.5 (Oficial)](docs/release_notes_v3_7_5.md)
* [Notas Técnicas de la Versión v3.7.4](docs/release_notes_v3_7_4.md)

---

## Licencia y Términos Legales

El uso, distribución y desarrollo de BlackBird Launcher se rigen por los siguientes acuerdos y normativas:

* **Licencia de Código Abierto:** Distribuido bajo los términos de la [GNU General Public License v3.0 (GPLv3)](LICENSE).
* **Compatibilidad y Rendimiento de Hardware:** Rendimiento garantizado exclusivamente en la plataforma de desarrollo y pruebas de referencia (MediaTek AC8257 / Jancar, Android 9.0). En otros procesadores o sistemas, el comportamiento y la fluidez pueden variar.
* **Información de privacidad:** Datos locales, diagnósticos y servicios externos descritos en [docs/PRIVACY.md](docs/PRIVACY.md). La app no incluye analítica ni publicidad propia; los SDK y servicios externos tienen sus propias prácticas.
* **Aviso de Uso y Seguridad Vial:** Advertencias de conducción, límites de la velocidad mostrada y avisos de radares en [docs/TERMS.md](docs/TERMS.md).
* **Atribuciones y Licencias de Terceros:** Reconocimiento de datos comunitarios © OpenStreetMap (ODbL), Open-Meteo, tipografía Inter (SIL OFL) de Rasmus Andersson, alias de compatibilidad Montserrat y librerías en [docs/ATTRIBUTIONS.md](docs/ATTRIBUTIONS.md).
* **Política de Seguridad:** Directrices para el reporte responsable de vulnerabilidades en [SECURITY.md](SECURITY.md).
