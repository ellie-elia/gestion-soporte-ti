# Pruebas realizadas

Secuencia de pruebas que se han hecho hasta ahora. Cada una con objetivo, qué se hizo, resultado y qué queda.

## P1 — Reproducir el síntoma al encender el equipo

**Objetivo:** confirmar que el síntoma coincide con lo descrito en el ticket.
**Procedimiento:** encender el equipo y observar el arranque.
**Resultado:** el equipo arranca, muestra el logo de Lenovo, llega a Windows con "Preparando dispositivos (70 %)", se apaga y vuelve a reiniciar.
**Conclusión:** síntoma reproducido. Coincide con el ticket.
**Evidencia:** foto de la pantalla en `04-evidencias/Evidencias-laptop.docx`.

## P2 — Revisar información de hardware en el BIOS

**Objetivo:** verificar qué detecta el firmware y descartar fallas evidentes de hardware.
**Procedimiento:** entrar al BIOS (InsydeH20 Setup Utility Rev. 5.0) y revisar las pestañas Information y Boot.
**Resultado:**
- CPU, RAM y disco se detectan correctamente.
- Disco: Crucial BX500 240 GB (CT240BX500SSD1).
- Boot Mode: Legacy Support. Boot Priority: UEFI First.
- Entradas de arranque: Windows Boot Manager (EFI) + SATA HDD (Legacy), ambas sobre el mismo disco.

**Conclusión:** el disco responde al firmware. La configuración de arranque mezcla Legacy y UEFI, lo que queda como punto a revisar.
**Evidencia:** fotos del BIOS Information y BIOS Boot.

## P3 — Inspección física interna

**Objetivo:** verificar el estado físico de los componentes.
**Procedimiento:** apagar y desconectar el equipo, retirar los tornillos de la tapa posterior con destornillador estrella, abrir y observar.
**Resultado:** placa base, ventilador, disipador, batería CMOS, altavoces, módulo de RAM y ranura M.2 WiFi sin daño visible. Zócalo del disco accesible.
**Conclusión:** no se observan daños visibles ni componentes sueltos.
**Evidencia:** fotos del interior.

## P4 — Cambio de disco (WD Blue 1 TB → Crucial BX500 240 GB)

**Objetivo:** probar el arranque con otra unidad de almacenamiento.
**Procedimiento:** retirar el disco original y colocar el disco de prueba.
**Resultado:** el equipo arranca, intenta cargar Windows y entra en "Reparación automática". El sistema muestra el mensaje **"Reparación automática no pudo reparar tu PC"**, con registro en `E:\Recovery\WindowsRE\Winre.wim\System32\Logfiles\Srt\SrtTrail.txt`.
**Conclusión:** el equipo sí arranca y accede a la partición de recuperación, pero no puede reparar automáticamente. Falta revisar el log SrtTrail.txt y las Opciones avanzadas.
**Evidencia:** fotos de ambos discos y de la pantalla de Reparación automática.

> **Nota:** la secuencia exacta entre P1 y P4 (qué disco estaba cuando se vio el bucle de "Preparando dispositivos") queda por confirmar con el equipo. En las fotos del BIOS ya aparece el Crucial BX500.

## P5 — Preparación del medio USB con la ISO

**Objetivo:** tener una USB arrancable con la ISO autorizada para intentar la recuperación o reinstalación.
**Procedimiento:**
1. Localizar la ISO en el servidor Proxmox del laboratorio (`https://192.168.50.175:8006` → Storage local → ISO Images).
2. Transferirla al equipo local vía WinSCP (sesión `root@192.168.50.175`, ruta `/var/lib/vz/template/iso/`).
3. Crear la USB arrancable con Rufus 4.15.2396 (esquema GPT, sistema de destino UEFI (no CSM), FAT32).

**Resultado:** USB en estado "PREPARADO" con la ISO `CCSA_X64FRE_ES-ES_DV5.iso` lista para arrancar.
**Conclusión:** medio de instalación listo. Queda arrancar el equipo desde la USB y continuar con la recuperación/instalación.
**Evidencia:** `04-evidencias/Proceso-instalacion-ISO.docx`.

> **Nota sobre el nombre de la ISO:** la guía del docente tiene un typo (dice `CCSA_X64_FRE_ES-ES_DB5.iso`). El nombre correcto es `CCSA_X64FRE_ES-ES_DV5.iso`, que es la ISO disponible en el servidor Proxmox del laboratorio y la que se usó para preparar la USB. Evidencia en `04-evidencias/Proceso-instalacion-ISO.docx` (capturas de Proxmox y WinSCP).
>
> **Nota sobre modo de arranque:** la USB se preparó para UEFI puro (GPT + UEFI no CSM), pero el BIOS del equipo está en Boot Mode = Legacy Support. Habrá que cambiar el BIOS a UEFI para arrancar desde esta USB.

## Pendientes de prueba

- Revisar el contenido de `SrtTrail.txt` desde Opciones avanzadas → Símbolo del sistema.
- Probar las opciones de recuperación: Reparación de inicio, Restaurar sistema, Desinstalar actualizaciones recientes.
- Si no se recupera, preparar medio USB con la ISO autorizada (ver guía del docente, paso 4) para reinstalar Windows.
- Test SMART del disco antes de dar por descartado el almacenamiento.
