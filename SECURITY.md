# Política de Seguridad — Libertad VZLA

> Libertad VZLA gestiona datos sensibles en un contexto geopolítico de alto riesgo. Este documento define la postura de seguridad del proyecto, el modelo de amenazas, la clasificación de datos, los protocolos de respuesta a incidentes, el programa de divulgación responsable de vulnerabilidades y las cláusulas de protección legal.

---

## 1. Premisa Operativa

La plataforma opera bajo una premisa: **las personas que la utilizan como fuentes podrían enfrentar represalias físicas, legales o sociales si su participación fuera expuesta.** Toda decisión de ingeniería, toda política de acceso y todo proceso editorial se evalúa contra esta premisa.

En Venezuela, entre julio de 2024 y marzo de 2025, se documentaron más de 2.000 detenciones post-electorales, 14 periodistas detenidos arbitrariamente y 566 violaciones a la libertad de prensa (Fuentes: [Foro Penal](https://foropenal.com), [IPYS Venezuela](https://ipysvenezuela.org)). La plataforma fue diseñada para operar en ese entorno.

---

## 2. Marco Normativo de Referencia

Las políticas de seguridad de Libertad VZLA se fundamentan en los siguientes instrumentos normativos. No son referencias genéricas: constituyen la base legal sobre la cual se justifican las decisiones técnicas de protección de datos, fuentes y usuarios.

### 2.1. Constitución de la República Bolivariana de Venezuela (1999)

- **Artículo 28 — Habeas Data y Secreto de Fuentes:**
  > *"Toda persona tiene derecho de acceder a la información y a los datos que sobre sí misma o sobre sus bienes consten en registros oficiales o privados [...] Queda a salvo el secreto de las fuentes de información periodística y de otras profesiones que determine la ley."*

- **Artículo 48 — Secreto e inviolabilidad de las comunicaciones:**
  > *"Se garantiza el secreto e inviolabilidad de las comunicaciones privadas en todas sus formas. No podrán ser interferidas sino por orden de un tribunal competente, con el cumplimiento de las disposiciones legales y preservándose el secreto de lo privado que no guarde relación con el correspondiente proceso."*

- **Artículo 57 — Libertad de expresión (sin censura):**
  > *"Toda persona tiene derecho a expresar libremente sus pensamientos, ideas u opiniones [...] sin que pueda establecerse censura."*

- **Artículo 58 — Derecho a la información veraz e imparcial:**
  > *"Toda persona tiene derecho a la información oportuna, veraz e imparcial, sin censura."*

- **Artículo 60 — Protección de la intimidad y uso de la informática:**
  > *"Toda persona tiene derecho a la protección de su honor, vida privada, intimidad, propia imagen, confidencialidad y reputación. La ley limitará el uso de la informática para garantizar el honor y la intimidad personal y familiar de los ciudadanos y ciudadanas."*

- [Constitución completa — OAS](https://www.oas.org/dil/esp/constitucion_venezuela.pdf)

### 2.2. Derecho Internacional

- **Artículo 19, Declaración Universal de Derechos Humanos** (DUDH, 1948) — [ONU](https://www.un.org/es/about-us/universal-declaration-of-human-rights)
- **Artículo 19, Pacto Internacional de Derechos Civiles y Políticos** (PIDCP, 1966) — [OHCHR](https://www.ohchr.org/es/instruments-mechanisms/instruments/international-covenant-civil-and-political-rights)
- **Observación General Nº 34** del Comité de Derechos Humanos de la ONU (2011) — Protección explícita del periodismo y de las fuentes periodísticas.
- **Artículo 13, Convención Americana sobre Derechos Humanos** (CADH, 1969) — [OAS](https://www.oas.org/dil/esp/1969_Convenci%C3%B3n_Americana_sobre_Derechos_Humanos.pdf)
- **Opinión Consultiva OC-5/85**, Corte Interamericana de DDHH — [Corte IDH](https://www.corteidh.or.cr/docs/opiniones/seriea_05_esp.pdf)
- **Declaración de Principios sobre Libertad de Expresión**, CIDH (2000), Principio 8: reserva de fuentes. — [OAS](https://www.oas.org/es/cidh/expresion/showarticle.asp?artID=26&lID=2)

### 2.3. Protección de Denunciantes

- **Directiva (UE) 2019/1937** — [EUR-Lex](https://eur-lex.europa.eu/legal-content/ES/TXT/?uri=CELEX%3A32019L1937)
- **Principios de Tshwane** (2013) — [Open Society Foundations](https://www.opensocietyfoundations.org/publications/global-principles-national-security-and-freedom-information-tshwane-principles)

### 2.4. Estándares Técnicos y Corporativos

- **ISO/IEC 27001** — Gestión de Seguridad de la Información.
- **ISO/IEC 27701** — Gestión de Información de Privacidad (extensión para PII).
- **ISO/IEC 29147** — Divulgación de vulnerabilidades.
- **OWASP Top 10** (2021) — Riesgos críticos en aplicaciones web. — [OWASP](https://owasp.org/Top10/)
- **Reglamento General de Protección de Datos (RGPD / GDPR)** — Principios de minimización, limitación de acceso y confidencialidad.

---

## 3. Modelo de Amenazas

### 3.1. Actores contemplados

| Actor | Capacidad estimada | Contramedidas |
|:---|:---|:---|
| **Actores estatales** | Vigilancia de red, manipulación DNS, presión legal, interceptación de tráfico, bloqueo de VPN, detención de periodistas | Distribución global sin infraestructura local, cifrado de extremo a extremo, minimización de datos, ausencia de registros IP innecesarios |
| **Atacantes dirigidos** | Robo de credenciales, phishing, ingeniería social | Autenticación fuerte, control de acceso por rol, gestión de sesiones en servidor exclusivamente |
| **Ataques a la cadena de suministro** | Dependencias comprometidas, bibliotecas falsificadas | Auditoría automática de dependencias, bloqueo de versiones, superficie mínima de dependencias |
| **Exfiltración de datos** | Acceso no autorizado a base de datos, abuso de endpoints | Aislamiento de datos por rol a nivel de base de datos, validación de entrada, limitación de velocidad, registro de auditoría |
| **Ataques a la reputación** | Inyección de contenido falso, suplantación de identidad, campañas de desprestigio | Flujo de verificación de doble capa, trazabilidad de auditoría, firma editorial |

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

**Controles:** Cifrado en reposo y en tránsito. Acceso restringido al mínimo de roles necesarios. Nunca se registran en logs. Nunca se almacenan en caché del lado del cliente. Protección amparada por el Artículo 28 de la Constitución de Venezuela (secreto de fuentes) y el Artículo 60 (intimidad y uso de la informática).

### Nivel 2 — Sensible (Protección Alta)

- Perfiles de usuarios registrados (nombres, correos).
- Borradores editoriales y contenido no publicado.
- Registros de auditoría y actividad editorial.
- Tokens de sesión y estado de autenticación.

**Controles:** Cifrado en tránsito. Acceso regulado por políticas a nivel de base de datos. Procesamiento exclusivo en servidor. Expiración automática. Alineado con ISO/IEC 27701 (gestión de PII).

### Nivel 3 — Público (Protección Estándar)

- Artículos y contenido multimedia publicado.
- Contenido informativo de la plataforma.
- Métricas analíticas agregadas y anonimizadas.

**Controles:** Validación de integridad. Distribución mediante red de contenido. Sin información personal embebida.

---

## 5. Controles de Seguridad

### 5.1. Autenticación y Control de Acceso

- Gestión de sesiones exclusivamente en servidor — no se exponen tokens en el navegador.
- Políticas de aislamiento de datos aplicadas a nivel de base de datos sobre todas las tablas.
- Control de acceso basado en roles: `testigo`, `reportero`, `verificador`, `periodista`, `admin`.
- Verificación de autorización en servidor para todas las rutas protegidas y acciones editoriales.
- Ninguna decisión de autorización se delega al cliente.

### 5.2. Protección de Datos

- Todos los secretos de infraestructura se gestionan mediante variables de entorno.
- Comunicación cifrada (HTTPS/TLS) en todos los puntos de acceso.
- Validación de entrada en todos los formularios y acciones del servidor (alineado con OWASP A03:2021 — Injection).
- Sanitización de salida para prevenir inyección de código y ataques cross-site (OWASP A07:2021 — XSS).

### 5.3. Protección de Fuentes

- **Minimización de datos:** Solo se recopila la información estrictamente necesaria (principio de minimización del RGPD, Art. 5.1.c).
- **Sin registro de direcciones IP** en los formularios de reporte.
- **Eliminación de metadatos** en contenido enviado por los ciudadanos.
- **La confidencialidad periodista-fuente es un requisito de arquitectura**, no una decisión discrecional. Amparada por el Artículo 28 de la Constitución de Venezuela, el Principio 8 de la Declaración de la CIDH y la Observación General Nº 34 del Comité de DDHH de la ONU.

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
| **Análisis posterior** | Documentación interna, medidas preventivas, notificación a afectados cuando corresponda | < 7 días |

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

Esta disposición se alinea con las directrices de **FIRST** (Forum of Incident Response and Security Teams) y con la norma **ISO/IEC 29147** para divulgación coordinada de vulnerabilidades.

---

## 8. Cláusulas de Protección Legal

### 8.1. Reserva de Acciones Legales

Libertad VZLA se reserva el derecho de emprender acciones legales civiles y/o penales, en las jurisdicciones aplicables, contra cualquier persona, organización o entidad que:

- **Acceda sin autorización** al código fuente, a la base de datos, a los sistemas de autenticación o a cualquier componente de la infraestructura de la plataforma. Tipificado como acceso indebido bajo legislaciones de delitos informáticos (Ley Especial contra los Delitos Informáticos de Venezuela, Art. 6, Gaceta Oficial Nº 37.313).
- **Extraiga, copie o distribuya** datos de fuentes, testigos o personas registradas en el Registro de Memoria Cívica sin autorización. Constituye violación de la confidencialidad amparada por el Art. 28 de la Constitución de Venezuela y el RGPD.
- **Suplante la identidad** de la plataforma, de sus integrantes o de sus publicaciones con el fin de desinformar o comprometer la credibilidad del proyecto.
- **Utilice el código fuente** para fines de Uso de Producción sin consentimiento previo por escrito, en violación de la Business Source License 1.1.
- **Ejecute ataques** de denegación de servicio, inyección de código, ingeniería social u otras ofensivas técnicas contra la plataforma o sus usuarios.
- **Amenace, hostigue o intimide** a periodistas, fuentes, testigos o colaboradores del proyecto en relación con su participación en la plataforma.

### 8.2. Jurisdicción y Legislación Aplicable

Las acciones legales se podrán ejercer bajo, sin limitarse a:

- **Venezuela:** Constitución de la República Bolivariana de Venezuela (1999), Ley Especial contra los Delitos Informáticos (Gaceta Oficial Nº 37.313, 2001), Código Penal venezolano (delitos contra las personas, difamación, injuria).
- **Internacional:** Computer Fraud and Abuse Act (CFAA, EE.UU.), General Data Protection Regulation (GDPR, Unión Europea), Convenio de Budapest sobre Ciberdelincuencia (2001), legislación de propiedad intelectual aplicable según la jurisdicción del infractor.
- **Sistema Interamericano:** Mecanismos de denuncia ante la Comisión Interamericana de Derechos Humanos (CIDH) y la Corte Interamericana de Derechos Humanos (Corte IDH).

### 8.3. Daños Reclamables

En caso de acción legal, Libertad VZLA podrá reclamar:

- Daños y perjuicios directos e indirectos.
- Lucro cesante derivado de la interrupción del servicio o la pérdida de confianza pública.
- Costos de remediación técnica (restauración de sistemas, auditorías de seguridad post-incidente).
- Honorarios legales y costas procesales.
- Daño moral al equipo editorial y a las personas afectadas.
- Medidas cautelares (cesación inmediata de la actividad infractora).

### 8.4. Cooperación con Autoridades

Libertad VZLA cooperará con las autoridades competentes, organismos internacionales de derechos humanos y entidades de ciberseguridad en la investigación de ataques contra la plataforma, siempre que dicha cooperación no comprometa la identidad de las fuentes ni la confidencialidad de los datos clasificados como Nivel 1.

---

## 9. Revisiones de Seguridad

| Tipo de revisión | Frecuencia |
|:---|:---|
| Auditoría de dependencias | En cada integración de código |
| Monitoreo de alertas de seguridad | Continuo |
| Revisión de políticas de aislamiento de datos | En cada cambio de esquema |
| Evaluación completa de seguridad | Trimestral |
| Pruebas de penetración | Pre-lanzamiento, luego anual |
| Revisión de cumplimiento normativo | Semestral |

---

*Última actualización: 25 de marzo de 2026*  
*Responsable: Luis Sambrano — soyluissambrano@gmail.com*
