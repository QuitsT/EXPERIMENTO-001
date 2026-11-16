# PROMPT DE CONTINUIDAD — EXPERIMENTO 001 (para Antigravity / Claude / Gemini)

Copia y pega este prompt completo en Antigravity, junto con el archivo `experimento_001_tanda14.html` (el código actual del juego). Responde siempre en español.

---

## 1. QUIÉN SOY Y QUÉ ES ESTE JUEGO

Soy Christopher, estudiante de Ingeniería en Ciberseguridad en la UNIPOLI (Durango, México), grupo 1B. Este es mi juego individual para la materia **Fundamentos de Ciberseguridad, del Dr. Raúl Villanueva**. No es un juego para publicar, es un trabajo de clase que yo mismo pruebo en mi celular (Redmi Note 11 Pro 5G) y en PC.

**Experimento 001** es un run-and-gun 2D estilo Metal Slug, en **un solo archivo HTML con Canvas, sin motor externo, sin librerías externas, sin internet**. Universo post-apocalíptico: los protagonistas son experimentos humanos del gobierno que escaparon. **El Capitán** fue el primer experimento, el que más sufrió, y lideró el escape.

Plataforma: PC (incluso máquinas muy modestas, ~2 GB RAM) y táctil en celular. **El cooperativo local para 2 jugadores en una PC es un objetivo de diseño, NO está implementado.** La identidad visual es provisional (los enemigos son rectángulos) y NO se debe rediseñar hasta que yo lo pida; primero jugabilidad, arte después.

## 2. REGLAS DE TRABAJO (OBLIGATORIAS)

- Trabajamos en **tandas**. Cada tanda entrega el **archivo HTML COMPLETO y actualizado**, nunca fragmentos de código para integrar a mano.
- Dime siempre **qué archivo abrir / reemplazar** (el nombre exacto).
- **No quites mecánicas que ya funcionan.** No rompas lo que ya está probado.
- **No digas que lo probaste en mi teléfono o en mi PC.** Solo puedes verificar con `node --check` y pruebas simuladas en Node; la prueba real la hago yo y te doy feedback con capturas.
- Cuando yo te dé feedback de una prueba real, corrige exactamente eso, sin cambiar otras cosas.
- El juego debe seguir funcionando **offline, en un solo archivo**, sin URLs externas.
- Responde en español, informal y directo.
- El código debe ser completo, listo para copiar y pegar.

## 3. ESTADO ACTUAL — TANDA 14 (15 de noviembre de 2026)

El archivo actual es `experimento_001_tanda14.html` (382.674 bytes, 5.888 líneas). La Tanda 14 es la última y está probada por mí en el celular. Las Tandas 3 a 13 quedan guardadas intactas, no las toques.

### 3.1 Base del juego (Tanda 2, probada por mí, está bien)

- Canvas 640×360, mundo de **9600 px** de ancho (Misión 1), fin de misión en X=9500, 60 actualizaciones/segundo.
- El Capitán: moverse, saltar, agacharse, apuntar arriba, correr (Shift / RUN), recargar (R en PC, automática en táctil), disparar en ambas direcciones. Sprites del Capitán embebidos en base64.
- **3 vidas.** Checkpoints. Al perder las 3 vidas y continuar desde checkpoint, **se pierden las míticas pero se conservan las cartas normales y los combos**.
- **4 armas:** Pistola (infinita), Ametralladora, Escopeta, Láser. 4 cofres, cada uno da un arma + una carta.
- **Enemigos base:** Grunt, Runner, Gunner, Heavy (9 HP).
- **Jefe final de la Misión 1: Comandante Experimental, 48 HP, fase de furia al 50%.**
- **Cartas:** 6 familias — POTENCIA +8% daño, SOBRECARGA +7% cadencia, RESILIENCIA +120 ms invulnerabilidad, REFLEJOS +6% velocidad, PRECISIÓN +4% crítico (crítico = daño doble), RECICLAJE +8% ahorro de munición. Rarezas: común 60% ×1, rara 25% ×1.5, épica 11% ×2, legendaria 4% ×3. Máx 48 cartas normales, máx 12 por familia. Al recibir un golpe se pierde una carta normal al azar, que cae físicamente y se puede recuperar en **5 segundos**. 5 combos, se crean solos.
- **Poderes míticos (4, NO son una 5ª rareza):** JETPACK INFERNAL 6.5 s, TORMENTA ELÉCTRICA 6 s, BOMBARDEO ORBITAL (instantáneo), ADRENALINA ABSOLUTA 7 s. Máx 3 guardados, sin duplicados.
- **Barricadas:** bloquean al jugador, a los enemigos y a los proyectiles enemigos; los proyectiles del jugador pasan.

