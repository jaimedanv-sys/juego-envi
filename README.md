# Guardianes ENVI · Inspección PROFEPA – Almacén de residuos

Juego web de capacitación ambiental (EHS). Recorres un almacén temporal de residuos peligrosos,
encuentras 5 hallazgos y respondes las preguntas del inspector antes de que la multa te lleve a la clausura.

**Jugar:** https://jaimedanv-sys.github.io/juego-envi/

> Simulación educativa. No es material oficial de PROFEPA y los montos de multa son ilustrativos.

## Cómo se juega

- **PC:** muévete con **WASD** o las **flechas**. En la tarjeta del inspector puedes responder con **1 / 2 / 3** (o A / B / C).
- **Celular:** usa el **joystick** amarillo de abajo a la izquierda y toca la respuesta.
- Busca los signos **!** amarillos (la flecha en el piso apunta al hallazgo pendiente más cercano). Al acercarte se abre la tarjeta.
- Cada respuesta incorrecta suma su multa al contador **Multa estimada**. Con **3 errores** aparece **CLAUSURA**.
- Al revisar los 5 hallazgos aparece **¡Inspección aprobada!** con aciertos, multa evitada y multa recibida.

## Los 5 hallazgos

| # | Hallazgo | Multa si fallas | Fundamento citado |
|---|---|---|---|
| 1 | Tambo sin etiqueta de residuo peligroso | $180,000 | Reglamento LGPGIR art. 46 · NOM-052-SEMARNAT-2005 |
| 2 | Falta charola antiderrames bajo tambos de aceite usado | $250,000 | Reglamento LGPGIR art. 82 |
| 3 | Bitácora de generación incompleta | $120,000 | Reglamento LGPGIR art. 71 |
| 4 | Extintor obstruido por cajas | $90,000 | NOM-002-STPS-2010 |
| 5 | Falta letrero "Almacén de residuos peligrosos" | $60,000 | Reglamento LGPGIR art. 82 · NOM-026-STPS-2008 |

Las preguntas, opciones, explicaciones y montos están en el arreglo `HALLAZGOS` al inicio del `<script type="module">` de `index.html`;
se pueden editar ahí sin tocar el resto del código.

## Decisiones que tomé (sin poder preguntarte)

- **Un solo archivo `index.html`**, sin imágenes ni modelos: todo son cajas, cilindros y conos con colores planos.
  Los textos de letreros y etiquetas (SALIDA, EXTINTOR, RESIDUO PELIGROSO, etc.) se dibujan con `<canvas>` dentro del mismo archivo.
- **Three.js r160 (0.160.0)** desde jsDelivr como módulo ES (`three.module.min.js`), versión fija. Si el CDN no carga en 12 s
  se muestra un aviso con botón "Recargar" en vez de una pantalla negra.
- **Cámara ortográfica isométrica** que sigue al jugador. En celular vertical se acerca más para que todo se vea grande.
  "Arriba" en el teclado/joystick es "arriba en la pantalla" (no el eje del mundo), que es lo más intuitivo en isométrico.
- **La tarjeta se abre sola** al acercarte (no hace falta botón de "interactuar"), para que sea fácil en celular.
- **Cada hallazgo se responde una sola vez.** Aunque falles, se muestra la explicación correcta, el hallazgo cuenta como revisado
  y el escenario se corrige (aparece la etiqueta, la charola, la bitácora llena, se quitan las cajas y aparece el letrero).
  Encima queda una ✓ verde o una ✗ roja.
- **"Inspección aprobada"** se muestra al revisar los 5 hallazgos con menos de 3 errores (puedes aprobar con 1 o 2 errores;
  el resumen lo indica). **Multa evitada** = suma de las multas de los hallazgos que respondiste bien.
- **Montos de multa ilustrativos** (entre $60,000 y $250,000 MXN), más altos para lo que implica riesgo de contaminación.
  No son cálculos legales; las multas reales se fijan en UMA según la gravedad y la circunstancia.
- **Opciones barajadas** en cada partida, para que no se memorice "siempre es la A".
- **Extras pequeños:** flecha guía en el piso, sonidos cortos generados con Web Audio (sin archivos), animación de caminar,
  pista que se desvanece en celular para no tapar el escenario.
- `window.__envi` expone el estado y una función para teletransportar al jugador; la usé para la prueba automática
  y no afecta el juego.

## Verificación hecha

Probé el juego con Chromium (Playwright) en tamaño PC (1280×800) y celular (390×844, táctil), sin errores de JavaScript:
pantalla de inicio, movimiento con teclado y con el joystick, apertura de las 5 tarjetas, respuesta correcta e incorrecta,
pantalla de aprobado, pantalla de clausura y botón de reintentar.

## Publicar en GitHub Pages (una sola vez)

1. En GitHub abre el repositorio → **Settings** → **Pages**.
2. En **Build and deployment → Source** elige **Deploy from a branch**.
3. En **Branch** elige **main** y la carpeta **/ (root)** → **Save**.
4. En 1–2 minutos queda en https://jaimedanv-sys.github.io/juego-envi/

## Ideas para después

- Más niveles: área de RME, patio de chatarra, planta de tratamiento de agua, emisiones.
- Modo "inspector": el jugador también debe tomar foto/evidencia de cada hallazgo.
- Banco de preguntas más grande con preguntas aleatorias por partida, y tabla de puntajes.
- Botón para silenciar sonido y opción de alto contraste.
- Tarjetas con un mini‑esquema de cómo se ve "lo correcto" (etiqueta modelo, bitácora modelo).
- Confirmar fundamentos y montos con el área legal antes de usarlo en capacitaciones formales.
