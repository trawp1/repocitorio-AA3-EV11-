# AA3 EV11 — Auth genérico con Supabase (HTML / CSS / JS)

Ejemplo de **login, registro y sesión** listo para que los aprendices lo adapten a su propio proyecto.

## Qué incluye

| Archivo | Rol |
|---------|-----|
| `index.html` | Login y registro |
| `dashboard.html` | Inicio del panel (protegido) |
| `perfil.html` | Segunda página del panel (protegido) |
| `js/guard.js` | Verifica sesión en páginas privadas |
| `css/styles.css` | Estilos |
| `js/config.js` | **Aquí pegas URL + anon key** |
| `js/config.example.js` | Plantilla segura para clonar |
| `.env.example` | Documentación de secretos (copiar a `.env`) |
| `js/auth.js` / `js/dashboard.js` | Lógica de autenticación |

## 1. Crear proyecto en Supabase

1. Entra a [https://supabase.com/dashboard](https://supabase.com/dashboard)
2. New project → espera a que esté listo
3. **Authentication → Providers → Email** activado
4. (Opcional) Si quieres login inmediato sin correo:  
   **Authentication → Providers → Email → Confirm email** = OFF (solo para práctica)

## 2. Copiar credenciales

En **Project Settings → API**:

- **Project URL** → `SUPABASE_URL`
- **anon public** → `SUPABASE_ANON_KEY`
- **service_role** → **NO** va en el frontend (solo backends)

### Opción A — Lo que usa esta demo (obligatorio)

Edita `js/config.js`:

```js
window.APP_CONFIG = {
  SUPABASE_URL: "https://xxxx.supabase.co",
  SUPABASE_ANON_KEY: "eyJhbGciOi...",
};
```

### Opción B — Documentar en `.env` (recomendado en clase)

```bash
copy .env.example .env
```

Completa `.env` con los mismos valores.  
En HTML puro el navegador **no lee** `.env`; por eso también se pegan en `js/config.js`.  
Si más adelante usas PHP/Node, sí leerás `.env` en el servidor.

## 3. Correr en XAMPP

1. Carpeta: `C:\xampp\htdocs\AA3_EV11_Auth\`
2. Apache ON
3. Abrir: [http://localhost/AA3_EV11_Auth/](http://localhost/AA3_EV11_Auth/)

## 4. Flujo de prueba

1. Pestaña **Registrarse** → crear cuenta  
2. **Iniciar sesión** → debes llegar a `dashboard.html`  
3. Ver email / user id  
4. **Cerrar sesión** → vuelves al login  
5. Si entras a `dashboard.html` sin sesión → te redirige a `index.html`

## Cómo adaptarlo a tu proyecto

1. Cambia textos, colores y logo  
2. Tras el login, redirige a tu pantalla real (no necesariamente `dashboard.html`)  
3. Crea tus tablas en Supabase y activa **RLS** con `auth.uid()`  
4. Reutiliza `js/supabase-client.js` y el patrón de `requireSession()` de `dashboard.js`

## Seguridad (mensaje clave para aprendices)

| Clave | ¿Va en HTML/JS? |
|-------|------------------|
| `anon` / public | Sí (con RLS bien configurado) |
| `service_role` | **Nunca** |

`js/config.js` y `.env` están en `.gitignore` para no subir secretos.

## Pasarme las claves (instructor / agente)

Cuando tengas el proyecto Supabase, completa:

1. `.env` (desde `.env.example`), **o**
2. `js/config.js`

con `SUPABASE_URL` y `SUPABASE_ANON_KEY`.  
No hace falta (ni conviene) compartir la `service_role` para este ejemplo de login en el navegador.
