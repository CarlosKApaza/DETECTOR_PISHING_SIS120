# Detector de Phishing — SIS120

Extensión web que identifica **patrones textuales sospechosos** mediante expresiones regulares (Regex), resalta las coincidencias y calcula un nivel orientativo de riesgo.

**Materia:** SIS120 — Lenguajes Formales y Autómatas  
**Universidad:** Universidad Mayor, Real y Pontificia de San Francisco Xavier de Chuquisaca  
**Integrantes:** Emily Karen Villarpando Olmedo y Carlos Daniel Kevin Apaza Villaca

## 1. ¿Qué hace el programa?

Al presionar **Analizar Página**, el detector examina el texto visible del sitio web abierto y busca ocho categorías de patrones:

- Palabras de urgencia o miedo.
- Promesas de premios, ofertas o dinero fácil.
- Frases que solicitan acciones, como «haz clic» o «inicia sesión».
- Palabras camufladas con números o símbolos, como `p4ssw0rd`.
- Nombres de archivos con extensiones potencialmente peligrosas.
- Enlaces HTTP/HTTPS que contienen una dirección IP.
- Tres o más signos `!` o `¡` consecutivos.
- Bloques largos de texto en mayúsculas.

La extensión muestra un puntaje total, un detalle por categoría y palabras resaltadas sobre la página. **Una coincidencia es una señal de revisión, no una prueba de que el sitio sea fraudulento.**

## 2. Requisitos

- Google Chrome o Brave de escritorio (navegador basado en Chromium).
- Los archivos de este repositorio descargados en una misma carpeta.

No necesita instalar librerías de JavaScript ni ejecutar un servidor para usar la extensión en sitios web normales.

## 3. Instalación de la extensión

1. Descarga el repositorio (botón **Code → Download ZIP**) y descomprime el archivo.
2. Abre el administrador de extensiones:
   - **Chrome:** `chrome://extensions/`
   - **Brave:** `brave://extensions/`
3. Activa **Modo de desarrollador**.
4. Haz clic en **Cargar descomprimida**.
5. Selecciona la carpeta que contiene directamente el archivo `manifest.json`.
6. Verifica que aparezca **Detector de Phishing**. Si quieres, fija su icono a la barra de herramientas.

## 4. Cómo utilizarlo

1. Abre una página web normal que contenga texto y, si la tenías abierta antes de instalar la extensión, **recárgala**.
2. Haz clic en el icono de **Detector de Phishing**.
3. Presiona **Analizar Página**.
4. Revisa el nivel de riesgo, el puntaje y las coincidencias de cada categoría.
5. Utiliza **Quitar Resaltado** para retirar las marcas, o **Re-analizar** para repetir el análisis.

**Importante:** el resultado aparece en el panel de la extensión, **no en la consola F12**. El análisis se inicia al pulsar el botón; no se ejecuta automáticamente al entrar en una web. El detector no puede analizar algunas páginas internas del navegador (por ejemplo, `chrome://extensions/`).

## 5. Pruebas con `prueba.html`

El archivo `prueba.html` incluye tres ejemplos: mensaje con múltiples indicios de phishing, mensaje publicitario sospechoso y comunicación académica legítima.

Para probarlo desde el equipo:

1. En los detalles de la extensión, activa **Permitir acceso a las URL de archivo** (puede aparecer como *Allow access to file URLs*).
2. Abre `prueba.html` con Chrome o Brave y recarga esa pestaña.
3. Abre la extensión y pulsa **Analizar Página**.
4. Observa las palabras resaltadas y el desglose por categorías.

**Cómo interpretar esta prueba:** los tres casos están dentro de **una sola página**. Por tanto, el detector suma las coincidencias de los tres textos y entrega **un puntaje global**; no evalúa cada tarjeta por separado. Si se desea comprobar un mensaje individual, hay que mostrar únicamente ese texto en la página analizada.

## 6. Puntuación de riesgo

Cada coincidencia agrega los puntos asignados a su categoría:

| Patrón detectado | Puntos por coincidencia |
|---|---:|
| Urgencia o miedo | 15 |
| Engaño o avaricia | 10 |
| Llamada a la acción | 25 |
| Texto camuflado | 30 |
| Archivo potencialmente peligroso | 40 |
| URL que contiene una IP | 50 |
| Exclamaciones repetidas | 10 |
| Texto largo en mayúsculas | 15 |

El total se calcula como la **suma de (número de coincidencias × puntos de cada categoría)**.

| Puntaje total | Clasificación |
|---|---|
| 0 | Limpio, sin coincidencias detectadas |
| 1 a 30 | Riesgo bajo |
| 31 a 70 | Riesgo medio |
| 71 o más | Riesgo alto |

Son umbrales definidos para este proyecto académico; no representan una certificación de seguridad ni una probabilidad estadística de fraude.

## 7. Archivos del proyecto

```text
DETECTOR_PISHING_SIS120/
├── manifest.json   # Configuración y permisos de la extensión
├── content.js      # Expresiones regulares, análisis y resaltado del texto
├── popup.html      # Interfaz visual del panel
├── popup.js        # Botones, comunicación y clasificación del puntaje
├── prueba.html     # Página local con casos de prueba
└── README.md       # Instrucciones de instalación y uso
```

## 8. Relación con Lenguajes Formales

Cada expresión regular describe un conjunto de cadenas que cumplen una estructura determinada. Los patrones regulares pueden representarse mediante **autómatas finitos (AFND y AFD)**; el informe del proyecto desarrolla ejemplos de ese reconocimiento formal. El programa aplica las expresiones regulares desde JavaScript para localizar coincidencias en textos de páginas web.

## 9. Alcances y limitaciones

La herramienta identifica **formas y palabras**, pero no comprende la intención del autor ni comprueba la reputación de un enlace. Puede marcar publicidad legítima, artículos periodísticos o advertencias educativas como sospechosos. Asimismo, los patrones no detectan todas las posibles estafas.

Por esta razón, el puntaje debe interpretarse como **una alerta orientativa** y no como un veredicto definitivo sobre la seguridad de la página.

---
**Proyecto académico — SIS120 · Lenguajes Formales y Autómatas.**