### 3.2 Misión 1 larga y especial (Tanda 5)

- Duración estimada **~8-10 minutos** (antes duraba 10-20 segundos porque se podía correr y pasar de los enemigos).
- **8 puertas de oleada** (X 650, 1550, 2750, 3950, 5150, 6350, 7550, 8950) que bloquean el avance hasta eliminar a todos, con el aviso "ELIMINA A TODOS PARA AVANZAR · QUEDAN: N".
- **6 cofres.** Temporizador de misión en el HUD (mm:ss) y pantalla de fin con el tiempo.
- **4 zonas, cada una con su paleta, su diálogo de El Capitán, su giro, su enemigo especial y su evento:**
  - **Zona 01 Desembarco (0–2400):** Explorador de Playa (2 HP, carga rápido). Evento en X 650: ¡ALARMA! (sirena, sacudida, 3 Runner de refuerzo).
  - **Zona 02 Perímetro Militar (2400–4800):** Centinela Acorazado (6 HP, lento, bloquea disparos frontales — no el láser ni por la espalda). Evento en X 2900: Suministros lanzados (+60 munición, carta rara).
  - **Zona 03 Resistencia (4800–7200):** Emboscador (3 HP, escondido como montículo con "?" hasta que el jugador se acerca, luego salta y dispara 3 perdigones). Evento en X 5300: Superviviente (+1 vida, carta rara).
  - **Zona 04 Instalación (7200–9600):** Dron Experimento 7 (4 HP, vuelo en seno, dispara desde arriba). Evento en X 7700: ¡Apagón! (~3-6 s de oscuridad con linterna).
- **2 decisiones con 2 rutas y 2 finales** (ver sección 3.6, rutas como mapas distintos).
- **Casa de Cambio en X 5600** (lugar seguro): casa dibujada con ventanas amarillas y letrero "CASA DE CAMBIO". Se abre con E cerca de ella, tocándola, o con el botón grande **"🛒 COMERCIAR"** (dorado, pulsante, centrado sobre la barra de botones, solo aparece cerca de la casa). Reglas: [1] 2 cartas → 1 carta de la familia elegida (teclas 1–6 o toque), [2] 1 carta → +50 XP, [3] 1 carta → +60 munición (si solo tienes pistola, +50 XP).

### 3.3 DROP MACHINE y árbol de habilidades (Tandas 3, 4 y 6)

- La DROP MACHINE es **solo para XP: 10 XP × multiplicador** (×2 = 20, ×3 = 30, ×5 = 50 XP). **100 XP = 1 punto de habilidad.**
- **Tanda 4:** la DROP MACHINE es estilo pinball: lanzador de resorte a la derecha (mantener el canal derecho o Espacio para cargar 0–100% en ~1 s, soltar dispara), **3 bumpers (+5 XP por golpe, 30 fotogramas de enfriamiento por bola)** y una fila de pines que se mueve.
- **Tanda 6 (arreglo de mi prueba):** el contador de bolas ya NO se reinicia: cada lanzamiento resta 1, cada bola da su extra **una sola vez**, con tope de 12 bolas extra por sesión (**máx 24 bolas por sesión**). Al acabarse, pantalla **"DROP TERMINADO"** con XP total, puntos y bolas jugadas (~2.5 s, o toque / T para saltar), y luego se abre el árbol de habilidades automáticamente.
- **Árbol de habilidades permanente, en forma de árbol de verdad:** tronco abajo, 6 ramas que se abren, cada rama una columna vertical de **5 nodos circulares (I–V)** unidos por líneas de colores. Nodo comprado = relleno, siguiente nivel = borde dorado pulsante con su costo ("2 PT"), MÁX en dorado. Se compra tocando el nodo en orden o con las teclas 1–6. **6 ramas (las mismas 6 familias de cartas), 5 niveles cada una (I–V), costos 1, 1, 2, 2, 3 puntos** (9 por rama, 54 en total). Guardado en **localStorage, clave `experimento001_skills_v1`**. `restartGame()` NO lo borra. Se abre con **T** o el botón táctil **HAB**; el juego se pausa mientras está abierto.

