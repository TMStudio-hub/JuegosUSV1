# Juego Amazon Fresh - Día del Trabajador

Juego de preguntas personalizable para capacitaciones rápidas sobre seguridad y operaciones de almacén. Está diseñado para que un administrador/arbitro prepare las preguntas y equipos entren con un código de sala.

## Qué incluye

- Archivo principal: `Juego Dia del trabajador.html`
- Configuración de salas y PIN de administrador
- Panel de administración para crear, editar y eliminar preguntas
- Modo árbitro para controlar la sesión en vivo
- Marcador por sala y resultados ordenados
- Configuración de duración de la ronda y tiempo por pregunta
- Persistencia local en el navegador usando `localStorage`

## Cómo usar

1. Abre `Juego Dia del trabajador.html` en un navegador moderno.
2. Presiona el botón ⚙️ para abrir el panel de administración.
3. Crea las salas (códigos) que usarán los equipos.
4. Agrega, edita o elimina las preguntas de entrenamiento.
5. Ajusta el número de preguntas por partida y el tiempo por pregunta.
6. Comparte el código de sala con los participantes.
7. Los jugadores ingresan su nombre y la sala para comenzar.
8. El árbitro puede usar la pestaña `🏁 Árbitro` para presentar preguntas y mostrar respuestas.

## Recomendaciones

- El juego soporta hasta 15 jugadores por sala.
- Para una actividad colectiva, usa un proyector o pantalla compartida con el modo árbitro.
- El puntaje se guarda localmente en el navegador, así que cada computador conserva su historial.

## Notas técnicas

- El juego es estático y funciona sin servidor.
- Si necesitas que varios dispositivos compartan una misma sala en tiempo real, recomienda alojar el archivo en un servidor interno y usar el mismo archivo en cada navegador.

## Despliegue con GitHub y Firebase

- El proyecto ya está preparado para Firebase Hosting con `firebase.json` y `.firebaserc`.
- También incluye una plantilla de GitHub Actions en `.github/workflows/firebase-hosting.yml`.
- Para habilitar el despliegue automático, agrega el secreto `FIREBASE_SERVICE_ACCOUNT` en tu repositorio de GitHub.
- Usa `index.html` como entrada principal para el hosting.
