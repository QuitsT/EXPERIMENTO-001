# Experimento 001

Juego individual para Fundamentos de Ciberseguridad (Dr. Raúl Villanueva, UNIPOLI).
Run-and-gun 2D estilo Metal Slug, en un solo archivo HTML con Canvas, sin motor externo, sin librerías, offline.

Protagonista: **El Capitán**, primer experimento del gobierno que lideró el escape.

## Cómo jugar

Abre `experimento_001_tanda11.html` en el navegador (PC o celular).

- Mover: ◀ ▶ / flechas
- Saltar: ↑ / botón ↑
- Agacharse: ↓ / S
- Disparar: botón ● (el juego apunta solo, auto-apuntado)
- Cambiar objetivo: botón OBJ / TAB / tocar al enemigo
- Esquiva: ESQ / C (0.4 s invulnerable, 2 s enfriamiento)
- Mítica: ★ (tocar = usar, mantener = cambiar)
- Árbol de habilidades: T / HAB
- Casa de Cambio: agáchate cerca o botón COMERCIAR

## Cómo trabajamos (3 IAs)

- **Archivo maestro:** siempre una sola versión actual (`experimento_001_tandaXX.html`).
- **Prompt maestro:** `PROMPT_CONTINUIDAD_ANTIGRAVITY.md` — léelo completo antes de tocar el código.
- **Tandas:** cada cambio es una tanda nueva, con el archivo HTML completo, nunca fragmentos.
- **Ramas:** cada IA trabaja en su rama (`claude/...`, `gemini/...`, `muse/...`) y se integra en la principal.
- **Pruebas:** `node --check` + pruebas simuladas. La prueba real la hace Quits en su celular.

## Estado

- **Tanda 11 (13 nov 2026):** Misión 1 completa (~8-10 min), 4 zonas, 8 puertas de oleada, rutas como mapas distintos (Subterráneo / Superficie) con jefes propios, auto-apuntado, DROP MACHINE pinball con árbol de habilidades.
- **Siguiente:** Misión 2.
