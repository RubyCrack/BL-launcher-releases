# Política de Seguridad — BlackBird Launcher

*Última actualización: 23 de septiembre de 2026*

La seguridad y la integridad del sistema de infoentretenimiento de su vehículo son de máxima prioridad en el desarrollo de **BlackBird Launcher**. Al operar directamente sobre el hardware del automóvil y capas de comunicación IPC (Android Binder / MCU / Bus CAN), aplicamos prácticas continuas de desarrollo seguro y minimización de vectores de ataque.

---

## 1. Versiones Compatibles

Actualmente se proporciona soporte activo de correcciones de seguridad para las siguientes versiones:

| Versión | Compatible / Recibe parches |
| :--- | :---: |
| **v3.7.x** | Sí |
| **< v3.7.0** | No (se recomienda actualizar a la última versión disponible) |

---

## 2. Áreas de Especial Sensibilidad

Agradecemos especialmente el reporte responsable de vulnerabilidades relativas a:
* **Interacción con el Microcontrolador (MCU):** Posibles desbordamientos de búfer o tramas maliciosas transmitidas a través del puerto serie / IPC del bus CAN.
* **Comunicaciones IPC / Binder:** Intentos de interceptación o inyección de intents desde aplicaciones de terceros no privilegiadas.
* **Procesamiento de Red:** Validaciones en la deserialización de respuestas JSON de APIs públicas (Open-Meteo, Overpass API, GitHub Releases OTA).
* **Fuga de Información:** Registro involuntario de coordenadas GPS o identificadores de hardware en logs del sistema (`logcat`).

---

## 3. Notificación Responsable de Vulnerabilidades

Si detecta una posible vulnerabilidad de seguridad en BlackBird Launcher, le solicitamos que **NO abra una incidencia pública** (*issue*) en el repositorio. En su lugar, siga el procedimiento de divulgación coordinada:

1. **GitHub Security Advisory:** Envíe un reporte confidencial a través de la pestaña **Security > Advisories > Report a vulnerability** en el repositorio oficial:  
   `https://github.com/RubyCrack/BL-launcher/security/advisories/new`
2. **Contacto directo:** Si no dispone de acceso a GitHub Security Advisories, contacte de forma privada con el mantenedor (`RubyCrack`) a través de un canal privado de GitHub.

### Información a incluir en el reporte:
* Versión exacta de BlackBird Launcher afectada.
* Modelo de pantalla / SoC (*Head Unit*, por ejemplo AC8257, Jancar) y versión de Android.
* Descripción detallada del fallo y pasos para reproducirlo (*Proof of Concept* si procede).
* Impacto potencial estimado en el dispositivo o en la seguridad del vehículo.

---

## 4. Compromiso de Respuesta

* **Reconocimiento inicial:** Responderemos a su reporte en un plazo máximo de **48 a 72 horas**.
* **Evaluación y parche:** Se coordinará el análisis del impacto y la publicación de una versión parcheada (*hotfix*) en el repositorio de descargas antes de hacer pública la divulgación.