### 3.4 Auto-apuntado y enfoque en esquivar (Tanda 7)

- **El juego apunta solo, yo solo disparo.** Al disparar, el juego elige al enemigo vivo más cercano en rango (460 px horizontal / 300 px vertical) y **prefiere a los voladores**; la bala va en diagonal (45° hacia arriba) si el objetivo está arriba, recta si está a nivel. Sin enemigo en rango, dispara recto hacia adelante. Hay una **retícula amarilla** sobre el objetivo apuntado. Apuntar arriba con W / flecha arriba en PC sigue como anulación manual.
- **El enfoque del juego es ESQUIVAR, no apuntar.**
- **Centinela Acorazado ya se puede matar (era un bug: bloqueaba el 100% de frente y era inmortal con pistola/escopeta):** su escudo ahora reduce el daño a la mitad (chip damage 50%) y **se rompe a los 3 impactos frontales**, quedando roto **4 segundos** con daño completo. El láser atraviesa y por la espalda hace daño completo. Sigue lento, 6 HP. Medido en simulación: pistola lo mata en 8 disparos, escopeta en 3.
- **Botones simplificados: de 12 a 9 (+ COMERCIAR contextual), más grandes (56×60 px, utilidades 48×50).** Eliminados: ↑ (apuntar, ya lo hace el auto-apuntado), R táctil (recarga automática), ↻ + PWR (dos botones de mítica), segundo botón de disparo duplicado. **Mítica en un solo botón ★:** tocar = usar la mítica, mantener 0.5 s y soltar = cambiar a la siguiente. En PC siguen E (usar) y Q (cambiar).
- **Recarga automática** al vaciar el cargador; R en PC sigue como recarga manual.
- **Esquiva:** botón **ESQ** (táctil) y tecla **C** (PC): dash corto con **0.4 s de invulnerabilidad** y **2 s de enfriamiento**, con indicador en el botón y en el HUD. Correr, saltar y agacharse siguen igual. El daño enemigo no se tocó: esquivar es la habilidad, el juego no se hizo más fácil.

### 3.5 Cambio de objetivo, cinemática del jefe y eventos jugables (Tanda 8)

- **Cambio de objetivo:** botón táctil **"OBJ"** (pequeño, junto al disparo), tecla **TAB** en PC, o **tocar directamente al enemigo** en pantalla. Una vez elegido a mano, el auto-apuntado se queda fijo en ese enemigo (**FIJO**, retícula naranja más gruesa con marcador "FIJO") hasta que muera, salga de rango o se cambie a otro; solo entonces vuelve a elegir solo.
- **Cinemática de entrada del jefe:** cuando aparece el Comandante Experimental, cinemática de **~3 segundos, saltable con cualquier tecla o toque**: cae del cielo y entra caminando desde la derecha, con sacudida de pantalla, tarjeta grande "COMANDANTE EXPERIMENTAL — EL JEFE FINAL DE LA MISIÓN 1" y su barra de vida entrando deslizándose. Jugador y enemigos en pausa durante esos ~3 s.
- **Eventos visuales y JUGABLES, no solo un letrero** (el texto del banner queda solo como subtítulo; el evento pasa en el mundo y el jugador decide/reacciona):
  - **Alarma (Zona 01):** bordes rojos parpadeando ~5 s + sacudida, refuerzos entran **corriendo a la vista desde la derecha** (3 corredores + 1 explorador). Hay que pelearlos o esquivarlos.
  - **Suministros (Zona 02):** una **caja cae del cielo con paracaídas** y aterriza con polvo y sacudida. (Ver 3.7: ahora se abre agachándose.)
  - **Superviviente (Zona 03):** el superviviente **sale caminando de entre los escombros y saluda con el brazo** (con su "!" encima). Al llegar hasta ti se abre su decisión: [1] Rescatarlo (+1 vida y carta rara, pero llegan 2 drones) o [2] Ignorarlo (se aleja caminando, sin recompensa ni emboscada).
  - **Apagón (Zona 04):** dura ~6 s; la escena se oscurece de verdad salvo un **círculo de linterna alrededor del Capitán**, con chispas, y los **enemigos no te ven (no disparan) a más de 220 px**. Decisión real: avanzar con cuidado o agacharse y aguantar.

