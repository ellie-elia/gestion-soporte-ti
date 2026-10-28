# Prompt espejo

Registro del uso de la conversación de IA de la cuadrilla y qué se hizo con sus sugerencias.

Herramienta usada: Claude (una sola conversación compartida, iniciada el 2026-10-28).

## Sugerencias registradas

### S1 — Estructura de carpetas del repositorio
**Qué sugirió la IA:** 8 carpetas numeradas (01-equipo, 02-ticket, 03-analisis, 04-evidencias, 05-bitacora, 06-prompt-espejo, 07-activitywatch, 08-cierre) con subcarpetas por tipo dentro de evidencias.
**Qué hicimos:** **Adaptada.** Se usó una estructura más simple: 4 carpetas numeradas por fase del incidente (01-ticket, 02-investigacion, 03-pruebas, 04-evidencias) + archivos sueltos en la raíz (bitacora.md, prompt-espejo.md, activitywatch.md, conclusiones.md).
**Justificación:** la propuesta era redundante para un incidente de este tamaño; la versión simple sigue cubriendo todos los puntos exigidos por el docente y se lee de arriba hacia abajo en GitHub sin perderse.

### S2 — Subdividir evidencias por tipo (capturas / fotos / comandos / cambios)
**Qué sugirió la IA:** subcarpetas dentro de `04-evidencias/` separando capturas, fotografías, comandos y cambios.
**Qué hicimos:** **Descartada.** Las evidencias van juntas en una sola carpeta.
**Justificación:** para este incidente, una sola carpeta mantiene todo visible sin tener que entrar a varias subcarpetas.

### S3 — Línea de descripción breve bajo cada foto en el Word de evidencias
**Qué sugirió la IA:** acompañar cada imagen con una sola línea diciendo qué se ve (datos clave del BIOS, modelo del disco, etc.).
**Qué hicimos:** **Aceptada.**
**Justificación:** se lee rápido y evita párrafos innecesarios.

### S4 — No confirmar causa sin evidencia (sobre la mezcla Legacy / UEFI)
**Qué sugirió la IA:** anotar la configuración mixta Legacy + UEFI como un dato a revisar, no como la causa del problema.
**Qué hicimos:** **Aceptada.**
**Justificación:** coincide con el principio rector de la guía del docente ("diagnosticar antes de intervenir"). Queda listada como hipótesis en `02-investigacion/hipotesis.md` (H3), sin confirmar.

### S5 — Incluir UUID del equipo en el estado inicial
**Qué sugirió la IA:** registrar el UUID completo del equipo junto al SN y MTM.
**Qué hicimos:** **Aceptada.** Se dejó en `02-investigacion/estado-inicial.md`.
**Justificación:** el UUID no es credencial y la guía pide identificación del equipo.
