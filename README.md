## 📋 Parte 1 — Descripción del proyecto

### 1.1 El problema jurídico

El problema jurídico que resuelve nuestra herramienta es determinar si un aumento del canon de arrendamiento de vivienda urbana en Colombia cumple con los límites establecidos por la ley. Este problema afecta principalmente a arrendatarios que reciben aumentos y no saben si el valor cobrado es legal. Actualmente, pueden buscar información en internet, hacer cálculos por su cuenta o consultar a un abogado, lo que puede resultar confuso. Nuestra herramienta permite realizar una primera verificación de manera sencilla y conocer la norma aplicable.

### 1.2 Usuarios

El usuario ideal es un arrendatario colombiano de vivienda urbana al que le aumentaron el canon y quiere saber si el aumento cumple con la ley. También puede ser utilizada por arrendadores que quieran verificar sus aumentos. Está dirigida principalmente a personas sin conocimientos especializados en derecho. Al finalizar el proyecto, al menos un usuario real probará la herramienta.

### 1.3 Qué hace y qué NO hace (alcance)

| ✅ Sí hace                                                        | ❌ No hace                                         |
| ---------------------------------------------------------------- | ------------------------------------------------- |
| Calcula el aumento máximo permitido.                             | No reemplaza la asesoría de un abogado.           |
| Verifica si han pasado los 12 meses necesarios para el reajuste. | No representa al usuario ante autoridades.        |
| Compara el aumento con el límite legal.                          | No determina el resultado de un proceso judicial. |
| Explica las normas aplicables.                                   | No redacta ni presenta demandas.                  |
| Cita la fuente normativa utilizada.                              | No analiza otros tipos de contratos.              |

*Consejo de abogado: un alcance pequeño y perfecto vale más que uno grande y roto.*

### 1.4 Marco jurídico y fuentes

¿Qué normas alimentan tu herramienta? Lista tu corpus normativo (leyes, decretos, sentencias — debe ser **pequeño y público**):

* [ ] **Ley 820 de 2003:** Régimen de Arrendamiento de Vivienda Urbana, especialmente el artículo 20. https://www.secretariasenado.gov.co/senado/basedoc/ley_0820_2003.html
* [ ] **DANE — Índice de Precios al Consumidor (IPC):** fuente para determinar el porcentaje máximo de reajuste. https://www.dane.gov.co/index.php/estadisticas-por-tema/precios-y-costos/indice-de-precios-al-consumidor-ipc

### 1.5 Nombre y lema

**Nombre:** ArrendamientoClaro

**Lema:** “¿Te subieron el arriendo? Comprueba si el aumento cumple la ley.”

---

## 🗺️ Parte 2 — Plan de desarrollo

Marca cada hito cuando lo termines. Los hitos siguen las sesiones del curso.

* [ ] **M0 — Descripción y plan** *(con Sesión 1)*: Partes 1 y 2 de este README completas.
* [ ] **M1 — Asistente con instrucciones v1** *(Sesión 1–2)*: redactaste las instrucciones (prompt de sistema) de tu asistente y funcionan en una herramienta gratuita de chat.
* [ ] **M2 — Casos de prueba documentados** *(Sesión 2)*: tienes al menos 5 casos de prueba guardados en `docs/casos-de-prueba.md`.
* [ ] **M3 — Corpus conectado (RAG)** *(Sesión 3)*: tu asistente **cita la fuente** normativa que usa y no inventa. Corpus cargado en `corpus/`.
* [ ] **M4 — Interfaz web desplegada** *(Sesión 4)*: tu herramienta tiene **URL pública** y un usuario real la probó.
* [ ] **M5 — Análisis crítico y demo** *(Sesión 5)*: Parte 7 completada + presentación de 5 minutos.

### Bitácora de avance semanal

| Semana | Qué hice                                                | Enlace/captura | Dudas para la clase                         |
| ------ | ------------------------------------------------------- | -------------- | ------------------------------------------- |
| 1      | Definimos el problema, usuarios, alcance y fuentes.     |                | ¿El alcance es suficientemente concreto?    |
| 2      | Desarrollamos el primer prototipo del asistente.        |                | ¿Qué casos debemos probar?                  |
| 3      | Conectamos el corpus normativo y las fuentes del IPC.   |                | ¿Cómo evitar que la IA invente información? |
| 4      | Desarrollamos la interfaz y realizamos una prueba real. |                | ¿Qué errores presentó?                      |
| 5      | Analizamos resultados y preparamos la presentación.     |                | ¿Qué debemos mejorar?                       |

---

## 🛠️ Parte 3 — Stack técnico recomendado

