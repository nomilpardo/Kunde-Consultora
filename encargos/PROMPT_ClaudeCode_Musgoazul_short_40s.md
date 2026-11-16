# Encargo para Claude Code: Short vertical "Los amigos de Musgoazul y la Semilla de Aurora" (40 s máximo)

Eres Claude Code y trabajas en el PC con Windows de Sebastián. Tu tarea es producir **de principio a fin** un **short vertical 9:16 (1080x1920)** de **40 segundos como máximo** (objetivo: 36–39 s), en **español**, para YouTube Shorts y TikTok. El short es un avance del cuento de 10 minutos y termina invitando a ver la historia completa en YouTube. Es una **prueba**: sirve para validar el estilo, las voces y el ritmo antes de producir más.

Usa el **ComfyUI local** para imágenes y animación. El guion está en la sección 8 y ya fue aprobado por Sebastián: no cambies las frases. Sí puedes mejorar los prompts visuales.

Trabaja de forma autónoma. Detente a pedir ayuda solo en los casos de la sección 2.

---

## 1. Entorno (verificado en el encargo del video de 10 minutos)

- **Sistema:** Windows x64 con GPU **NVIDIA**.
- **ComfyUI portable v0.45.0:**
  `C:\Users\USER\Desktop\Animaciones IA\ComfyUI_windows_portable_nvidia\ComfyUI_windows_portable\`
  - Para iniciarlo: `run_nvidia_gpu.bat`. También sirve `python_embeded\python.exe -s ComfyUI\main.py --windows-standalone-build`.
  - API en `http://127.0.0.1:8188`.
