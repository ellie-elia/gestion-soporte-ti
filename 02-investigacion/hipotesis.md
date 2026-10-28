# Hipótesis

Posibles causas del bucle de arranque. Ninguna está confirmada todavía.

## H1 — Perfil de usuario o actualización fallida de Windows

El síntoma (quedarse en "Preparando dispositivos" y reiniciar) suele asociarse a una actualización, driver o perfil que no termina de aplicarse. Se descarta sólo si una recuperación limpia no resuelve.

## H2 — Corrupción de archivos del sistema o del arranque

Compatible con el BSOD previo que reportó el usuario. La pantalla "Reparación automática no pudo reparar tu PC" (ver evidencia posterior al cambio de disco) apunta en esta dirección: Windows intentó repararse y no pudo.

## H3 — Configuración de arranque mixta Legacy / UEFI

El BIOS está en Boot Mode = Legacy Support pero con Boot Priority = UEFI First, y aparecen entradas duplicadas (Windows Boot Manager en EFI y SATA HDD en Legacy). Si el gestor de arranque está instalado en un modo y el firmware intenta por el otro, Windows puede entrar en bucle.

## H4 — Falla lógica del disco

El BIOS detecta el disco, pero eso no asegura que el área del sistema esté íntegra. Pendiente: ejecutar diagnóstico de superficie / SMART cuando se tenga acceso.

## Descartadas por ahora

- **Falla total del disco:** el BIOS detecta el SSD (CT240BX500SSD1) y aparece "Windows Boot Manager" en EFI, por lo que el disco responde.
- **Falla de RAM:** el POST se completa, el BIOS reporta 8 192 MB y el equipo llega al logo de Windows. Pendiente de confirmar con un test de memoria si otras hipótesis se descartan.