### 3.6 Rutas como mapas distintos (Tanda 10)

- En la bifurcación de X 4600 el camino se divide de verdad, con letrero en el mundo ("↑ TÚNEL · RUTA A / → SUPERFICIE · RUTA B").
- **RUTA A — SUBTERRÁNEO:** mapa oscuro propio (techo de roca con estalactitas, tuberías, lámparas tenues que parpadean, suelo de roca oscura con rieles y charcos; nada de cielo ni edificios). Enemigos propios: emboscadores (firma del túnel) y corredores-rata. Jefe de ruta: **REY RATA DEL SUBTERRÁNEO (30 HP, grande, marrón, corona dorada y cola; carga hacia ti, más rápido de lejos, y cada ~6 s cría una rata)**. Cofre propio con láser en X 5600 y +50 XP al bajar.
- **RUTA B — SUPERFICIE:** mapa verde abierto de la Resistencia, con plataformas metálicas propias. Enemigos propios: centinelas (firma de la superficie), artillero, pesado. Jefe de ruta: **CENTINELA MAYOR (30 HP, más grande, azul acero; escudo frontal como el Centinela — chip 50%, se rompe a los 3 impactos, 4 s roto — con triple disparo)**. Cofre propio con escopeta en X 5600.
- Los jefes de ruta son distintos en nombre, aspecto, HP (30, no 48 como el final) y comportamiento, y NO tienen la cinemática del Comandante: al aparecer solo muestran su nombre en grande con sacudida. Al caer, cada uno suelta carta épica + 50 XP.
- **El progreso general NO se toca al cambiar de mapa:** puntos, XP, puntos de habilidad, cartas, combos, míticas, armas, munición, vidas y tiempo viven en las mismas variables; cambiar de ruta solo cambia el mapa, la paleta/fondo, las plataformas y la oleada 5.
- Ambas rutas convergen en la Zona 04 Instalación y en el mismo jefe final (Comandante Experimental, 48 HP). Finales distintos: Ruta A = carta legendaria + 150 XP; Ruta B = carta épica + 100 XP + 1 vida. El HUD muestra "RUTA A · SUBTERRÁNEO" o "RUTA B · SUPERFICIE".

### 3.7 Caja de suministros y puerta trabada (Tanda 9)

- **La caja de suministros se abre AGACHÁNDOSE junto a ella ~0.8 s** (↓ en táctil, S/↓ en PC), con barra de progreso verde "ABRIENDO..." y pista "▼ AGÁCHATE PARA ABRIRLA ▼". Ya NO se agarra con E ni tocándola. Si te alejas o te levantas, el progreso se pierde. Recompensa: +60 munición y carta rara, con emboscada de 2 corredores.
- **Puerta trabada (bug encontrado en mi prueba):** el Emboscador escondido no se podía matar ni alcanzar y su oleada bloqueaba la puerta para siempre (mi captura: Zona 03, Ruta A, "ELIMINA A TODOS PARA AVANZAR" con el Emboscador en el borde derecho). Arreglos: el Emboscador salta a **320 px** (antes 180), salta si estás trabado en su puerta, se le puede disparar al montículo para hacerlo saltar, ya revelado te persigue, y si un enemigo bloqueador lleva **~10 s fuera de pantalla regresa a la arena**. El aviso muestra **"QUEDAN: N"** y hay una **flecha amarilla en el borde** hacia el enemigo que falta, con su nombre y distancia.

### 3.8 Ruta opcional, progreso por mapa y spawns con lógica (Tanda 11, lo último)