Todo es **gratuito y no exige tarjeta de crédito**. Tu proyecto final debería verse así:

```text
[Usuario] → [Interfaz web] → [Orquestación (LangChain)] → [Modelo (OpenRouter)]
                                   ↕
                          [Tu corpus normativo (RAG)]
```

| Pieza                         | Herramienta recomendada          | Para qué sirve (en cristiano)                                     |
| ----------------------------- | -------------------------------- | ----------------------------------------------------------------- |
| **Interfaz web**              | **v0.dev** o **Streamlit**       | Lo que el usuario ve: campos, botones y resultados.               |
| **Orquestación**              | **LangChain / LangGraph**        | Organiza la pregunta, busca la información y genera la respuesta. |
| **Modelo (LLM)**              | **OpenRouter** — modelos `:free` | Genera las respuestas de la herramienta.                          |
| **Memoria de fuentes (RAG)**  | **LangChain + Chroma o FAISS**   | Permite consultar las normas antes de responder.                  |
| **Trazabilidad** *(opcional)* | **LangSmith**                    | Permite revisar y detectar errores del asistente.                 |

> 🔑 **Regla de oro:** tu `OPENROUTER_API_KEY` va en una **variable de entorno**, jamás pegada en el código ni en el chat. Si se filtra en GitHub, revócala inmediatamente.

La herramienta **ArrendamientoClaro** funcionará así:

1. El usuario ingresa el canon actual y el nuevo valor.
2. Indica la fecha del último reajuste.
3. La herramienta verifica los datos.
4. Consulta el corpus jurídico.
5. Compara el aumento con el límite legal.
6. Explica el resultado de forma sencilla.
7. Muestra la norma utilizada como fundamento.

El objetivo es que el usuario conozca tanto el resultado como **la razón jurídica y la fuente normativa** que lo sustentan.

## 🚀 Parte 4 — Ruta de despliegue

Tu meta: **una URL pública** que cualquiera pueda abrir. Elige una ruta:

