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

## Día 4 — Voz local (Whisper + Piper)
- Whisper (faster-whisper, modelo tiny-int8) y Piper añadidos como servicios 
  Docker junto a Home Assistant, conectados vía integración Wyoming Protocol
- Asistente de voz local ("Assist") creado en español, con Whisper como 
  voz-a-texto y Piper (voz carlfm x_low) como texto-a-voz
- Probado por texto: comandos directos funcionan correctamente 
  (ej. "enciende/apaga el aire acondicionado" → ejecuta la acción real)
- Limitación detectada: comandos complejos o ambiguos ("ponlo en modo eco") 
  no se interpretan bien sin frases personalizadas — pendiente de explorar 
  "Sentences" personalizadas más adelante
- Pendiente: prueba con micrófono/altavoz real (hoy solo por texto)
