# NebaCosmeticsWebsite3d

Sitio web interactivo de **NEBA Cosmetics** enfocado en el producto estrella **NEBA-10 Gel Corporal** (200 g) con experiencia 3D en tiempo real (Three.js) y animaciones fluidas con GSAP y ScrollTrigger.

## Tecnologías
- **HTML5 & CSS3** responsive y optimizado.
- **Three.js r128**: renderizado del modelo 3D del tubo y caja modelados en Blender con texturas PBR y control interactivo en 360°.
- **GSAP 3 & ScrollTrigger**: scroll interactivo, transiciones botánicas y fijación cinemática.
- **Modelos 3D**: GLB optimizados y base64 para carga instantánea.

## Estructura del Proyecto
- `index.html`: Landing page principal.
- `assets/`: Imágenes webp optimizadas, videos y logos.
- `neba10_tubo_blender.js`: Modelo 3D del tubo NEBA-10 empaquetado para web.
- `neba10_caja_blender.js`: Modelo 3D de la caja NEBA-10 empaquetado para web.
- `neba10_tubo_blender.glb`: Modelo GLB estándar del tubo.
- `neba10_caja_blender.glb`: Modelo GLB estándar de la caja.
- `favicon.ico` / `assets/favicon.png`: Favicon oficial.

## Despliegue
Sitio estático listo para ser servido con Nginx u otro servidor HTTP con compresión gzip/brotli y soporte SSL.
