# Política de Seguridad — Libertad VZLA

> Libertad VZLA gestiona datos sensibles en un contexto geopolítico de alto riesgo. Este documento define la postura de seguridad del proyecto, el modelo de amenazas, la clasificación de datos, los protocolos de respuesta a incidentes y el programa de divulgación responsable de vulnerabilidades.

---

## 1. Premisa Operativa

La plataforma opera bajo una premisa: **las personas que la utilizan como fuentes podrían enfrentar represalias físicas, legales o sociales si su participación fuera expuesta.** Toda decisión de ingeniería, toda política de acceso y todo proceso editorial se evalúa contra esta premisa.

Esta no es una declaración retórica. En Venezuela, entre julio de 2024 y marzo de 2025, se documentaron más de 2.000 detenciones post-electorales, 14 periodistas detenidos arbitrariamente y 566 violaciones a la libertad de prensa (Fuentes: Foro Penal, IPYS Venezuela). La plataforma fue diseñada para operar en ese entorno.

---

## 2. Marco Normativo de Referencia

Las políticas de seguridad de Libertad VZLA se alinean con los siguientes marcos normativos internacionales:

- **Artículo 19, Declaración Universal de Derechos Humanos (DUDH):** Derecho a investigar, recibir y difundir información sin limitación de fronteras.
- **Artículo 19, Pacto Internacional de Derechos Civiles y Políticos (PIDCP):** Libertad de buscar, recibir y difundir informaciones e ideas de toda índole.
- **Observación General Nº 34, Comité de DDHH de la ONU:** Confirma que la protección de fuentes periodísticas es componente fundamental de la libertad de expresión.
- **Directiva (UE) 2019/1937:** Protección de denunciantes — establece que los canales de denuncia deben garantizar confidencialidad y que los denunciantes son fuentes esenciales del periodismo de investigación.
- **Principios de Tshwane (2013):** Seguridad nacional y derecho a la información — los denunciantes que revelan información de interés público no deben enfrentar represalias.
- **Reglamento General de Protección de Datos (RGPD / GDPR):** Principios de minimización de datos, limitación de acceso y confidencialidad en el tratamiento de información personal.

---

## 3. Modelo de Amenazas

### 3.1. Actores contemplados

| Actor | Capacidad estimada | Contramedidas aplicadas |
|:---|:---|:---|
| **Actores estatales** | Vigilancia de red, manipulación DNS, presión legal, interceptación de tráfico, detención de periodistas | Distribución global sin infraestructura local, comunicaciones cifradas, minimización de datos, ausencia de registros IP innecesarios |
| **Atacantes dirigidos** | Robo de credenciales, phishing, ingeniería social | Autenticación fuerte, control de acceso por rol, gestión de sesiones en servidor |
| **Ataques a la cadena de suministro** | Dependencias comprometidas, bibliotecas falsificadas | Auditoría automática de dependencias, bloqueo de versiones, superficie mínima de dependencias |
| **Exfiltración de datos** | Acceso no autorizado a base de datos, abuso de API | Aislamiento de datos por rol a nivel de base de datos, validación de entrada, limitación de velocidad, registro de auditoría |

### 3.2. Superficie de exposición

- **Acceso público (sin autenticación):** Páginas informativas y feed de noticias (solo lectura).
- **Acceso protegido (autenticación + rol requerido):** Panel editorial, flujos de verificación, administración, Registro de Memoria Cívica.

---

## 4. Clasificación de Datos

### Nivel 1 — Crítico (Protección Máxima)

- Identidades y datos de contacto de fuentes y testigos.
- Contenido y metadatos de denuncias.
- Credenciales de autenticación de usuarios.
- Claves y secretos de infraestructura.

**Controles:** Cifrado en reposo y en tránsito. Acceso restringido al mínimo de roles necesarios. Nunca se registran en logs. Nunca se almacenan en caché del lado del cliente.

### Nivel 2 — Sensible (Protección Alta)

- Perfiles de usuarios registrados (nombres, correos).
- Borradores editoriales y contenido no publicado.
- Registros de auditoría y actividad del CMS.
- Tokens de sesión y estado de autenticación.

**Controles:** Cifrado en tránsito. Acceso regulado por políticas a nivel de base de datos. Procesamiento exclusivo en servidor. Expiración automática.

### Nivel 3 — Público (Protección Estándar)

- Artículos y contenido multimedia publicado.
- Contenido informativo de la plataforma.
- Métricas analíticas agregadas y anonimizadas.

**Controles:** Validación de integridad. Distribución mediante red de contenido. Sin información personal embebida.

---

## 5. Controles de Seguridad

### 5.1. Autenticación y Control de Acceso

