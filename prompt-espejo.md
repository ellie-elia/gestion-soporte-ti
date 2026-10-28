# Prompt espejo

Herramienta usada: Claude (una sola conversación compartida, iniciada el 2026-10-28).

Rol asumido por la IA: consultor senior de ingeniería de software, administración de sistemas y documentación técnica, siguiendo el prompt proporcionado por el docente para revisar críticamente el repositorio y proponer mejoras.

---

## 1. Comprensión del repositorio

El repositorio documenta la atención del incidente **INC-01 — Falla de inicio de equipo portátil** (Lenovo IdeaPad 320-14ISK). Contiene:

- Texto del ticket recibido por correo (`01-ticket/`).
- Datos del equipo tomados del BIOS + hipótesis sin confirmar (`02-investigacion/`).
- Pruebas realizadas P1–P5 con objetivo, procedimiento, resultado y conclusión (`03-pruebas/`).
- Fotos del equipo, BIOS, desarmado y proceso de preparación de la USB con la ISO (`04-evidencias/`, dos .docx).
- Bitácora cronológica, estado del incidente y siguientes pasos para el relevo.

Lo que pretende demostrar: trazabilidad del trabajo hecho hasta ahora, con evidencia física/digital para cada afirmación, para que otro equipo pueda continuar sin partir de cero.

## 2. Fortalezas verificadas

- **Estructura legible por fase del incidente** (01-ticket → 04-evidencias). Se recorre de arriba hacia abajo sin instrucciones adicionales.
- **Hipótesis separadas de hechos.** `hipotesis.md` lista cuatro causas posibles sin afirmar ninguna; las dos descartadas incluyen la razón.
- **Discrepancia DB5 vs DV5 resuelta con evidencia.** La guía dice DB5, el servidor Proxmox del laboratorio tiene DV5 y la USB se grabó con DV5. Ambas capturas (Proxmox + WinSCP) están en el .docx.
- **Reglas de seguridad respetadas.** No hay credenciales de WinSCP, usuarios ni contraseñas publicadas en los .md o .docx. En las capturas de WinSCP y Proxmox se ve el host y el usuario (`root@192.168.50.175`, `root@pam`) pero no la contraseña.
- **Pruebas sin acciones destructivas.** No se formateó ni se sobrescribió el disco original. El cambio de disco preservó la unidad WD Blue como se encontró.

## 3. Oportunidades de mejora

### Críticos
Ninguno. No hay afirmaciones sin respaldo que puedan inducir a una intervención incorrecta, ni credenciales expuestas, ni recomendaciones de acciones destructivas.

### Importantes
- **I1 — Falta la secuencia exacta entre P1 (síntoma visto) y P4 (cambio de disco).** La foto del BIOS muestra el disco Crucial, por lo que el bucle de "Preparando dispositivos" pudo ocurrir ya con ese disco. El relevo necesita saber con qué disco se vio cada síntoma.
  - *Mitigado en este commit:* se añade en `03-pruebas/pruebas-realizadas.md` una nota con la lectura más coherente a partir de las fotos (el BIOS Information muestra el Crucial, no el WD Blue), declarando explícitamente que no está confirmada por una nota tomada en el momento. No se inventa cronología que no conste.
- **I2 — El `SrtTrail.txt` todavía no se ha leído.** Es el log que Windows deja cuando la Reparación automática no puede reparar y suele indicar el componente que falla. Es el siguiente paso natural.
  - *Fuera de alcance de esta sesión:* requiere estar frente al equipo. Está anotado como siguiente paso 1 en `conclusiones.md`.

### Recomendables
- **R1 — Referencia explícita a la guía del docente.** El repo no la cita por nombre.
  - *Resuelto en este commit:* se añade en el README de raíz una línea con el ID y versión de la guía (INC-01 v1.0, Ing. Diego Cárdenas Sejas).
- **R2 — Diferenciar en `04-evidencias/` qué foto respalda qué prueba.** El .docx está organizado por secciones, pero las pruebas no las referencian imagen por imagen.
  - *Resuelto en este commit:* cada prueba de `pruebas-realizadas.md` ya referencia a `04-evidencias/Evidencias-laptop.docx` o `Proceso-instalacion-ISO.docx`. Se refina para nombrar la sección exacta.