- **La ruta NO es obligatoria.** Pasar de largo por la puerta oscura de X 4700 no te mete en ningún sitio: se sigue derecho por la superficie. **Se entra y se sale AGACHÁNDOSE en la puerta, en los dos sentidos** (~0.5 s, con barrita de progreso y fundido): en superficie dice "SUBTERRÁNEO · ▼ AGÁCHATE AQUÍ PARA BAJAR ▼" y dentro del túnel "SUPERFICIE · ▼ AGÁCHATE AQUÍ PARA SALIR ▼". La puerta se re-arma solo al **soltar** agacharse (si no, al mantener agachado rebotaba de mapa).
- **Cada mapa tiene su propio progreso, congelado al salir.** Cada mapa guarda su oleada 5 (vivos/muertos con su vida, spawns pendientes, jefe de ruta y su vida, cofre de ruta, superviviente). Al salir, ese estado se congela exacto: nada reaparece ni avanza mientras no estás ahí. Al volver, se reanuda idéntico. Los jefes son independientes: matar al Rey Rata no toca al Centinela Mayor. La barra "AVANCE DE MISIÓN" sigue siendo la del progreso general (x/9500) y no se resetea al cambiar de mapa.
- **La puerta nunca exige matar a un enemigo fuera de alcance** (mi captura: "QUEDAN: 2" con el Rey Rata al borde). Los spawns de oleada se fijan **dentro de la arena, antes de su puerta**; si un enemigo queda más allá de la puerta, se le trae de vuelta a la arena; si lleva ~3 s a más de 500 px sin poder alcanzarlo, viene a por ti.
- **Los spawns tienen lógica, no aparecen de la nada:** hay **19 edificios con nombre y puerta propia** (CASA, TIENDA, TALLER, FARMACIA, BAR, MERCADO, HOTEL, PANADERÍA, FERRETERÍA, ESCUELA, CINE, BANCO, CLÍNICA...) dibujados con letrero y puerta a nivel de suelo; en el subterráneo, **5 alcantarillas** (y bocas de tubería). Los enemigos salen **POR ESAS PUERTAS**: la puerta brilla con "!" y luz amarilla ~0.75 s antes, y el enemigo emerge visible (~0.5 s). En el subterráneo salen de túneles, tuberías y alcantarillas. Ningún enemigo aparece de la nada en suelo abierto.
- Bonus: el Rey Rata ya no cría ratas después de muerto.

### 3.9 Diálogos (Tanda 6)

- Todos los diálogos de El Capitán están en un **banner inferior** (y 306–348, semi-transparente, nunca en el centro de la pantalla). Cada diálogo tiene su bandera y **se muestra solo una vez por partida**; volver atrás o huir nunca lo vuelve a activar. Solo `restartGame` reinicia las banderas. Se oculta solo tras ~4 s, se puede cerrar con cualquier tecla/toque, y hay 4.5 s de enfriamiento para que no se apilen. Los diálogos NO se quitaron, solo se cambió su comportamiento y su visualización.

### 3.10 Verificación de la Tanda 11

- `node --check` del JS extraído: OK.
- Prueba simulada: **44 PASS, 0 FAIL** (entrar/salir agachándose en ambos sentidos, progreso por mapa congelado, jefes independientes, barra sin reset, puerta sin traba con enemigos lejanos, spawns en puertas visibles, `draw()` sin errores).
- **La prueba en mi teléfono YA ESTÁ HECHA.** Yo ya probé la Tanda 11 en mi celular y te di mi feedback. **No me pidas que la pruebe primero, no me digas que falta probarla, no esperes a que yo te diga qué tanda toca: avanza directamente con el siguiente paso (sección 4).**

### 3.11 ¡ATENCIÓN! La Tanda 12 que subiste NO es la Misión 2

Subiste a GitHub `experimento_001_tanda12.html` ("Misión 2: Sector Industrial", 14 nov 2026, 11:30 CST). **Esa tanda NO vale como Misión 2.** La hiciste con el prompt VIEJO, antes de que escribiéramos la historia, y por eso inventaste un Sector Industrial genérico que no tiene nada que ver con la historia.

**NO la uses como base. NO la repitas. La base sigue siendo la Tanda 11.**

La Misión 2 real es la de **Yuki en Tokio** (sección 4). Hazla como **Tanda 13**, basada en la Tanda 11, no en la Tanda 12.

### 3.12 Tanda 13 — Misión 2: Yuki en Tokio (HECHA, 14 nov 2026, 11:44 CST, por Gravity)

