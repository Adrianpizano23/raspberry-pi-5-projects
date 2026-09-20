# raspberry-pi-5-projects
Roadmap de 1 año: domótica, visión por computador, robótica e IA en una Raspberry Pi 5
## Día 1 — Setup inicial
- Raspberry Pi OS Lite (64-bit) instalado
- Configuración SSH headless (sin monitor)
- Sistema actualizado (`apt update && upgrade`) 

## Día 2 — Docker instalado
- Docker Engine 29.8.1 instalado vía script oficial
- Usuario añadido al grupo `docker` (sin necesidad de sudo)
- Contenedor de prueba `hello-world` ejecutado correctamente

## Día 3 — Home Assistant funcionando
- Home Assistant desplegado en Docker (docker-compose.yml)
- Ubicación, zona horaria y unidades configuradas
- App móvil (Home Assistant Companion) vinculada, notificaciones push funcionando
- Automatización 1: aviso al inicio de la "hora dorada" (trigger nativo de sol)
- Automatización 2: interruptor de prueba (helper) → notificación de confirmación