## 4. Preguntas espejo (con respuesta)

- **¿Qué evidencia demuestra que el problema existía?** → Texto literal del ticket (`01-ticket/ticket-INC-01.md`) + foto de la pantalla "Preparando dispositivos (70 %)" en el .docx.
- **¿La causa identificada explica los síntomas?** → No hay causa confirmada. Están en hipótesis, lo cual es coherente con el principio de la guía ("diagnosticar antes de intervenir").
- **¿Otro técnico puede repetir el procedimiento sin preguntarnos?** → Sí para P2 (revisar BIOS), P3 (abrir equipo), P5 (preparar USB con Rufus). Para P4 también: el procedimiento es "cambiar disco por el de prueba y arrancar". Para P1 es trivial (encender).
- **¿Qué afirmaciones del README no están respaldadas?** → Ninguna. "En trabajo" refleja el estado real.
- **¿Qué información necesita el siguiente equipo para continuar?** → Está en `conclusiones.md`: 5 pasos concretos, en orden, con rutas y nombres de archivo.
- **¿Qué pasa si el servicio falla nuevamente?** → El equipo todavía no da servicio (sigue sin arrancar Windows). Esta pregunta aplicará después de la recuperación; se verá en ese momento.

## 5. Tres acciones prioritarias

Todas aplicadas en el mismo commit que publica este documento.

| # | Qué cambia | Por qué | Dónde | Cómo verificar |
|---|---|---|---|---|
| 1 | Nota de cronología P1–P4 añadida (lectura de las fotos, no afirmación cerrada) | El relevo necesita entender qué se puede concluir desde las fotos y qué no | `03-pruebas/pruebas-realizadas.md` (nota debajo de P4) | Leer la nota: describe lo que las fotos permiten inferir sin inventar |
| 2 | Referencia a la guía del docente en el README | Trazabilidad del procedimiento oficial seguido | `README.md` (raíz) | Buscar "guía del docente" o "INC-01 v1.0" en el README |
| 3 | Cada prueba referencia su evidencia por nombre de .docx | Correspondencia pruebas ↔ fotos | `03-pruebas/pruebas-realizadas.md` | Cada bloque P1–P5 cita el archivo exacto |

## 6. Siguiente paso

El siguiente trabajo frente al equipo es el paso 1 de `conclusiones.md`: entrar a **Opciones avanzadas** desde la pantalla de Reparación automática, abrir Símbolo del sistema y leer `SrtTrail.txt`. Es la pieza que probablemente destraba o acota el diagnóstico; después de leerlo, se decide entre continuar con las opciones de recuperación o arrancar desde la USB ya preparada.

---

## Historial de decisiones tomadas con apoyo de la IA

Durante el armado del repositorio, estas fueron las sugerencias relevantes de la IA y qué hicimos con cada una.

### S1 — Estructura de carpetas
**Sugerencia:** 8 carpetas numeradas con subcarpetas por tipo dentro de evidencias.
**Decisión:** **adaptada.** Se usó una versión más simple: 4 carpetas por fase + archivos sueltos en raíz.
**Justificación:** suficiente para un incidente de este tamaño.

### S2 — Subcarpetas por tipo dentro de evidencias
**Sugerencia:** separar capturas / fotos / comandos / cambios.
**Decisión:** **descartada.** Todo junto en `04-evidencias/`.
**Justificación:** una sola carpeta mantiene todo visible.

### S3 — Descripción breve bajo cada foto en el Word
**Sugerencia:** una sola línea por imagen diciendo qué se ve.
**Decisión:** **aceptada.**
**Justificación:** se lee rápido, evita párrafos innecesarios.

### S4 — No confirmar causa sin evidencia (mezcla Legacy/UEFI)
**Sugerencia:** anotar la configuración mixta como dato a revisar, no como causa.
**Decisión:** **aceptada.**
**Justificación:** coincide con la guía ("diagnosticar antes de intervenir"). Está como H3 en `hipotesis.md`.

### S5 — Incluir UUID del equipo
**Sugerencia:** registrar el UUID completo junto al SN y MTM.
**Decisión:** **aceptada.**
**Justificación:** no es credencial y la guía pide identificación del equipo.
