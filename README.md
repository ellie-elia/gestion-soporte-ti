# gestion-soporte-ti

Registro técnico de incidentes, pruebas, evidencias y continuidad del soporte de TI.

Trabajo grupal — **Simulación profesional de soporte técnico de TI** (Hito 4).
Universidad Privada Franz Tamayo (UNIFRANZ) — Ingeniería de Sistemas.

---

## Integrantes y responsabilidades

| # | Rol | Integrante |
|---|-----|------------|
| 1 | Coordinador del incidente | Lucas David Loayza |
| 2 | Operador técnico | Fabrizio Magne Luizaga |
| 3 | Analista e investigador | Nathan Ezequías Torrico Torrez |
| 4 | Responsable de evidencias y documentación | Elia Solis Escobar |
| 5 | Responsable de continuidad y relevo | Juan Manuel Chacón Villarroel |

---

## Estado del incidente

**Ticket INC-01** — Falla de inicio de equipo portátil. Lenovo IdeaPad 320-14ISK.

| Campo | Detalle |
|---|---|
| Estado | En trabajo (abierto) |
| Última actualización | [18/10/2026] |
| Síntoma confirmado | Bucle: carga → "Preparando reparación automática" → reinicia |
| Pruebas realizadas | Acceso a BIOS (F2): detecta todo con nromalidad. 
| Medio de instalación | USB de 8 GB creado con Rufus 4.15 (ISO `CCSA_X64FRE_ES-ES_DV5.iso`, GPT/UEFI, FAT32). Estado: se esataba descargando del servior proxmox y se quemo en USB para isntalar |
| Cambios hechos en el equipo | se ha cambiado el disco duro |
| Respaldo de datos del usuario | se instalo el disco duro de respaldo  |
| Hipótesis activas | Arranque dañado (en buclle) (BCD/EFI); archivos del sistema; disco; hardware |
| Hipótesis descartadas | no era problema de RAM  |
| Responsable del siguiente paso | Fabrizio (ejecuta), Lucas (autoriza) |
| Riesgos | No usar "Restablecer este equipo" ni "System Recovery" (borran datos) |
| Ultima actualizacion | no completo el quemado de la imagen en el USB |
---

## Estructura del repositorio

| Carpeta / archivo | Contenido |
|---|---|
| `01-ticket/` | Ticket recibido y descripción del incidente |
| `02-investigacion/` | Estado inicial, síntomas, hipótesis y posibles causas |
| `03-pruebas/` | Comandos, procedimientos y resultados |
| `04-evidencias/` | Capturas, fotografías y archivos que demuestran lo realizado |
| `bitacora.md` | Registro cronológico de actividades, dificultades y pendientes |
| `prompt-espejo.md` | Sugerencias de la IA aceptadas, adaptadas o descartadas (con justificación) |
| `activitywatch.md` | Reporte de ActivityWatch, periodo registrado y limitaciones |
| `transferencia.md` | Correo de transferencia para el relevo |
| `conclusiones.md` | Solución comprobada, estado final y siguientes pasos |
