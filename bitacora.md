# Bitácora de trabajo

Registro cronológico de lo que la cuadrilla ha hecho.

## 2026-10-28

- Recepción del ticket **INC-01 — Falla de inicio de equipo portátil** por correo del docente. Guardado en `01-ticket/`.
- Lectura de la guía rápida de atención del docente (INC-01 v1.0).
- Encendido del equipo y confirmación del síntoma: bucle en "Preparando dispositivos (70 %)".
- Entrada al BIOS. Verificación de que CPU, RAM y disco se detectan. Fotografía de las pestañas Information y Boot.
- Identificación del equipo: Lenovo IdeaPad 320-14ISK, SN PF129XH1, MTM 80XG008ALM.
- Apertura del equipo (desarmado de la tapa posterior) para inspección física interna. Sin daños visibles.
- Prueba con otro disco (Crucial BX500 240 GB en lugar del WD Blue 1 TB original). El equipo arranca y entra en Reparación automática, con mensaje **"no pudo reparar tu PC"** y log en `SrtTrail.txt`.
- Documentación en `04-evidencias/Evidencias-laptop.docx`.
- Primera subida al repositorio: estructura inicial, ticket, evidencias y estado del incidente.
- Preparación del medio USB con la ISO: ISO descargada desde el servidor Proxmox vía WinSCP y grabada con Rufus en modo GPT / UEFI (no CSM). Evidencias en `04-evidencias/Proceso-instalacion-ISO.docx`.

## Dificultades

- La cronología exacta entre ver el bucle de arranque y hacer el cambio de disco no quedó registrada en el momento. Hay que precisarla con el equipo.
- El código del BSOD inicial que vio el usuario no se pudo identificar (ya no reaparece).

## Tareas pendientes

- [ ] Revisar `SrtTrail.txt` desde Opciones avanzadas → Símbolo del sistema.
- [ ] Probar Reparación de inicio, Restaurar sistema, Desinstalar actualizaciones recientes.
- [x] Preparar medio USB con la ISO (ver guía del docente, paso 4).
- [ ] Cambiar BIOS a UEFI y arrancar desde la USB preparada.
- [ ] Si procede, reinstalar Windows; respaldar datos accesibles del disco original antes.
- [ ] Test SMART del disco.
- [ ] Confirmar con el equipo la secuencia real entre P1 y P4.
- [ ] Reporte de ActivityWatch cuando esté disponible.
