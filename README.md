# Raspberry Pi 5 — Domótica, IA y Robótica

Roadmap de 1 año explorando una Raspberry Pi 5 (4GB): domótica con Home Assistant, 
un asistente de voz local con IA, visión por computador y robótica. 
Proyecto personal documentado día a día, con el objetivo de construir un 
portafolio técnico real mientras aprendo.

## Stack actual

- **Raspberry Pi OS Lite (64-bit)** — sistema base, sin escritorio gráfico
- **Docker + Docker Compose** — todos los servicios corren en contenedores aislados
- **Home Assistant** — núcleo de domótica, automatizaciones y dashboard
- **Whisper (faster-whisper)** — reconocimiento de voz local (STT)
- **Piper** — síntesis de voz local (TTS)
- **Emulated Hue** — integración con Amazon Alexa sin coste adicional

## Hardware

- Raspberry Pi 5 (4GB RAM)
- Carcasa con disipador + heatsink de aluminio
- microSD 64GB
- Acceso remoto vía SSH (sin monitor conectado, uso headless)

## Progreso

### Día 1 — Setup inicial
- Raspberry Pi OS Lite (64-bit) instalado con Raspberry Pi Imager
- Configuración SSH headless (sin monitor)
- Sistema actualizado (`apt update && upgrade`)

### Día 2 — Docker
- Docker Engine instalado vía script oficial
- Usuario añadido al grupo `docker` (sin necesidad de sudo)
- Contenedor de prueba `hello-world` ejecutado correctamente

### Día 3 — Home Assistant
- Home Assistant desplegado en Docker (`docker-compose.yml`)
- Ubicación, zona horaria y unidades configuradas
- App móvil (Home Assistant Companion) vinculada, notificaciones push funcionando
- Automatización 1: aviso al inicio de la "hora dorada" (trigger nativo de sol)
- Automatización 2: interruptor de prueba (helper) → notificación de confirmación

### Día 4 — Voz local (Whisper + Piper)
- Whisper y Piper añadidos como servicios Docker, conectados vía integración Wyoming Protocol
- Asistente de voz local ("Assist") en español, funcionando end-to-end por texto
- Comandos directos funcionan correctamente (ej. "enciende/apaga el aire acondicionado")
- Limitación detectada: comandos ambiguos no se interpretan bien sin frases personalizadas

### Día 5 — Cierre y documentación
- Revisión y limpieza de `docker-compose.yml` (comentarios explicativos)
- README completo
- Cierre del sprint inicial de 5 días

## Día 6 — Voz real (pausado)
- Probado el micrófono del móvil vía app Home Assistant Companion: el 
  reconocimiento de voz funciona, pero responde en inglés porque el móvil usa 
  el asistente por defecto de la app, no "Asistente Casa"
- Pendiente: conseguir micrófono USB dedicado para la Pi y fijar "Asistente 
  Casa" como predeterminado

## Día 7 — MQTT (Mosquitto) + LLM local (Ollama)
- Mosquitto (broker MQTT) desplegado en Docker — base para el futuro proyecto 
  del inversor solar
- Integración MQTT nativa conectada en Home Assistant, verificada con mensaje 
  de prueba end-to-end (`mosquitto_pub` → recibido en tiempo real en HA)
- Ollama desplegado en Docker, modelo `qwen2.5:0.5b` descargado y probado por 
  terminal — respuesta rápida y en español, buen resultado para 4GB de RAM

## Extra — Integración con Alexa (Emulated Hue)

Aire acondicionado (Midea) y enchufe inteligente (Tuya) expuestos a Alexa 
mediante `emulated_hue`, sin necesidad de suscripción de pago (Nabu Casa). 
Fue necesario forzar `listen_port: 80` en la configuración, ya que Alexa 
dejó de soportar el descubrimiento en otros puertos en versiones recientes.

Control por voz funcionando desde un dispositivo Echo:
- "Alexa, enciende el aire acondicionado"
- Ajuste de temperatura vía mapeo de porcentaje/brillo (limitación conocida 
  de Emulated Hue con entidades tipo `climate`)

## Pendiente / próximos pasos

- [ ] Probar el asistente de voz local con micrófono y altavoz reales (hoy solo por texto)
- [ ] Frases personalizadas ("Sentences") para comandos más naturales en Assist
- [ ] Integración del inversor solar (MPP Solar VM IV-5600, app WatchPower) — 
      investigación inicial hecha, pendiente de desarrollo (ver notas internas)
- [ ] Trimestre 2: visión por computador (OpenCV + cámara)
- [ ] Trimestre 3: robótica (evasor de obstáculos / seguidor de línea)
- [ ] Trimestre 4: proyecto final integrador (robot + cámara + IA + control remoto)

## Notas técnicas

- Todos los servicios corren con `network_mode: host` para permitir 
  descubrimiento de dispositivos en la red local (mDNS, SSDP)
- La configuración de Home Assistant persiste en `./config`, independiente 
  del ciclo de vida del contenedor
