# Real Ones — Guía paso a paso: instalar el frontend y jugar una partida real

Esta guía asume que ya hiciste la guía anterior (el backend instalado en
`real-ones-backend`, corriendo con `npm start`) y que funcionó la
simulación. Ahora vamos a construir las pantallas y jugar de verdad, con
varios dispositivos o pestañas.

---

## Paso 1 — Crear el proyecto del frontend

Abrí una terminal en el lugar donde guardás tus proyectos (al lado de la
carpeta `real-ones-backend`, no adentro) y ejecutá:

```
npm create vite@latest real-ones-frontend -- --template react
```

Te va a preguntar un par de cosas de confirmación — aceptá las opciones
por defecto. Al terminar, vas a tener una carpeta nueva `real-ones-frontend`.

Entrá a esa carpeta:

```
cd real-ones-frontend
```

---

## Paso 2 — Reemplazar los archivos generados por los nuestros

Adentro de `real-ones-frontend`, hay una carpeta `src`. Ahí Vite generó un
`App.jsx` y un `App.css` de ejemplo — **reemplazalos** por los que te
pasé (mismo nombre, así que es sobreescribir el archivo, no renombrar
nada).

También borrá estos dos archivos que Vite generó y que no usamos:
- `src/App.css` → ya lo reemplazaste, ignorá este punto
- `src/assets/react.svg` (si existe, no es necesario, podés dejarlo o
  borrarlo, no rompe nada)

Copiá también el `real-ones-frontend-package.json` que te pasé, y
**reemplazá** el `package.json` que ya existe en la raíz de
`real-ones-frontend` (no el de `src`, el de la raíz de la carpeta).

---

## Paso 3 — Instalar las dependencias

Con la terminal parada en `real-ones-frontend`:

```
npm install
```

---

## Paso 4 — MUY IMPORTANTE: apuntar el juego a tu servidor local

El código que te pasé tiene esta línea al principio de `App.jsx`,
pensada para cuando el backend ya esté desplegado en Render:

```js
const socket = io('https://real-ones-backend.onrender.com');
```

Como todavía **no desplegamos nada** (eso es la Fase 4, más adelante),
esa dirección no existe todavía. Para probarlo ahora, tenés que cambiar
esa línea **temporalmente** a:

```js
const socket = io('http://localhost:3002');
```

Abrí `src/App.jsx` con cualquier editor de texto, buscá esa línea cerca
del principio del archivo, y cambiala. **Guardá el archivo.**

(Vamos a tener que acordarnos de revertir este cambio antes de subirlo a
producción — te lo voy a recordar cuando lleguemos a la Fase 4.)

---

## Paso 5 — Levantar el backend (si no lo tenés corriendo ya)

Abrí una terminal en la carpeta `real-ones-backend` (la del Paso 1 de la
guía anterior) y ejecutá:

```
npm start
```

Confirmá que veas `Servidor de Real Ones activo en puerto 3002`. Dejala
abierta.

---

## Paso 6 — Levantar el frontend

En otra terminal, parada en `real-ones-frontend`, ejecutá:

```
npm run dev
```

Te va a mostrar algo como:

```
Local:   http://localhost:5173/
```

Abrí esa dirección en tu navegador. Deberías ver el título **"REAL ONES"**
en grande, con la pantalla para elegir signo y nombre.

---

## Paso 7 — Jugar una partida real con varias pestañas

Ya que todavía no tenés esto desplegado en internet, la forma más simple
de probarlo con "varios jugadores" es abrir la misma dirección
(`http://localhost:5173`) en **3 o más pestañas distintas** del navegador
(o ventanas — cada una simula un jugador distinto).

En cada pestaña:
1. Elegí un signo y un nombre distinto.
2. En la primera pestaña, tocá **CREAR SALA** — anotá el código que te
   muestra.
3. En las demás pestañas, pegá ese código y tocá **UNIRSE**.
4. Desde la primera pestaña (el anfitrión), elegí la composición del
   grupo y tocá **EMPEZAR**, después **EMPEZAR A JUGAR**.
5. Jugá la partida completa, votando distinto en cada pestaña para poder
   ver variedad en los resultados.

Si tenés el celular en la misma red WiFi que la computadora, también
podés probarlo ahí: fijate qué dirección IP te muestra la terminal al
lado de "Network" (en vez de "Local") cuando corriste `npm run dev`, y
abrí esa dirección desde el navegador del celular.

---

## Paso 8 — Qué mirar y qué contarme

Andá jugando la partida completa (las 12 rondas) y fijate especialmente:

1. **¿Cada pantalla se ve como corresponde?** (elegir signo, lobby con
   los jugadores, las 3 mecánicas de ronda, el resultado de cada ronda,
   la tarjeta final)
2. **¿El Ranking se siente cómodo de tocar?** Es la pantalla más nueva y
   la que más dudas me genera en cuanto a la interacción táctil — avisame
   si se siente incómoda o confusa.
3. **¿La tarjeta final muestra bien tu rol, tu signo, y el ranking
   general?**
4. Si algo se rompe, **abrí la consola del navegador** (F12, pestaña
   "Console") y copiame cualquier error en rojo que aparezca, además de
   contarme en qué pantalla y qué estabas haciendo cuando pasó.

No hace falta que sea una partida "linda" — con que llegue de punta a
punta sin romperse ya es un montón de información. El diseño visual
final (colores, animaciones, la estética de marca) lo dejamos para
después, como ya habíamos hablado.