- **Modelos instalados** (en `ComfyUI\models\`). No descargues otros a menos que falte algo imprescindible:
  - `checkpoints/flux1-schnell-fp8.safetensors` → imágenes clave (incluye CLIP y VAE).
  - `diffusion_models/ltx-2.5-22b-distilled-transformer-w4a8_convrot.safetensors` → imagen a video.
  - `text_encoders/gemma4-12b-with-proj-ltx-2.5-w4a8_convrot.safetensors`
  - `vae/ltx-2.5-video-vae-bf16.safetensors` y `vae/ltx-2.5-audio-vae-bf16.safetensors` (LTX 2.5 genera video con audio).
- **Nodos personalizados:** ninguno relevante; solo nodos nativos.
- **Carpeta de salida de este short:** `C:\Users\USER\Desktop\Animaciones IA\Musgoazul\short_01\`
  - **No toques** nada fuera de `short_01\`: en `Musgoazul\` puede haber material del video de 10 minutos (`pipeline\`, `narracion\`, `keyframes\`, `clips\`, `final\`, `_v1_obsoleta\`).
  - Si en `Musgoazul\pipeline\` ya existen `flux_keyframe_api.json` y `ltx_i2v_api.json` que funcionan, **cópialos** a `short_01\pipeline\` y adáptalos a vertical en lugar de rehacerlos.

## 2. Reglas de trabajo con Sebastián

1. **Aviso con sonido.** Cada vez que necesites una acción de Sebastián, primero reproduce un sonido de notificación y después escribe la petición:
   `powershell -c "(New-Object Media.SoundPlayer 'C:\Windows\Media\Windows Notify System Generic.wav').PlaySync()"`
   (alternativa: `powershell -c "[console]::beep(880,500)"`).
2. **Idioma:** todo el contenido del video va en **español**. Los prompts de imagen y video van en inglés.
3. **Pide ayuda solo si:** ComfyUI no arranca después de 2 intentos, falta VRAM incluso con las opciones de bajo consumo, o hay una decisión creativa que cambia el resultado. Todo lo demás lo decides tú y lo anotas en `short_01\LOG.md`.
4. **No uses** música con derechos de autor, personajes de marcas ni estilos atribuidos por nombre a estudios reales.

## 3. Qué cambia respecto al video de 10 minutos

Estas decisiones son de Sebastián (16-nov-2026) y mandan sobre el encargo anterior:

| Tema | Video de 10 min | Este short |
|---|---|---|
| Formato | 16:9, 1920x1080 | **9:16, 1080x1920** |
| Estilo | 3D, colores saturados | **2D de libro infantil, pastel Montessori** (sección 4) |
| Voces | Solo narradora | **Una voz por personaje; narrador solo en lo crucial** (sección 6) |
| Onomatopeyas | "¡hip!", "tum-tum" en el texto | **Ninguna dicha en voz.** El hipo de Don Hipo y el latido de la semilla son solo efectos de sonido |
| Ritmo | Un plano por párrafo narrado | **Diálogo rápido**: réplicas de unos 2–5 s, cambio de plano cada 3–6 s |

## 4. Estilo visual (agrégalo a TODOS los prompts de imagen)

`2D children's picture book illustration, soft colored pencil and watercolor texture, visible paper grain, muted pastel Montessori palette of sage green, dusty pink, soft ochre, powder blue and cream, simple rounded shapes, thin sketchy pencil outlines, gentle flat lighting, cozy calm storybook mood, vertical composition, no text, no watermark, no humans, not 3D, not photorealistic`

Referencia de Sebastián para este estilo: animales dibujados a lápiz y acuarela pastel (panda rojo, ardilla con bufanda, erizo con gafas, nutria y caracol) alrededor de un nido con una esfera luminosa entre cristales, bajo una aurora. Si tienes clonado el repositorio `nomilpardo/Kunde-Consultora`, la imagen está en `referencias/estilo-cuento-infantil.webp`: mírala y compara tus resultados con ella.

**Composición vertical:** sujeto principal en el tercio central. Deja libre el **20 % inferior** (ahí van los subtítulos y la interfaz de la app) y evita poner caras en el **12 % superior** y en la franja derecha (botones de la app).

## 5. Personajes y lugares (copia EXACTAMENTE el mismo texto cada vez)

| Token | Descripción para el prompt |
|---|---|
| `{BAMBU}` | a small red panda with a huge fluffy ringed tail, carrying a little birch-bark notebook and a charcoal pencil |
| `{PIPPA}` | a big-eyed flying squirrel with hazel-brown fur and gliding membranes, wearing a long knitted bright red scarf |
| `{HIPO}` | a chubby friendly hedgehog with round glasses tied with a fine silver thread, wearing a small brown leather backpack |
| `{LULA}` | a sleek river otter with velvety brown fur and a warm smile, holding a hollow reed flute |
| `{TITO}` | a tiny snail with a spiral shell painted with yellow and blue polka dots |
| `{SEMILLA}` | an apple-sized perfectly transparent crystal sphere with a tiny pulsing blue spark of light inside |

- Con 3 o más personajes, pon primero la composición ("five small animal friends...") y después las descripciones. Si FLUX mezcla rasgos, separa con "at the top / in the middle / at the bottom" o "on the left / on the right".
- **Gran Roble Anciano:** an enormous ancient oak with giant twisting roots, golden autumn leaves.
- **Montaña de Cristal:** a tall glittering crystal mountain in the distance, with a dark forest, a river and an icy cliff along the path.

## 6. Voces (definen los tiempos de todo)

Instala `edge-tts` (`pip install edge-tts`). Antes de generar, ejecuta `edge-tts --list-voices` y confirma que existen las voces de la tabla; si falta alguna, sustitúyela por otra en español del mismo género y anótalo en el log.

| Quién | Voz | Ajustes | Carácter |
|---|---|---|---|
| Narrador | `es-MX-DaliaNeural` | `--rate=-4%` | Cuentacuentos cálida, acento neutro |
| Pippa | `es-CO-SalomeNeural` | `--rate=+14% --pitch=+22Hz` | Pura energía, impulsiva |
| Don Hipo | `es-MX-JorgeNeural` | `--rate=-4% --pitch=-8Hz` | Prudente, bonachón |
| Lula | `es-US-PalomaNeural` | `--rate=-6% --pitch=+4Hz` | Dulce, serena |
| Tito | `es-CO-GonzaloNeural` | `--rate=-8% --pitch=+28Hz` | Pequeño, pausado |
| Bambú | `es-US-AlonsoNeural` | `--rate=+4% --pitch=+18Hz` | Soñador, entusiasta |

- Genera un archivo por línea: `voces\LNN_quien.mp3`. Mide cada duración con ffprobe y guárdala en `manifest.json`.
- Recorta el silencio inicial y final de cada archivo (ffmpeg `silenceremove`), dejando unos 0,1 s.
- **Sin onomatopeyas:** el texto que se envía al TTS es exactamente el de la sección 8. No añadas "hip", "tum-tum" ni interjecciones.
- **Límite conocido:** estas voces tienen poca variación emocional. Usa los signos de exclamación e interrogación del guion tal cual y no intentes compensarlo con efectos. Anota en el log si alguna voz suena plana o robótica, para que Sebastián decida si las reemplaza por voces de mayor calidad.

### Ajuste a 40 segundos

Duración total = Σ(duración de cada plano) + tarjeta final. Cada plano dura lo que suman sus líneas, más 0,25 s de aire antes y después, más 0,2 s entre líneas del mismo plano.

- Si el total pasa de **39,5 s**: sube el `--rate` de todas las voces en pasos de +3 % (máximo +12 % sobre la tabla) y regenera. Si aún no cabe, reduce el aire a 0,15 s.
- Si aún no cabe, **avisa a Sebastián con sonido** antes de recortar texto.
- **Nunca** entregues un archivo de más de 40,0 s.

## 7. Pipeline

Escribe el pipeline en **Python** dentro de `short_01\pipeline\`, con `requests` para la API de ComfyUI y **ffmpeg** para el montaje (si no está en el PATH: `winget install Gyan.FFmpeg`). Debe poder **reanudarse**: guarda el estado de cada plano en `manifest.json` y no regeneres lo que ya existe y es válido.

```
Musgoazul\short_01\
  pipeline\            (scripts .py + workflows API .json)
  voces\LNN_quien.mp3
  keyframes\pNN_k.png
  clips\pNN.mp4
  audio\musica.wav, mezcla.wav
  final\Musgoazul_short_9x16.mp4
  final\Musgoazul_short_9x16_subs.mp4
  final\Musgoazul_short_9x16.srt
  final\hoja_contacto.jpg
  manifest.json
  LOG.md
```

### Paso 0. Diagnóstico
1. Arranca ComfyUI y espera a que `GET /system_stats` responda. Anota GPU, VRAM y versión.
2. `GET /object_info`: anota qué nodos LTX existen.
3. Si la VRAM es menor de 16 GB, reinicia con `--lowvram` (o `--reserve-vram 1.5`) y usa la resolución de video reducida.

### Paso 1. Voces
Sección 6. Al terminar ya conoces la duración exacta de cada plano.

### Paso 2. Prueba de estilo (único punto de aprobación obligatorio)
- Con FLUX, genera una **hoja de personajes** vertical (`keyframes\_personajes.png`) con los 5 personajes en el estilo de la sección 4. Genera 4 semillas, míralas y elige una.
- Genera la imagen clave del **plano 3** (Don Hipo con la lupa) y anímala con LTX como prueba.
- Descarta lo que tenga deformidades, personajes extra, texto, aspecto 3D o fotográfico, colores saturados o el animal equivocado.
- **Envía a Sebastián la hoja y el clip de prueba, con aviso sonoro, y espera su visto bueno** antes de generar el resto.

### Paso 3. Imágenes clave con FLUX schnell
- Resolución **768x1344** (9:16, múltiplos de 64).
- Por plano, genera **3 candidatos** con semillas `1000*NN + k`, míralos y elige el mejor. Revisa: personajes correctos, bufanda de Pippa roja, gafas redondas de Don Hipo, lunares amarillos y azules en el caparazón de Tito, sin texto, estilo 2D pastel coherente entre planos.
- Si ninguno sirve, ajusta el prompt y repite, como máximo 2 rondas.

Plantilla del workflow en formato API (nodos nativos):
```json
{
 "1": {"class_type": "CheckpointLoaderSimple", "inputs": {"ckpt_name": "flux1-schnell-fp8.safetensors"}},
 "2": {"class_type": "CLIPTextEncode", "inputs": {"clip": ["1", 1], "text": "<PROMPT>"}},
 "3": {"class_type": "CLIPTextEncode", "inputs": {"clip": ["1", 1], "text": ""}},
 "4": {"class_type": "EmptySD3LatentImage", "inputs": {"width": 768, "height": 1344, "batch_size": 1}},
 "5": {"class_type": "KSampler", "inputs": {"model": ["1", 0], "positive": ["2", 0], "negative": ["3", 0], "latent_image": ["4", 0], "seed": 0, "steps": 4, "cfg": 1.0, "sampler_name": "euler", "scheduler": "simple", "denoise": 1.0}},
 "6": {"class_type": "VAEDecode", "inputs": {"samples": ["5", 0], "vae": ["1", 2]}},
 "7": {"class_type": "SaveImage", "inputs": {"images": ["6", 0], "filename_prefix": "musgoazul_short/pNN"}}
}
```
Envía con `POST /prompt`, consulta `GET /history/{id}` y descarga con `GET /view?filename=...&subfolder=...&type=output`.

### Paso 4. Animación con LTX 2.5 (imagen a video)
- **No adivines los nombres de los nodos.** Parte de la plantilla oficial de imagen a video de LTX 2/2.5 (`GET /api/workflow_templates`, o los `.json` con "ltx" en `python_embeded\Lib\site-packages\comfyui_workflow_templates*\`), conviértela a formato API y guárdala como `pipeline\ltx_i2v_api.json`.
- Al ser un modelo destilado, usa los pasos y el CFG de la plantilla (normalmente unos 8 pasos y CFG 1).
- Resolución **704x1280** (múltiplos de 32). Si falta VRAM: **544x960**.
- FPS **24**. La cantidad de frames debe cumplir el formato que exija LTX (normalmente 8·n+1). Genera cada clip con **0,5 s de más** respecto a la duración del plano, para poder recortar.
- Prompt de cada plano = `mov` + `sfx` + este sufijo fijo:
  `"2D picture book animation, simple limited animation of heads, arms, eyes and mouths, gentle and smooth, consistent characters, stable faces, no morphing, no camera shake, no text. Audio: ambient sound effects only, no speech, no dialogue, no singing."`
- **Quien habla mueve la boca y gesticula; quien escucha reacciona** (mira, ladea la cabeza, abre los ojos). No se busca sincronía labial exacta.
- **Control de calidad:** extrae 4 frames de cada clip y míralos. Regenera, como máximo 2 veces con otra semilla, si hay deformaciones graves, personajes que se derriten o se duplican, o el estilo deriva hacia 3D.
- **Plan B:** si LTX falla siempre con un plano, anímalo con un movimiento de cámara suave (ffmpeg `zoompan`) sobre la imagen clave y anótalo en el log.

### Paso 5. Música y mezcla
- **No descargues música.** Genera con Python (`numpy`, `scipy`) un fondo original y suave: acordes cálidos tipo pad o celesta en Do mayor, unos 76 BPM, con un giro a menor entre los planos 4 y 5 (cuando la semilla se apaga) y vuelta a mayor en el plano 7. Exporta `audio\musica.wav` con fundidos.
- Mezcla con ffmpeg, del volumen más alto al más bajo:
  1. Voces, cada una colocada en su instante exacto. Mezcla final normalizada a **-14 LUFS**, pico máximo -1,5 dBTP.
  2. Audio ambiente de LTX, unos **-20 dB** por debajo de la voz. Si un clip trae algo parecido a habla o canto, silencia su audio.
  3. Música, unos **-24 dB**, con *ducking* (`sidechaincompress`) bajo las voces.
- Entre planos usa **corte directo**. Solo un fundido de entrada de 0,3 s al inicio y fundido cruzado de 0,4 s hacia la tarjeta final.

### Paso 6. Subtítulos, tarjeta final y exportación
- **Subtítulos:** `.srt` con los tiempos reales de cada línea. Máximo 26 caracteres por línea y 2 líneas por subtítulo. En la versión quemada: fuente redondeada de Windows (Segoe UI Bold o similar), blanco con borde oscuro, centrados, con la base a un **24 % del alto** desde abajo. No pongas el nombre de quien habla.
- **Tarjeta final (plano 8):** último frame del plano 7 con desenfoque suave y oscurecido un 25 %, y el texto en dos líneas: "Mira la historia completa" / "en nuestro canal de YouTube". Fuente redondeada, color crema, centrado en el tercio medio, con fundido de entrada. Esta tarjeta sí lleva texto en ambas versiones.
- **Exportación:** escala a 1080x1920 con lanczos. H.264 (`-preset slow -crf 18`), 24 fps, `yuv420p`. Audio AAC 192 kbps 48 kHz. `-movflags +faststart`.
- Entrega dos versiones: limpia (`Musgoazul_short_9x16.mp4`) y con subtítulos quemados (`Musgoazul_short_9x16_subs.mp4`).

### Paso 7. Verificación final (obligatoria)
- Duración total **≤ 40,0 s** y resolución 1080x1920 (ffprobe).
- Los 8 planos están en orden: hoja de contacto con un frame por plano (`final\hoja_contacto.jpg`). Mírala.
- Cada voz suena dentro de su plano y ninguna se pisa con otra.
- Volumen integrado cerca de -14 LUFS, sin saturación (`ebur128`).
- No hay frames negros inesperados.
- Al terminar: sonido de notificación y un resumen corto con la ruta de los MP4, la duración, los planos que usaron el Plan B, las voces sustituidas y el tiempo total de render.

---

## 8. Guion aprobado (8 planos)

Las duraciones son orientativas: las reales salen de las voces (sección 6).

```yaml
- plano: 1            # ~4 s
  lineas:
    - {quien: Narrador, texto: "Una mañana de otoño, algo cayó del cielo en Musgoazul."}
  img: "five small animal friends having a picnic of wild berries and nuts under the enormous ancient oak with giant twisting roots and golden autumn leaves, a glowing crystal orb falling from the sky above them leaving a trail of golden sparkles, all looking up surprised: {BAMBU}, {PIPPA}, {HIPO}, {LULA}, {TITO}"
  mov: "a gust swirls the leaves, the glowing orb falls and lands softly in front of the red panda with a puff of golden dust, the friends lean back startled"
  sfx: "whistling gust, soft magical chime, gentle thud"

- plano: 2            # ~4 s
  lineas:
    - {quien: Pippa, texto: "¡Por todas las bellotas del bosque! ¿Una estrella caída?"}
  img: "{PIPPA} jumping backwards in the air with an astonished face, red scarf swirling, golden dust floating, autumn oak roots behind"
  mov: "the flying squirrel leaps backwards, lands, then leans forward talking excitedly with wide eyes and waving paws"
  sfx: "whoosh, leaves rustling"

- plano: 3            # ~6 s
  lineas:
    - {quien: Don Hipo, texto: "No es una estrella. Es una Semilla de Aurora: enciende las luces del cielo en invierno."}
  img: "{HIPO} examining {SEMILLA} through a big magnifying glass, his eye hugely magnified, soft blue light on his face, autumn leaves on the ground"
  mov: "the hedgehog leans in with the magnifier, adjusts his round glasses, then looks up and explains calmly, moving his mouth and raising one paw, the blue spark pulses"
  sfx: "soft magical hum, gentle heartbeat pulse"

- plano: 4            # ~6 s
  lineas:
    - {quien: Lula, texto: "Su latido se apaga. Si no vuelve a su nido antes de la noche, el cielo quedará oscuro."}
  img: "{LULA} with her ear close to {SEMILLA}, worried gentle expression, the blue spark dim, {BAMBU} and {PIPPA} behind her looking concerned"
  mov: "the otter listens to the sphere, then turns to her friends and speaks softly, the blue glow pulses slower and dimmer, the friends behind exchange worried looks"
  sfx: "slowing heartbeat pulse, quiet wind"

- plano: 5            # ~5 s
  lineas:
    - {quien: Tito, texto: "El camino tiene tres pruebas que nadie ha cruzado en años."}
  img: "{TITO} on top of a mushroom at the bottom of the frame, looking up at a steep winding path that climbs to a tall glittering crystal mountain at the top of the frame, a dark forest, a river and an icy cliff along the way"
  mov: "the snail stretches its antennae and talks slowly, pointing one antenna at the path, mist drifts across the mountain"
  sfx: "distant wind, low soft drum"

- plano: 6            # ~6 s
  lineas:
    - {quien: Pippa, texto: "¡No hay tiempo que perder!"}
    - {quien: Don Hipo, texto: "¡Espera, Pippa! Necesitamos un plan."}
    - {quien: Bambú, texto: "¡Entonces vamos juntos!"}
  img: "{PIPPA} dashing off toward the trees with her red scarf flying, {HIPO} raising a paw to stop her, {BAMBU} beside him smiling with his notebook raised"
  mov: "the flying squirrel darts forward, the hedgehog reaches out and calls her, she stops and looks back, the red panda steps in smiling and raises his notebook"
  sfx: "fast whoosh, rustling leaves"

- plano: 7            # ~4 s
  lineas:
    - {quien: Narrador, texto: "¿Lograrán devolverla a tiempo?"}
  img: "the five small animal friends seen from behind, standing together at the start of a winding path, facing the tall glittering crystal mountain under a soft violet sunset sky, a faint blue glow coming from the hedgehog's backpack: {BAMBU}, {PIPPA}, {HIPO}, {LULA}, {TITO} on the red panda's shoulder"
  mov: "the friends take their first steps together up the path, the blue glow in the backpack flickers, camera slowly rises toward the mountain"
  sfx: "evening wind, hopeful soft swell"

- plano: 8            # ~4 s, tarjeta final (sin clip nuevo: usa el último frame del plano 7)
  lineas:
    - {quien: Narrador, texto: "Mira la historia completa en nuestro canal de YouTube."}
  texto_en_pantalla: ["Mira la historia completa", "en nuestro canal de YouTube"]
```

Notas del guion:
- La línea de Bambú del plano 6 ("¡Entonces vamos juntos!") no está en el cuento original; se añadió para que hablen los cinco personajes.
- En el plano 6 las tres líneas van seguidas, con 0,2 s entre ellas, como una conversación rápida.

## 9. Entregables

En `C:\Users\USER\Desktop\Animaciones IA\Musgoazul\short_01\final\`:
1. `Musgoazul_short_9x16.mp4`: versión limpia (solo la tarjeta final lleva texto).
2. `Musgoazul_short_9x16_subs.mp4`: con subtítulos quemados.
3. `Musgoazul_short_9x16.srt`
4. `hoja_contacto.jpg`
5. `LOG.md`: GPU/VRAM, parámetros, voces usadas y sustituidas, duración de cada línea, planos regenerados o con Plan B, y tiempos de render.

Deja en `short_01\pipeline\` los workflows en formato API y los scripts, para repetir el proceso con otros shorts.
