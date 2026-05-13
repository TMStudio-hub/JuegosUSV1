# Manual de Usuario

## Propósito

Este juego sirve para capacitar a equipos de Amazon Fresh en seguridad y operaciones básicas de almacén. Los participantes responden preguntas sobre acciones operativas, y el árbitro controla la sesión.

## 1. Abrir el juego

1. Localiza `Juego Dia del trabajador.html`.
2. Abre el archivo con un navegador moderno: Chrome, Edge o Firefox.

## 2. Configuración inicial (Administrador)

1. Haz clic en el botón `⚙️` en la parte superior derecha.
2. En la pestaña `🎭 Acciones`, agrega preguntas nuevas:
   - `Nombre`: la respuesta correcta.
   - `Pregunta`: lo que verán los jugadores.
   - `Opciones incorrectas`: separadas por comas.
   - Selecciona la animación que acompañará la acción.
3. En la pestaña `⚙️ Config`, crea las salas que usarán los jugadores.
4. Ajusta la configuración del juego:
   - Número de preguntas por partida.
   - Tiempo por pregunta.
   - Máximo recomendado: hasta 15 jugadores por sala.
5. Si deseas, cambia el PIN de administrador para proteger el marcador.

## 3. Uso del modo árbitro

1. En el panel de administración, selecciona la pestaña `🏁 Árbitro`.
2. Presiona `Iniciar ronda` para cargar las preguntas.
3. Usa `Siguiente pregunta` para avanzar en la sesión.
4. Usa `Mostrar respuesta` para revelar la respuesta correcta cuando quieras.
5. El árbitro puede usar esta pantalla como guía durante la actividad.

## 4. Cómo juegan los participantes

1. Cada participante ingresa su nombre.
2. Introduce el código de sala proporcionado por el administrador.
3. Da clic en `¡Jugar! 🎮`.
4. Responde las preguntas dentro del tiempo asignado.
5. El juego muestra el puntaje final y la posición en la sala.

## 5. Resultados y clasificaciones

- La pestaña `🏆 Resultados` del administrador muestra el ranking por sala.
- El sistema guarda los marcadores de cada sala en Firebase Realtime Database cuando está disponible.
- El marcador retiene las mejores 15 puntuaciones por sala.

## 6. Consejos para sesiones grupales

- Si hay más de una sala, crea códigos diferentes como `TURNO-A`, `TURNO-B`, etc.
- El administrador puede generar un código de sala automático en la pestaña de `⚙️ Config`.
- Al compartir el enlace o QR, los jugadores abrirán el juego con ese código ya completo.
- Para una mejor experiencia, muestra el modo árbitro en una pantalla compartida.
- Antes de iniciar el juego, verifica que las preguntas sean claras y adecuadas.
- Usa el botón de edición para corregir preguntas sin tener que eliminarlas y recrearlas.

## 7. Limitaciones

- El juego funciona sin backend, por lo que los datos se almacenan localmente en el navegador.
- Para compartir el juego en varios dispositivos, abre el mismo archivo en cada uno.
- El marcador por sala se guarda solo en el navegador donde se juegue.

## 8. Sugerencia de uso

- Ideal para actividades de capacitación tipo Kahoot pero con un enfoque personalizado.
- Funciona bien en talleres de seguridad y dinámicas de repaso.
- Permite a tu esposa preparar una actividad de Amazon Fresh para hasta 15 personas con control del árbitro.

## 9. Publicación en GitHub / Firebase

- Usa `index.html` como archivo principal para hosting.
- El directorio incluye `firebase.json` y `.firebaserc` para Firebase Hosting.
- Si quieres desplegar automáticamente desde GitHub, puedes usar el flujo en `.github/workflows/firebase-hosting.yml`.
- Necesitarás agregar el secreto `FIREBASE_SERVICE_ACCOUNT` en tu repositorio de GitHub.
