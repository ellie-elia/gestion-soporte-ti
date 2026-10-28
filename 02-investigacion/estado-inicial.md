# Estado inicial del equipo

Datos tomados del BIOS (InsydeH20 Setup Utility Rev. 5.0) y de la inspección física. Ver fotos en [`../04-evidencias/Evidencias-laptop.docx`](../04-evidencias/Evidencias-laptop.docx).

## Identificación

| Dato | Valor |
|---|---|
| Modelo | Lenovo IdeaPad 320-14ISK |
| MTM | 80XG008ALM |
| Nº de serie (SN) | PF129XH1 |
| UUID | E1F801FB-EC42-11E7-8A95-8C1645065057 |
| BIOS Version | 4WCN37WW |
| EC Version | 4WEC37WW |

## Hardware

| Componente | Valor |
|---|---|
| CPU | Intel Core i3-6006U @ 2.00 GHz |
| RAM | 8 192 MB (BIOS) — módulo visto: Samsung 4 GB DDR4 SODIMM (M471A5244CB0-CWE) |
| Disco (al momento de la inspección) | Crucial BX500 240 GB SSD (CT240BX500SSD1) |
| Disco original observado | Western Digital WD Blue 1 TB (WD10SPZX), 2.5" SATA |

## Configuración de arranque (BIOS → Boot)

- Boot Mode: **Legacy Support**
- Boot Priority: **UEFI First**
- USB Boot: Enabled
- PXE Boot to LAN: Disabled
- EFI: Windows Boot Manager (CT240BX500SSD1)
- Legacy: SATA HDD : CT240BX500SSD1

## Síntoma reportado

Al encender, llega al logo de Windows con el texto **"Preparando dispositivos (70 %)"**, se apaga y vuelve a iniciar. Bucle de reinicio.