- Archivo `experimento_001_tanda13.html` (5002 líneas). **En ese momento era la base actual: Tanda 13, NO Tanda 11 ni Tanda 12.** (Hoy la base actual es la Tanda 14, ver 3.13.)
- 4 zonas: Akihabara, Shinjuku, Archivo Clandestino, Estación Shibuya. Enemigos: shinobi, ciberagente, mecha sentry. Jefe: El Científico del Secuestro, 48 HP, fase de furia.
- Momento de nostalgia: servilleta con el dibujo de Hana, +1 vida y carta legendaria, diálogos de Yuki y El Capitán.
- Hana desbloqueable: al terminar la Misión 2, `localStorage experimento001_hana_unlocked = true`, selector Capitán / Yuki / Hana. Hana +15% velocidad, Yuki +10%.
- **Probada por mí en el celular: sirve excelente.**
- La Tanda 12 (Sector Industrial) queda descartada, no es base de nada.

### 3.13 Tanda 14 — Misión 3: Amara en Dakar (HECHA, 15 nov 2026, por Claude)

- Archivo `experimento_001_tanda14.html` (382.674 bytes, 5.888 líneas). **Base actual: Tanda 14, NO Tanda 11, ni Tanda 12, ni Tanda 13.**
- 4 zonas: Mercado de Sandaga, Puerto y Corniche, Archivo de la «ONG», Mi Escuela. Enemigos: Asaltante de la «ONG» (carga hasta ~80 px, dispara 3 perdigones). Evento: una camioneta blanca sin placas llega y bajan los asaltantes. Jefa: la Directora del Proyecto en África, 48 HP, fase de furia al 50%. **No muere:** se rinde y Amara la sienta en un salón frente al pizarrón «NADIE ES UN EXPERIMENTO».
- Momento de nostalgia: el expediente «Experimento 003… Recomendación: uso como arma de asalto» y después la grabación en wolof; Amara vuelve a cantar bajito por primera vez en dos años. Da +1 vida, carta legendaria y +150 XP, solo una vez por partida.
- Selector: Capitán / Yuki / Hana / Amara. Amara +10% de daño. Hana sigue desbloqueándose solo al terminar la Misión 2.
- Arreglos incluidos: el teclado de PC ya funciona (error `cy is not defined` corregido), el selector del HUD ya no está tapado, «REPETIR M2» funciona, continuar desde checkpoint en la M2 usa los enemigos de su misión, el cronómetro arranca en 00:00 en cada misión, y la pantalla de fin ya no pisa los botones ni la frase final.
- **Verificación: PASS en los 8 controles (base Tanda 13, Misión 3 completa, jefa no muere, selector con Amara, Hana intacta, sin sistemas inventados, arreglos en código, `node --check` OK). Commit en GitHub `68870dc`.**
- **Probada por mí en el celular: me gustó, el nivel de Amara se siente con más vida.**
- La Tanda 12 (Sector Industrial) queda descartada, no es base de nada.

## 4. HISTORIA (ESCRITA EL 14 DE NOVIEMBRE DE 2026 — LÉELA, ES LA BASE DE TODO)

El gobierno encontró tecnología alienígena caída del cielo, secuestró a 4 personas que no tenían nada que ver entre ellas, les hizo experimentos, y ahora escapan juntos. **Son 5 misiones en total, mínimo.**

- **Misión 1 (ya hecha, Tanda 11):** los 4 escapan juntos de la Instalación, peleando contra el Comandante Experimental. No solo El Capitán, los 4 juntos, con diálogos entre ellos.
- **Misión 2 — YUKI (Tokio, Japón):** Yuki vuelve a buscar a su hermana Hana. Su momento de nostalgia: encontrar un dibujo de Hana que hizo en una servilleta antes de que la secuestraran. Jefe: el científico que la secuestró. **Al terminar esta misión se desbloquea Hana como personaje seleccionable en el lugar de Yuki — NO es un quinto experimento, siguen siendo 4. Antes de terminar la misión, Hana ni aparece en el menú: es un easter egg.**
- **Misión 3 — AMARA (Dakar, Senegal):** maestra de primaria, recupera su escuela convertida en laboratorio. Su momento: encontrar una grabación de ella cantando para sus niños y volver a cantar después de 2 años.
- **Misión 4 — VIKTOR (Moscú, Rusia):** ex soldado, vuelve con su esposa Irina y su hija Katya. Su momento: encontrar las 47 cartas que escribió y nunca mandó.
- **Misión 5 — EL CAPITÁN (Daniel Reyes, México):** vuelven a la Instalación a cerrarla. Jefe final: el director del proyecto.