- Gestión de sesiones exclusivamente en servidor — no se exponen tokens en el navegador.
- Políticas de aislamiento de datos (Row-Level Security) aplicadas a nivel de base de datos sobre todas las tablas.
- Control de acceso basado en roles: `testigo`, `reportero`, `verificador`, `periodista`, `admin`.
- Verificación de autorización en servidor para todas las rutas protegidas y acciones editoriales.
- Ninguna decisión de autorización se delega al cliente.

### 5.2. Protección de Datos

- Todos los secretos de infraestructura se gestionan mediante variables de entorno — cero credenciales en código.
- Comunicación cifrada (HTTPS) en todos los puntos de acceso.
- Validación de entrada en todos los formularios y acciones del servidor.
- Sanitización de salida para prevenir inyección de código y ataques cross-site.

### 5.3. Protección de Fuentes

- **Minimización de datos:** Solo se recopila la información estrictamente necesaria para el funcionamiento del sistema.
- **Sin registro de direcciones IP** en los formularios de reporte.
- **Eliminación de metadatos** en contenido enviado por los ciudadanos.
- **La confidencialidad periodista-fuente es un requisito de arquitectura**, no una decisión discrecional.

Estos principios se alinean con el Artículo 19 del PIDCP, la Observación General Nº 34 del Comité de DDHH de la ONU, y los Principios de Tshwane sobre seguridad nacional y derecho a la información.

---

## 6. Respuesta a Incidentes

### 6.1. Protocolo

| Fase | Acción | Tiempo de respuesta |
|:---|:---|:---|
| **Detección** | Monitoreo continuo, detección de anomalías, reportes de usuarios | Continuo |
| **Evaluación** | Clasificación de severidad (Crítica / Alta / Media / Baja) | < 1 hora |
| **Contención** | Aislamiento de sistemas afectados, revocación de credenciales comprometidas | < 4 horas |
| **Erradicación** | Análisis de causa raíz, despliegue de corrección | < 24 horas |
| **Recuperación** | Restauración de servicio, verificación de integridad de datos | < 48 horas |
| **Análisis posterior** | Documentación interna, medidas preventivas | < 7 días |

### 6.2. Clasificación de Severidad

- **Crítica:** Filtración de datos de fuentes o testigos, compromiso de autenticación, caída de producción.
- **Alta:** Escalamiento de privilegios, exposición de datos sensibles, ejecución de código malicioso en páginas autenticadas.
- **Media:** Divulgación de información no personal, falsificación de solicitudes, redirecciones abiertas.
- **Baja:** Violaciones de mejores prácticas, filtraciones menores de información no clasificada.

---

## 7. Divulgación Responsable de Vulnerabilidades

### 7.1. Cómo reportar

Si descubre una vulnerabilidad de seguridad en la plataforma:

1. **NO** cree un Issue público en GitHub.
2. **NO** divulgue la vulnerabilidad públicamente antes de que sea corregida.
3. Envíe un correo a: **soyluissambrano@gmail.com**

### 7.2. Información a incluir

- Pasos para reproducir la vulnerabilidad.
- Evaluación de impacto (qué datos o sistemas se ven afectados).
- Corrección sugerida (si aplica).
- Su información de contacto para seguimiento.

### 7.3. Tiempos de Respuesta

| Acción | Plazo |
|:---|:---|
| Confirmación de recepción del reporte | **48 horas** |
| Evaluación inicial | **72 horas** |
| Desarrollo de corrección | **7 días** (crítica), **14 días** (alta), **30 días** (media/baja) |
| Divulgación pública | Posterior al despliegue y verificación de la corrección |

### 7.4. Protección al Investigador (Safe Harbor)

No se emprenderán acciones legales contra investigadores de seguridad que:

- Actúen de buena fe.
- Eviten la destrucción de datos o la interrupción del servicio.
- No accedan a datos más allá de lo necesario para demostrar la vulnerabilidad.
- Reporten los hallazgos de forma oportuna y confidencial.

Esta disposición se alinea con las mejores prácticas de divulgación coordinada de vulnerabilidades establecidas por FIRST (Forum of Incident Response and Security Teams) y con los estándares ISO/IEC 29147.

---

## 8. Revisiones de Seguridad

| Tipo de revisión | Frecuencia |
|:---|:---|
| Auditoría de dependencias | En cada integración de código |
| Monitoreo de alertas de seguridad | Continuo |
| Revisión de políticas de aislamiento de datos | En cada cambio de esquema |
| Evaluación completa de seguridad | Trimestral |
| Pruebas de penetración | Pre-lanzamiento, luego anual |

---

*Última actualización: 25 de marzo de 2026*  
*Responsable: Luis Sambrano — soyluissambrano@gmail.com*
