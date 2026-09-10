# La página pública de BujiOps

**BujiOps** es un CRM para talleres de servicio: motos, bicicletas, máquinas de
coser, instrumentos musicales, carpintería, celulares y cómputo.

Este repositorio es sólo la página que explica el producto. Una sola página
estática: `index.html`, `base.css` y las imágenes. Sin build, sin dependencias,
sin JavaScript. Se publica en GitHub Pages.

Para verla en local basta un servidor estático — `file://` no la sirve igual:

```bash
python3 -m http.server 4500
# → http://localhost:4500
```

## Cómo se publica

Cualquier push a `main`. El workflow prende Pages solo la primera vez
(`enablement: true`), así que no hay nada que configurar a mano, y antes de
subir revisa dos cosas: que exista **cada imagen que el HTML referencia** —una
faltante deja un hueco blanco que nadie nota hasta que lo ve un prospecto— y si
el número de WhatsApp sigue siendo el de ejemplo, avisa.

## Lo que falta para que sirva

**El número de WhatsApp.** Los dos botones apuntan a `wa.me/5210000000000`, que
es un marcador de posición. Escribir por WhatsApp es la única acción que la
página pide: mientras el número no sea el real, publicarla pierde todos los
contactos.

Se cambia en `index.html`, en los dos `href` que contienen `wa.me`, en formato
internacional sin signos: `52` + `1` + los diez dígitos.

## Por qué está hecha así

- **Todas las pantallas son capturas del producto corriendo**, no maquetas. Se
  generan montando los componentes reales del CRM; el detalle del método vive
  en el repositorio del producto. Una maqueta enseña lo que el diseñador quiso,
  no lo que el producto hace.
- **Los nombres, folios y montos son inventados.** Nunca datos de un taller real
  en material público.
- **El botón dice "Escríbenos por WhatsApp" y no "Crear mi taller"** porque hoy
  el alta la hacemos nosotros, taller por taller. Cuando el registro propio esté
  abierto, esto cambia.
- **Sin tipografía web.** El link llega por WhatsApp con datos móviles: una
  familia descargada cuesta entre 40 y 90 KB y un salto de texto al cargar,
  justo en los segundos que deciden si la persona se queda. La pila del sistema
  cuesta 0 KB.
- **Imágenes WebP** y `loading="lazy"` debajo del pliegue. En el teléfono la
  página **carga con 182 KB**; recorrerla entera son ~640 KB, que sólo se paga
  si alguien se queda a verla toda.
- **La paleta y los contrastes son los del CRM.** Quien entra por aquí tiene que
  aterrizar en el producto sin sentir que cambió de empresa.

## Antes de dar por buena una versión

```
axe (wcag2a, wcag2aa, wcag21aa, wcag22aa)   sin faltas, en 1280 y en 390
desbordamiento horizontal                    ninguno
ninguna imagen en blanco                     ni una
peso al cargar en móvil                      182 KB hoy; que no suba sin motivo
```

Y la prueba que decide: **abre la página en el teléfono y no hagas scroll**. Si
un tallerista que no te conoce no entiende qué es y qué gana en diez segundos,
sobra texto o falta imagen.

## Una advertencia para quien edite el texto

La página **afirma cosas sobre el producto**: que sirve para tal rubro, que el
cliente ve su saldo, que los estados los configura el taller. Cada afirmación
tiene que ser verdad **hoy**, no en el roadmap.

Vivir en un repositorio aparte hace fácil olvidarlo: aquí no está el código que
lo respalda. **Antes de publicar un cambio de copy, verifica la afirmación
contra el producto**, no contra lo que recuerdas. Un prospecto que se registra
por algo que no existe se va a la semana, y ésa es la baja más cara porque ya se
pagó por conseguirla.
