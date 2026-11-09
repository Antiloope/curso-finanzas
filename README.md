# Café y finanzas

Landing de la clase presencial de finanzas personales: sábado 5 de diciembre a la mañana, en Boerr Café (General Paz), con desayuno y un grupo de hasta 7 personas. Es una página estática (HTML y CSS, sin build ni dependencias) publicada con GitHub Pages.

El diseño sale del design system "Café y finanzas" (tokens, componentes, voz y contenido): https://claude.ai/artifact/Sq821tLn7Vkwne7UVK37Ck

## Estructura

| Archivo | Qué es |
| --- | --- |
| `index.html` | La página completa |
| `assets/css/tokens.css` | Colores (tema claro y oscuro), tipografías, espacios y radios del design system |
| `assets/css/estilos.css` | Componentes (clases `fc-`) y layout de la página |
| `assets/img/rodri.jpg` | Foto de "Quién da la clase" (cuadrada) |
| `assets/favicon.svg` | Ícono de la pestaña |
| `.nojekyll` | Hace que GitHub Pages sirva los archivos tal cual, sin procesarlos con Jekyll |

## Verla en tu compu

```bash
python3 -m http.server 8080
```

Después abrí http://localhost:8080. Para ver la versión de celular, usá el modo responsive de las herramientas de desarrollo del navegador.

## Cambiar datos de la clase

Fecha, lugar, horario, precio y cupo aparecen en más de un lugar de `index.html`: la volanta del inicio, el ticket, las preguntas frecuentes y la carta de la reserva. Si cambiás alguno, buscalo en todo el archivo:

```bash
grep -n "5 de diciembre\|Boerr\|30.000\|7 personas" index.html
```

El número de WhatsApp está en el botón de reserva, con el formato `549` + código de área sin el 0 + número sin el 15.

## Publicación

La rama `main` se publica con GitHub Pages (Settings → Pages → "Deploy from a branch" → `main` y `/ (root)`). Cada push a `main` actualiza la página en uno o dos minutos.

- Sin dominio propio: https://antiloope.github.io/curso-finanzas/
- Con dominio propio: https://curso-finanzas.rodripizarro.com.ar

## Dominio propio con Cloudflare

`rodripizarro.com.ar` está registrado en NIC Argentina, que no aloja registros DNS. Por eso el dominio se delega a Cloudflare y los registros se cargan ahí.

1. **Cloudflare:** agregá el dominio (plan Free) y copiá los dos nameservers que te asigna.
2. **nic.ar:** en el dominio, "Delegar" → cargá esos dos nameservers (sin IP) → confirmá los cambios. Esperá el mail de Cloudflare que dice que el dominio está activo.
3. **GitHub, verificación del dominio** (evita que otra cuenta lo use): en tu perfil, Settings → Pages → Add a domain → `rodripizarro.com.ar`. Cargá en Cloudflare el registro `TXT` que te indica (nombre `_github-pages-challenge-antiloope`) y tocá Verify. Ese registro tiene que quedar cargado.
4. **Cloudflare, registro de la página:** `CNAME` con nombre `curso-finanzas`, destino `antiloope.github.io` y proxy apagado ("DNS only", nube gris), para que GitHub pueda emitir el certificado HTTPS.
5. **GitHub, el repo:** Settings → Pages → Custom domain → `curso-finanzas.rodripizarro.com.ar` → Save. GitHub agrega un archivo `CNAME` en `main`, así que después hacé `git pull`.
6. Cuando aparezca el certificado, activá "Enforce HTTPS".

Para revisar el DNS desde la terminal:

```bash
dig +short curso-finanzas.rodripizarro.com.ar
```

Tiene que devolver `antiloope.github.io.` y las IP de GitHub (`185.199.108.153` a `185.199.111.153`).
