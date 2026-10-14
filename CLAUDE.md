# NEBA Cosmetics — contexto del proyecto

Sitio web estático (HTML + Three.js r128 por CDN) para NEBA-10 Gel Corporal (200 g).
Se abre con doble clic (file://, sin servidor) → por eso los assets pesados van embebidos en .js en base64
(ver `textures_data.js`, `neba10_tubo_blender.js`). Un .glb suelto NO carga vía file:// (CORS).

## Entorno
- Windows, usuario: `C:\Users\STIVEN ANTEQUERA`
- Blender 5.2.2 con el addon "MCP for Blender" (ahujasid/blender-mcp, paquete `mcp-for-blender`), puerto 9876.
  En Blender: N → pestaña "MCP for Blender" → Start/Connect.
- uv/uvx en `C:\Users\STIVEN ANTEQUERA\.local\bin\uvx.exe`
- Claude Desktop (versión Microsoft Store), config en
  `%LOCALAPPDATA%\Packages\Claude_pzs8sxrjxfjjc\LocalCache\Roaming\Claude\claude_desktop_config.json`
- Para Claude Code: `claude mcp add blender "C:\Users\STIVEN ANTEQUERA\.local\bin\uvx.exe" mcp-for-blender`
  (no usar Claude Desktop y Claude Code conectados a Blender al mismo tiempo)

## Modelo 3D del tubo (hecho en Blender)
Archivo: `blender/neba10_tubo.blend`, colección "NEBA10".
- `Tubo_NEBA10`: malla generada por script. Cuerpo H = 165 mm, radio 25.1 mm (Ø 50.3 mm),
  perímetro = H·6000/6267 (proporción de la etiqueta). Se aplana hacia el sello con f(t)=t^1.35,
  conservando longitud de arco. Tapa abajo (z 0–21 mm), sello arriba (z = 186 mm).
  UV "UVMap": u por tramos (lateral −0.007, frente 0.239, lateral 0.505, reverso 0.759, lateral 0.993).
  UV "UVBake" = UVMap + 0.007 (dentro de 0..1, usada para hornear/exportar).
- Material `Etiqueta_NEBA10`: textura `blender/tubo_label_texture_hd.png` (6000×6267, frente izq / reverso der),
  mezcla con blanco por alpha → Gamma 1.5 ("Contraste_Patron", resalta el patrón de hojas) →
  franja de sello 5 mm arriba sin impresión + estrías verticales (Wave bands escala 350, Bump).
- `Tapa_NEBA10`: torno (spin) Ø ~50.5 mm, alto 21 mm, ranura de apertura a z = 5 mm,
  muesca medio óvalo 16×9 mm, 1.6 mm de profundidad (Boolean con `Corte_Muesca`, oculto) + Bisel.
  Material `Plastico_Verde` (0.006, 0.16, 0.03), roughness 0.22, coat 0.6.
- Render: EEVEE, view transform Standard, exposición −0.45, fondo gris, 3 luces de área
  (Luz_Principal 4.5 W, Luz_Relleno 1.8 W, Luz_Contra 2.5 W), cámara 85 mm de frente.
- `Cube`, `Esfera_Roja` y `Light` (pruebas/default) están ocultos, no borrados.

## Exportación web
- Texturas horneadas: `blender/neba10_web_color.jpg` (4096²), `blender/neba10_web_normal.png` (2048²).
- `Tubo_NEBA10_web` (oculto): copia con material simple `Etiqueta_Web` usada para exportar.
- `neba10_tubo_blender.glb` (3.3 MB) y `neba10_tubo_blender.js` (`window.NEBA10_GLB_B64`).
- `tubo_3d.html`: visor de prueba (GLTFLoader.parse desde base64, OrbitControls, autorotación).

## Pendiente
- Verificar `tubo_3d.html` en el navegador.
- Opcional: reemplazar el tubo procedural de la portada de `index.html` por el modelo de Blender
  (conservar respaldo de `index.html`).
- Opcional: renders PNG con fondo transparente para catálogo/redes; toma inclinada con hojas y flores
  (referencia: `NEBA10-imgen.jpeg` / mockups).

## Caja (14-oct)
- `Caja_NEBA10` en `blender/neba10_tubo.blend`: 70 × 55 × 215 mm (estimado de foto, confirmar medidas reales),
  bisel 0.6 mm, junto al tubo (x 88 mm, rot −12°).
- Textura `blender/caja_neba10_textura.png` (4096², 15 px/mm): fondo `blender/detalles.jpg` (patrón de hojas) +
  tinta extraída de `tubo_label_texture_hd.png` (frente y costados = panel frontal, reverso = ingredientes,
  tapas = logo). Atlas: fila alta y=825..4050 (front 0–1050, back 1050–2100, left 2100–2925, right 2925–3750),
  fila baja y=0..825 (top 0–1050, bottom 1050–2100).
- Web: `blender/caja_neba10_web.jpg` (con gamma 1.5 aplicado), `neba10_caja_blender.glb` / `.js`
  (`window.NEBA10_CAJA_GLB_B64`), visor `caja_3d.html`.
- `atras-03.svg` no se usó (Blender no lo carga como imagen).

- Ajuste 14-oct 02:10: caja bajada a 70 × 55 × 190 mm (mínimo para el tubo de 186 mm); costados solo con patrón; frente = presentación, reverso = ingredientes.
