# Simulador A1: reglas de tránsito (Clase A, Categoría I)

Práctica del examen de reglas de tránsito para la licencia Clase A, Categoría I (A1), en Lima, Perú.
Es una app de HTML, CSS y JavaScript sin frameworks ni backend. Funciona sin conexión.

> No es una herramienta oficial del MTC y no garantiza aprobar el examen.

## Cómo usarla

1. Descarga `index.html` y la carpeta `imagenes/` de Drive. Deben quedar en la misma carpeta.
2. Abre `index.html` con un navegador moderno (Chrome, Edge, Firefox o Safari).
3. No hace falta servidor, cuenta ni internet.

Si falta la carpeta `imagenes/`, la app funciona igual, pero no muestra las señales y te avisa en pantalla.

## Qué hay en Drive

| Elemento | Qué es |
|---|---|
| `index.html` | La app completa. El CSS, el JavaScript y el banco de preguntas van dentro de este archivo. |
| `imagenes/balotario/` | 67 imágenes de señales y gráficos recortados del balotario oficial. Van como archivos sueltos porque incrustarlas inflaría `index.html`. |
| `data/banco-preguntas.json` | Copia legible del banco de preguntas. La app no lo lee: su contenido ya está dentro de `index.html`. |
| `docs/` | Documentos oficiales del MTC que sirvieron de fuente. |
| `README.md` | Este archivo. |

## Modos

| Modo | Qué hace |
|---|---|
| Simulacro | 40 preguntas al azar, sin repetir, en 40 minutos. Aprobado con 35 aciertos o más. Cada intento genera una combinación distinta. Puedes pausar el tiempo y, si se agota, reiniciarlo para seguir en la misma pregunta. |
| Estudio | Practica todo el balotario o un tema. Al responder ves la respuesta correcta, la explicación (si existe) y la fuente. |
| Refuerzo | Practica las preguntas cuya última respuesta fue incorrecta y los temas con bajo rendimiento (menos del 70% de aciertos, con al menos 3 respuestas). |
| Estadísticas | Historial de simulacros, preguntas dominadas, rendimiento por tema y borrado del progreso. |

**Pregunta dominada:** acertada dos veces seguidas. Estos valores están al inicio del script de configuración dentro de `index.html`.

### Simulacro: pausa y tiempo agotado

- **Pausar:** el botón "Pausar" detiene el reloj y oculta las preguntas. Al reanudar vuelves a la misma pregunta, con tus respuestas.
- **Tiempo agotado:** el simulacro no se entrega solo. Puedes reiniciar el tiempo (40 minutos) y seguir desde la misma pregunta, o entregar ahora. Tus respuestas se conservan.
- **Tiempo usado:** en el resultado suma solo los tramos en que el reloj corrió, sin contar las pausas.
- Estas ayudas son para practicar. No reproducen las condiciones del examen oficial.

## Progreso

El progreso se guarda en `localStorage` del navegador. Es local: no se sincroniza entre dispositivos ni navegadores. Si el navegador bloquea el almacenamiento, el progreso dura solo mientras la página esté abierta. Si recargas la página durante un simulacro, el intento se pierde.

## Banco de preguntas

- El banco va incrustado en `index.html`, como `window.BANCO_PREGUNTAS`.
- `data/banco-preguntas.json` es la copia legible de ese mismo banco, con la fuente de cada pregunta.
- Si cambias una pregunta en el JSON, hay que volver a incrustarla en `index.html`. La app no vuelve a leer el JSON.

### Estructura de una pregunta

```json
{
  "id": "A1-001",
  "numeroOficial": 1,
  "tema": "normas-conduccion-vehiculo",
  "enunciado": "Está permitido en la vía:",
  "imagen": null,
  "alternativas": [{ "letra": "a", "texto": "..." }, { "letra": "b", "texto": "..." }],
  "respuestaCorrecta": "c",
  "explicacion": null,
  "fuente": { "id": "balotario-a1-mtc", "referencia": "Pregunta N.º 1, página 1 del PDF" }
}
```

`explicacion` puede ser `null` mientras no esté verificada con normativa oficial. En ese caso la app muestra "Explicación pendiente".

## Estado del contenido

Ver `meta.pendientes` y `meta.fuentes` en `data/banco-preguntas.json`. Resumen:

- **Fuente:** balotario oficial del MTC para Clase A Categoría I (M1, M2 y N1), 200 preguntas numeradas del 1 al 200, con 67 imágenes de señales y gráficos.
- **Vigencia no verificada:** el PDF tiene fecha de creación del 16/01/2018 y no indica resolución ni vigencia. No se pudo confirmar que siga vigente en 2026.
- **Explicaciones pendientes:** el balotario no incluye explicaciones. Se redactarán solo citando normativa oficial verificada.
- **Temas de apoyo:** el balotario oficial trae un solo tema. Los 14 temas de esta app son una agrupación por palabras clave para estudiar. No son oficiales y pueden tener errores de clasificación.
- **Comillas:** en el PDF, algunas comillas aparecen como `¿` (por ejemplo, en la pregunta 3). Se conservó el texto original.
