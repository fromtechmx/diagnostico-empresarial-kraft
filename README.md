# Diagnóstico de Salud Empresarial — Corporación Kraft

Cuestionario interactivo de diagnóstico empresarial basado en la metodología de 5 bloques de Corporación Kraft. Funciona como archivo HTML estático — sin backend, sin instalación, abre directo en el navegador del celular.

---

## Cómo usarlo

1. Descarga o clona el repositorio
2. Abre `KRAFT_Diagnostico_Salud_Empresarial.html` en cualquier navegador
3. Listo — no requiere servidor, internet ni dependencias

Para compartirlo con un cliente: manda el archivo por WhatsApp o súbelo a Google Drive como público y comparte el link.

---

## Cómo personalizar

Todo el contenido editable está en el bloque `<script>` al final del archivo, en el array `BLOQUES`. Cada objeto representa un bloque del diagnóstico.

### Estructura de un bloque

```js
{
  id: 1,                              // Número del bloque (no cambiar)
  nombre: 'Arquitectura Empresarial', // Nombre visible en la tarjeta
  desc: 'Estructura y responsabilidades', // Subtítulo corto
  color: 'var(--c1)',                 // Color del bloque (ver paleta abajo)
  preguntas: [
    '¿Pregunta uno?',
    '¿Pregunta dos?',
    // ... siempre 5 preguntas por bloque
  ]
}
```

### Cambiar preguntas

Localiza el bloque que quieres editar dentro del array `BLOQUES` y reemplaza el texto de cada pregunta dentro del array `preguntas`. Cada bloque tiene exactamente 5 preguntas — si cambias ese número, actualiza también el divisor en `updateBlockScore`.

### Cambiar nombres de bloques

Edita los campos `nombre` y `desc` de cada objeto en `BLOQUES`.

### Paleta de colores por bloque

Los colores están definidos en `:root` al inicio del `<style>`:

```css
:root {
  --c1: #00B4D8;  /* Bloque 1 — Arquitectura */
  --c2: #9A5AEE;  /* Bloque 2 — Educación */
  --c3: #F0B429;  /* Bloque 3 — Dominio */
  --c4: #52C97F;  /* Bloque 4 — Financiero */
  --c5: #E85555;  /* Bloque 5 — Comercial */
}
```

Cambia el valor hex para modificar el color de un bloque completo (tarjeta, slider, barra de resultado).

### Cambiar colores de marca

```css
:root {
  --navy: #1F3A5F;   /* Color principal — headers, textos oscuros */
  --lime: #A8CC00;   /* Acento — porcentaje global, etiquetas */
  --cyan: #00B4D8;   /* Acento secundario */
}
```

### Cambiar nombre y datos de la marca

En el `<header>` del HTML:

```html
<div class="hdr-brand">CORPORACIÓN <em>KRAFT</em></div>
```

En el pie de resultados (`res-firma`):

```html
<div class="rf-name">Corporación Kraft × FROM TECH 4D</div>
<div class="rf-contact">jaimepasa@jaimepasa.com<br>fromtechmx@gmail.com · 378 111 4980</div>
```

### Cambiar los rangos de estado de salud

El array `ESTADOS` define cómo se interpreta el porcentaje global:

```js
const ESTADOS = [
  { min: 0,  max: 25,  label: 'En riesgo',      ... },
  { min: 26, max: 50,  label: 'Por desarrollar', ... },
  { min: 51, max: 75,  label: 'En crecimiento',  ... },
  { min: 76, max: 100, label: 'Empresa sólida',  ... },
];
```

Ajusta los rangos `min`/`max` y el `label` según la escala que prefieras.

### Cambiar los textos de alerta por nivel

El array `ALERTAS` define qué se muestra debajo de cada bloque en los resultados según el porcentaje obtenido:

```js
const ALERTAS = {
  0: { text: 'Área crítica — requiere atención inmediata',          icon: '🔴' },
  1: { text: 'Área débil — bloque prioritario de intervención',     icon: '🟠' },
  2: { text: 'Área en desarrollo — avance posible con acciones',    icon: '🟡' },
  3: { text: 'Área sólida — mantener y optimizar',                  icon: '🟢' },
};
```

El nivel se calcula así: `< 26% → 0`, `26-50% → 1`, `51-75% → 2`, `76%+ → 3`.

---

## Agregar o quitar un bloque

1. Agrega o elimina el objeto correspondiente en el array `BLOQUES`
2. Agrega o elimina la clase CSS correspondiente (`.b6`, `.rb6`, etc.) copiando el patrón de los existentes
3. Agrega la variable de color `--c6` en `:root`
4. El cálculo del porcentaje global es automático — divide entre el número de bloques que haya

---

## Despliegue en GitHub Pages

1. Sube el archivo al repositorio
2. Ve a **Settings → Pages**
3. Source: `main` / `root`
4. GitHub genera un link público — ese link funciona directo en celular sin descargar nada

---

## Stack

- HTML + CSS + JavaScript vanilla
- Sin dependencias externas
- Sin backend
- Compatible con Chrome, Safari, Firefox — mobile y desktop

---

## Créditos

Metodología: **Corporación Kraft** — Jaime Alberto Padilla Díaz  
Desarrollo: **FROM TECH 4D** — Edgar Fabián Romero Pérez  
fromtechmx@gmail.com · 378 111 4980 · San Juan de los Lagos, Jalisco, México