### Opción A — Vercel ⭐ (recomendada, la del curso)
1. Sube tu código a este repo de GitHub (ya lo tienes ✅).
2. Crea cuenta gratis en [vercel.com](https://vercel.com) con tu GitHub.
3. "Add New Project" → importa tu repo → Deploy.
4. Cada `git push` re-despliega solo.
- ✅ Ideal para Next.js/Streamlit (Streamlit via [streamlit.io/community-cloud](https://streamlit.io)) · gratis · sin servidor.

### Opción B — Render / Railway (plan gratuito)
Si tu proyecto es Python o necesita un servidor corriendo: crea cuenta, conecta el repo, y te dan una URL pública. Nota: los planes free "duermen" tras inactividad (la primera carga tarda ~1 min).

### Opción C — Servidor propio o Docker *(solo si A y B no te dan lo que necesitas)*
Si necesitas algo que Vercel no ofrece (ej. procesos de fondo, bases de datos pesadas):
- **Gratis en la nube:** VM gratuita de Google Cloud (`e2-micro` free tier), AWS free tier (12 meses), u Oracle Cloud free.
- **Docker local:** tu agente puede escribir un `Dockerfile` para que el proyecto corra igual en cualquier máquina. Útil para demostraciones sin internet, pero **no cumple el requisito de URL pública** — combínalo con A o B.

### Checklist de despliegue ✅
- [ ] URL pública funciona en el navegador de otra persona (pídele a alguien que la abra)
- [ ] La advertencia de la Parte 7 es **visible** en la interfaz
- [ ] No hay API keys ni secretos en el código (verifica con una búsqueda de `sk-` en el repo)
- [ ] Anota la URL aquí: **`[tu-url-publica]`**

> El dominio propio (.com, .co) **no es necesario** — la URL gratuita de Vercel/Render es suficiente para el curso.

---

🧠 Parte 5 — Guía de prompting para vibe coding
Tu competencia más transferible a la práctica profesional: instruir bien a la IA. Reglas:
1. Un hito a la vez. No le pidas "hazme todo el proyecto". Pide: "vamos por M1".
2. Da contexto jurídico, recibe código. Pega tu Parte 1 y dile: "eres mi ingeniero, yo soy el abogado del proyecto".
3. Pide explicaciones. "Explícame como a alguien que no sabe programar qué acabas de hacer."
4. Commits frecuentes. Cada vez que algo funcione: git add . && git commit -m "M1: instrucciones del asistente" y push. Si rompes algo, siempre puedes volver atrás.
5. Nunca pegues datos personales reales de usuarios en el chat ni en el código (Ley 1581).
6. Verifica como abogado. Toda respuesta legal que dé la herramienta, contrástala con la norma. Tú respondes por lo que publicas.
Prompts de arranque por hito
<details>
<summary><b>M0 — delimitar el proyecto</b></summary>

"Soy estudiante de derecho primer semestre. Mi idea de proyecto es [idea]. Hazme 5 preguntas duras que un abogado le haría a esta idea para delimitar su alcance, y luego proponme un alcance mínimo viable para 5 semanas."

</details>

<details>
<summary><b>M1 — instrucciones del asistente</b></summary>

"Escribe el prompt de sistema de mi asistente jurídico. Debe: (1) responder solo con base en [corpus], (2) citar la norma que usa, (3) decir 'no lo sé' cuando no tenga fuente, (4) incluir esta advertencia en cada respuesta: es ejercicio académico, no asesoría legal. Proponme 3 versiones y explícame las diferencias."

</details>

<details>
<summary><b>M3 — RAG con mis normas</b></summary>

"Tengo [ley X] en archivos de texto en /corpus. Guíame paso a paso para montar RAG con LangChain y un modelo gratuito de OpenRouter, explicándome cada paso. Al final, el asistente debe citar artículo y norma en cada respuesta."

</details>

<details>
<summary><b>M4 — interfaz y despliegue</b></summary>

"Crea una interfaz web simple para mi asistente: un recuadro para escribir la consulta, el espacio de respuesta, la advertencia legal visible arriba, y el logo/nombre. Luego guíame para desplegarla gratis en Vercel con mi repo de GitHub. No sé programar: dime exactamente qué archivo tocar y qué copiar."

</details>

⚖️ Parte 6 — Ética, datos y responsabilidad
Estas salvaguardas son obligatorias y hacen parte de la evaluación:
- Advertencia visible obligatoria. Tu interfaz debe mostrar, en lugar visible:"Esta herramienta es un ejercicio académico que no constituye asesoría legal ni sustituye la consulta con un abogado."
  - [ ] Implementada y visible en la interfaz
- Protección de datos (Ley 1581 de 2012). Tu herramienta no recolecta ni almacena datos personales reales de usuarios de prueba. Los usuarios de prueba usan situaciones ficticias o datos inventados.
  - [ ] Verificado: no guardo datos personales
- Corpus público. Solo fuentes públicas: leyes, decretos, jurisprudencia publicada.
  - [ ] Verificado
- Anti-alucinaciones. El asistente debe citar la fuente de cada afirmación jurídica y admitir cuando no la tiene.
  - [ ] Casos de prueba donde la herramienta se niega a inventar
🔍 Parte 7 — Análisis crítico (insumo de tu sustentación final)
Responde con total honestidad — aquí es donde demuestras tu criterio jurídico:
1. ¿Dónde falla tu herramienta? Describe 2 situaciones donde se equivoca o se queda corta.
Respuesta: Puede fallar cuando la pregunta del usuario no está dentro del contenido del corpus o cuando la norma ha cambiado y la información no está actualizada. También puede interpretar incorrectamente los hechos de un caso y dar una respuesta incompleta.
2. ¿Qué datos procesa? Qué entra, qué se guarda, qué sale.
Respuesta: Entra la pregunta o situación jurídica planteada por el usuario. La herramienta utiliza las fuentes jurídicas públicas disponibles en su corpus y genera una respuesta basada en ellas. No se guardan datos personales reales de los usuarios de prueba.
3. ¿Por qué no reemplaza al abogado? Argumenta en 5–8 frases.
Respuesta: No reemplaza al abogado porque la IA puede equivocarse, interpretar mal los hechos o utilizar información incompleta. El abogado debe analizar las circunstancias particulares de cada caso. También debe verificar que las normas y jurisprudencia utilizadas estén vigentes y sean aplicables. La IA puede servir como herramienta de apoyo para buscar y organizar información jurídica. Sin embargo, no tiene la responsabilidad profesional del abogado. Por eso, toda respuesta generada por la herramienta debe ser revisada antes de utilizarse.

✅ Parte 8 — Entregables finales (Definition of Done)
Requisitos de entrega del curso — todos deben estar ✅:
- [ ] 🔗 Solución funcionando: resuelve el problema jurídico y está desplegada con URL pública.
- [ ] 👤 Usuario real: al menos una persona externa al curso la usó, con evidencia (video corto o testimonio). Guarda la evidencia en docs/evidencia-usuario.md.
- [ ] 📦 Repositorio con historial: este repo muestra tus avances semanales (commits + bitácora).
- [ ] 🧠 Análisis crítico: Parte 7 completada.
- [ ] 📋 Partes 1–7 de este README completas y al día.