Los 4 personajes (archivo `HISTORIA-EXPERIMENTO-001.md` en el repo, léelo completo):
- **El Capitán / Daniel Reyes, México:** mecánico de Durango, vivía con su mamá y su hermanito. Fue el primero, le hicieron lo peor. Lidera porque se acuerda de cómo era tener familia.
- **Yuki Tanaka, Japón, 22 años:** estudiaba diseño, vivía con su hermana Hana (16). Dibujaba en servilletas. Poder: velocidad y reflejos.
- **Amara Diallo, Senegal, 29 años:** maestra de primaria en Dakar, vivía con su abuela. Poder: fuerza sobrehumana.
- **Viktor Petrov, Rusia, 34 años:** ex soldado, esposa Irina, hija Katya (5). Poder: resistencia y regeneración.

**Cada misión tiene que ser profunda, no solo enemigos y venganza:** tiene que tener un momento de nostalgia, un recuerdo, una canción, una foto, una carta, un dibujo, diálogos interesantes entre los personajes. La historia no es de venganza, es de **volver a ser personas**.

## 5. QUÉ QUIERO HACER AHORA (SIGUIENTE PASO)

**La prueba de la Tanda 14 YA ESTÁ HECHA por mí en mi celular. No me pidas probarla, avanza directamente.**

El siguiente paso es:

1. **Misión 4 — VIKTOR EN MOSCÚ, como Tanda 15, basada en la Tanda 14 (NO en la Tanda 12 ni en la Tanda 13):** su propio mapa (Moscú, Rusia), su propio enemigo especial, su propio evento, su propia decisión/ruta, su propio jefe (su comandante, el que lo vendió al gobierno por dinero; Viktor lo derrota pero NO lo mata, lo deja vivir), su momento de nostalgia (las 47 cartas que escribió y nunca mandó; las lee una por una y dice: «Yo no quiero ser un héroe. Yo quiero ser un papá. Nomás eso»). Viktor es ex soldado, vuelve con su esposa Irina y su hija Katya. Selector: Capitán / Yuki / Hana / Amara / Viktor.
2. Después: Misión 5 (El Capitán, volver a la Instalación a cerrarla), más profundidad en la DROP MACHINE, más sinergias de cartas, el cooperativo local para 2 jugadores en una PC, y pulido de arte/sonido solo cuando yo lo pida.

**SIEMPRE usa el prompt más nuevo del repo de GitHub (`QuitsT/EXPERIMENTO-001`, archivo `PROMPT_CONTINUIDAD_ANTIGRAVITY.md`). Si el prompt que tienes no menciona a Yuki, Hana, Amara, Viktor y las 5 misiones, es un prompt VIEJO: no lo uses, pide el nuevo.**

## 6. COSAS QUE NO QUIERO (TODAVÍA)

- No rediseñes el arte (los enemigos son rectángulos a propósito, por ahora).
- No añadas música de fondo (todavía no).
- No hagas un jefe nuevo por tu cuenta sin que lo acordemos (ya me lo preguntaste una vez y te dije que no, que lo hacemos juntos).
- No toques la Tanda 14 ni las tandas anteriores; la siguiente tanda es una copia nueva (**Tanda 15**) basada en la Tanda 14. La Tanda 12 (Sector Industrial) NO es base de nada.
- No me pidas instalar nada ni activar ningún servidor: el juego es un archivo HTML que abro en el navegador.

## 7. ARCHIVOS QUE TE PASO

- **`experimento_001_tanda14.html`** — el código actual, completo. Este es el archivo que debes copiar y modificar para la siguiente tanda. **NO uses la Tanda 12 como base, ni la Tanda 13: la base es la Tanda 14.**
- Este prompt — léelo completo antes de tocar el código. **Si tu copia no tiene la sección 4 (Historia, Yuki, Hana, Amara, Viktor, 5 misiones), es vieja: usa la del repo de GitHub.**

Empieza confirmándome que leíste el prompt y el código, y **avanza directamente con la Misión 4 — Viktor en Moscú (Tanda 15)**. No me pidas que pruebe la Tanda 14 primero: esa prueba ya está hecha.
