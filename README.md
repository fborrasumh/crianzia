# CrianzIA

Sistemas de producción de especies menores y acuícolas: cerdos, cuyes, conejos, pollos de engorde, gallinas ponedoras, trucha y tilapia. Aplicación web de un solo fichero, sin servidor.

**Usar la app:** https://fborrasumh.github.io/crianzia/

**Idiomas:** español (por defecto), inglés y portugués; selector en la barra superior (o `?lang=en` / `?lang=pt` en la URL).

## Qué hace

- **Atlas de especies.** Siete especies con generalidades, razas y líneas, reproducción, alimentación, instalaciones, sanidad y bioseguridad, y una ficha de parámetros de referencia.
- **Planificador de la granja.** Con los parámetros de la finca calcula el flujo de producción (destetados, vendidos, cuyes de saca, huevos por gallina alojada…), el alimento por fase, las plazas y superficies de instalaciones, el IEP del pollo, la curva de postura, la biomasa, la ración diaria, el volumen de estanques y el caudal mínimo para trucha, y avisa si la temperatura del agua está fuera del rango de la especie.
- **Costos de producción.** Matriz editable (cantidad × precio, fijos y variables) con las cantidades enlazadas al plan: costo total y unitario, ingresos, utilidad, relación beneficio/costo y punto de equilibrio. Exporta a Word y CSV.
- **Retos con solución calculada.** Diez tipos de problema (conversión, IEP, postura, plazas de ceba, alimento de ceba, cuyes de saca, gazapos, ración de trucha, caudal, punto de equilibrio). Cada estudiante recibe datos propios a partir de su código; la app reconoce la solución y diagnostica los errores típicos (no descontar la mortalidad, olvidar el ×100, gramos y kilos…). El profesorado imprime las hojas de la clase y descarga las soluciones en CSV sin guardar nada: todo se regenera con el código de la actividad.
- **Práctica adaptativa.** 28 preguntas trilingües por unidad del sílabo y nivel de Bloom. Un modelo de dominio por unidad (tipo Elo, con olvido) elige la siguiente pregunta de la unidad más débil, intercala unidades y vuelve sobre las falladas (espaciado); la app explica siempre por qué toca cada pregunta.
- **Proyecto integrador.** Diagnóstico situacional, objetivo, propuesta técnica, plan sanitario, conclusiones y referencias; las tablas del plan y de los costos se insertan solas en el Word. Comprobación de forma de las referencias (DOI, año).
- **Revisión formativa con IA (opcional).** La IA comenta fortalezas y mejoras citando el texto del estudiante; no pone nota.
- **Sílabo.** Ficha, resultado de aprendizaje, calendario con la sesión de hoy marcada, evaluación, bibliografía y una revisión crítica del documento con propuesta de resultados de aprendizaje medibles.
- **Datos y profesorado.** Exportación anónima del registro de práctica, analítica de ítems (dificultad, discriminación, distractores que nadie elige) a partir de varias exportaciones y banco de ítems para Moodle (GIFT).

## Qué calcula el código y qué hace la IA

Todos los números (plan, costos, soluciones y diagnóstico de los retos, modelo de dominio) los calcula el código con fórmulas explícitas; la IA no calcula nada. La IA solo interviene en la revisión del proyecto, con la clave de cada persona (OpenAI, Google Gemini o Anthropic Claude). El código comprueba que cada cita existe en el proyecto, señala las cifras que no están ni en el proyecto ni en los cálculos y descarta los comentarios que ponen nota.

## Privacidad

Todo se guarda en el navegador (IndexedDB). Solo sale información si se pide la revisión con IA: el texto del proyecto, con correos, documentos y teléfonos enmascarados, tras un aviso que muestra lo que se va a enviar. La exportación de datos de práctica usa un seudónimo aleatorio y no contiene nombres ni texto libre.

## Límites

- Los parámetros de referencia y los precios (en USD) son orientativos: dependen de la línea genética, el clima, la altitud, el manejo y el mercado. No sustituyen el criterio técnico ni la normativa sanitaria vigente.
- La comprobación de referencias es solo de forma: la app no consulta ninguna base de datos.
- La app no se ha probado todavía con estudiantes reales ni con una clave de IA real (la IA se probó simulada). Su efecto en el aprendizaje está por medir. Para publicar con los datos que exporta hacen falta aprobación de un comité de ética, consentimiento informado y, idealmente, un diseño preregistrado con grupo de comparación.
- Las curvas de crecimiento y de postura son formas típicas escaladas a los datos de inicio y final, no modelos ajustados a una línea concreta.

## Pruebas realizadas

22 000 comprobaciones de lógica en Node (300 variantes por tipo de reto: solución, errores típicos sin colisiones, determinismo; modelo de dominio: mismos eventos, misma ruta) y una prueba de punta a punta en Chromium: IA simulada de los tres proveedores (con una cita inventada, una cifra inventada y un comentario con nota), error 429, enmascarado, exportaciones Word/CSV/JSON/GIFT sin red, persistencia, funcionamiento sin conexión, cobertura de traducciones, móvil (390 px) en los tres idiomas y accesibilidad con axe-core (WCAG 2.2 A/AA, cero infracciones). Primera pantalla útil en unos 0,6 s con la CPU ralentizada ×4.

## Adaptarla a otra asignatura o universidad

El currículo está en datos: `src/datos.js` (especies, parámetros, costos, sílabo), `src/items.js` (preguntas) y `src/calc.js` (`RETOS`). Se cambian esos ficheros, se traduce en `src/i18n.js` y se monta con `python3 build.py`.

## Autoría

Fernando Borrás Rocher (Universidad Miguel Hernández de Elche) y Jose Alfonso Angel Armas (Universidad Politécnica Estatal del Carchi).

Origen de la idea: a partir del sílabo de Sistemas de Producción de Especies Menores y Acuícolas (0811BSPEMA6UP-AJ2025, nivel 6, Carrera de Agropecuaria, UPEC) del profesor Jose Alfonso Angel Armas: sus bloques de cerdos, cuyes y conejos, aves (engorde y postura) y acuicultura (trucha y peces tropicales), el aprendizaje basado en proyectos y el proyecto integrador de saberes.

Roles (CRediT): Jose Alfonso Angel Armas, conceptualización y recursos (sílabo y contenidos de la asignatura); Fernando Borrás Rocher, software y metodología.

ORCID: Fernando Borrás Rocher [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573) · Jose Alfonso Angel Armas [0009-0001-4066-1028](https://orcid.org/0009-0001-4066-1028)

## Cómo citar

Borrás Rocher, F. y Angel Armas, J. A. (2026). *CrianzIA* (v1.0.0) [Software]. (DOI en trámite)

## Licencia

MIT. Véase [LICENSE](LICENSE). Los contenidos pedagógicos se publican con la misma licencia.
