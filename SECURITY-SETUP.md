# Seguridad reutilizable para esta app y otros proyectos

## Lo que ya quedó hecho aquí
- `index.html` ya trae una capa de acceso preparada con Firebase Auth.
- La constante `AUTH_REQUIRED` existe y hoy está en `false` para no romper la app actual.
- Hosting ya envía `X-Robots-Tag: noindex, nofollow`.
- También existe `robots.txt` para desalentar indexación básica.

## Lo que falta para activar protección real
Sin Firebase Auth o App Check, una web estática no puede impedir de verdad que un script externo intente hablar con Firebase.
La protección fuerte para este patrón es:
1. Firebase Auth para exigir inicio de sesión.
2. App Check para frenar clientes automatizados o no legítimos.
3. Reglas de Realtime Database que rechacen tráfico sin autenticación.

## Ruta gratis y básica recomendada
Si quieres que el jugador entre casi sin fricción pero que el panel y los datos sensibles no queden abiertos, el patrón recomendado es:
1. `Anonymous Auth` para jugadores.
2. `Email/Password` solo para admins o líderes.
3. `App Check` para endurecer el acceso desde fuera de la app.

Ventaja:
- El jugador no ve formulario de login.
- Aun así Firebase le asigna un `uid` y puedes escribir reglas más seguras.
- Las pantallas de admin, preguntas y settings pueden quedar solo para cuentas autorizadas.

Límite real:
- Si un jugador puede unirse a la partida, algo de `sessions`, `scores` o `ranking` seguirá siendo accesible para esa experiencia.
- Lo correcto no es esconder todo, sino separar `datos de juego` y `datos de admin`.

## Activación en este proyecto
### 1. Habilitar Firebase Auth
En Firebase Console:
1. Abre `Authentication`.
2. Pulsa `Get started` si aún no está inicializado.
3. Activa un proveedor.

Nota importante de este proyecto:
- Al intentar inicializar Authentication por API respondió `BILLING_NOT_ENABLED`.
- Eso significa que el primer encendido no se pudo automatizar desde CLI.
- Haz el primer `Get started` desde Firebase Console y, si Google lo pide, activa billing antes de volver a cerrar reglas o encender `AUTH_REQUIRED`.

Recomendado para uso interno:
- `Email/Password` si van a manejar una cuenta compartida del equipo.
- `Google` si todos tienen correo corporativo o cuentas controladas.

### 2. Crear los usuarios autorizados
Si usas `Email/Password`:
1. Ve a `Authentication`.
2. Abre `Users`.
3. Crea el usuario o usuarios del equipo.

### 3. Encender el gate en la app
En `index.html` cambia:

```js
const AUTH_REQUIRED = false;
```

a:

```js
const AUTH_REQUIRED = true;
```

Opcional:
- `AUTH_ALLOWED_EMAILS = ['correo1@empresa.com']`
- `AUTH_ALLOWED_DOMAINS = ['empresa.com']`

Si dejas ambas listas vacías, cualquier usuario válido del proveedor activo podrá entrar.

### 4. Cerrar las reglas de la base de datos
Cuando Auth ya funcione, cambia `database.rules.json` a reglas autenticadas.
Patrón base:

```json
{
  "rules": {
    ".read": false,
    ".write": false,
    "rooms": {
      ".read": "auth != null",
      ".write": "auth != null"
    },
    "questions": {
      ".read": "auth != null",
      ".write": "auth != null"
    },
    "settings": {
      ".read": "auth != null",
      ".write": "auth != null"
    },
    "scores": {
      ".read": "auth != null",
      ".write": "auth != null"
    },
    "sessions": {
      ".read": "auth != null",
      ".write": "auth != null"
    },
    "flag_ranking": {
      ".read": "auth != null",
      ".write": "auth != null"
    },
    "ideas_bucket": {
      ".read": "auth != null",
      ".write": "auth != null"
    }
  }
}
```

### 5. Desplegar
```powershell
firebase deploy --only hosting,database --project juegosusv1-947476458528
```

## Recomendación extra: App Check
Si quieres protegerte mejor contra crawlers o scripts que intenten llamar a Firebase directamente:
1. Abre `Build > App Check` en Firebase Console.
2. Registra tu app web.
3. Usa `reCAPTCHA v3` o `reCAPTCHA Enterprise`.
4. Activa enforcement para `Realtime Database`.

Esto es importante porque Auth por sí sola protege el acceso lógico, pero App Check ayuda a bloquear clientes no válidos.

## Cómo repetirlo en otros dos proyectos
1. Copia el bloque de acceso de `index.html`.
2. Ajusta `FIREBASE_CONFIG`.
3. Activa `AUTH_REQUIRED = true` solo después de habilitar Auth.
4. Aplica reglas `auth != null`.
5. Agrega `robots.txt` y cabeceras `noindex`.
6. Si el proyecto es público pero la base no debe serlo, habilita App Check.

## Lo importante
- `robots.txt` y `noindex` no son seguridad real; solo quitan visibilidad.
- La seguridad real en Firebase para este tipo de app es `Auth + App Check + Rules`.
- Si enciendes reglas autenticadas antes de habilitar Auth, la app se quedará sin acceso.
