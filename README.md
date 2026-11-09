# Finanzas con café

Landing de la clase presencial de finanzas personales: un sábado a la mañana, en un café, con desayuno y 7 lugares. Es una página estática (HTML y CSS, sin build ni dependencias) pensada para GitHub Pages.

El diseño sale del design system "Finanzas con café" (tokens, componentes, voz y contenido): https://claude.ai/artifact/Sq821tLn7Vkwne7UVK37Ck

## Estructura

| Archivo | Qué es |
| --- | --- |
| `index.html` | La página completa |
| `assets/css/tokens.css` | Colores (tema claro y oscuro), tipografías, espacios y radios del design system |
| `assets/css/estilos.css` | Componentes (clases `fc-`) y layout de la página |
| `assets/favicon.svg` | Ícono de la pestaña |
| `.nojekyll` | Hace que GitHub Pages sirva los archivos tal cual, sin procesarlos con Jekyll |

## Verla en tu compu

```bash
python3 -m http.server 8080
```

Después abrí http://localhost:8080.

## Datos a completar

En `index.html` todo lo pendiente está entre corchetes:

- `[FECHA]`, `[CAFÉ]`, `[BARRIO]` y `[PRECIO]` (en el ticket y en la carta de la reserva).
- `[CÓMO SE PAGA Y HASTA CUÁNDO SE PUEDE RESERVAR.]` en la sección de reserva.
- El número de WhatsApp en el botón de reserva: reemplazá `549XXXXXXXXXX` por `549` + código de área sin el 0 + número sin el 15.
- `[TU FOTO]` y la bio en "Quién da la clase". La foto va en `assets/img/` (hay un comentario en el HTML con la etiqueta lista).
- `[DETALLE DEL DESAYUNO]`, `[MEDIO DE RESERVA Y PAGO]` y `[POLÍTICA DE CAMBIOS Y DEVOLUCIONES]` en las preguntas frecuentes.
- `[TU EMAIL O INSTAGRAM]` en el pie.

Para encontrarlos todos:

```bash
grep -n '\[[A-ZÁÉÍÓÚ]' index.html
```

## Publicar en GitHub Pages

1. Creá un repo público en GitHub llamado `curso-finanzas` y subí la rama `main`. En el plan gratis de GitHub, Pages solo funciona con repos públicos.
2. En el repo: Settings → Pages → Build and deployment → Source: "Deploy from a branch" → `main` y carpeta `/ (root)`.
3. En un par de minutos queda en `https://antiloope.github.io/curso-finanzas/`.

## Dominio propio: curso-finanzas.rodripizarro.com.ar

1. Registrá `rodripizarro.com.ar` en NIC Argentina (nic.ar).
2. NIC Argentina no aloja registros DNS: delegá el dominio a un proveedor de DNS (por ejemplo Cloudflare, que tiene plan gratis) cargando sus servidores en la delegación del dominio en nic.ar.
3. En ese proveedor, creá un registro `CNAME` con nombre `curso-finanzas` y valor `antiloope.github.io`. Si usás Cloudflare, dejalo en "DNS only" (sin el proxy) para que GitHub pueda emitir el certificado.
4. En GitHub: Settings → Pages → Custom domain → `curso-finanzas.rodripizarro.com.ar`. Esto agrega un archivo `CNAME` al repo.
5. Cuando GitHub termine de emitir el certificado, activá "Enforce HTTPS".

Opcional: verificá el dominio en la configuración de tu cuenta de GitHub (Settings → Pages → Add a domain) para que nadie más pueda usarlo con su propio repo.
