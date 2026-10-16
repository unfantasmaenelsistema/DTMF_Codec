# DTMF Codec

**Codificador y decodificador de tonos DTMF**, de [Un Fantasma en el Sistema](https://www.unfantasmaenelsistema.com).

▶ **Abrir:** https://unfantasmaenelsistema.github.io/DTMF_Codec/

Los tonos DTMF son los pitidos de marcación de los teléfonos: cada tecla suena como la suma de dos frecuencias (ITU-T Q.23). Esta herramienta los genera y los descifra, algo muy útil en los retos CTF de audio, donde a menudo te dan una grabación de tonos y tienes que sacar el número, el PIN o el texto escondido.

## Qué hace

- **Codificador:** teclado de 16 teclas (0-9, A-D, \*, #) que suena al pulsarlo con el ratón, con el dedo o con el teclado del ordenador. Guarda la secuencia y la descarga en WAV.
- **Decodificar un archivo:** arrastra un WAV, MP3, OGG o FLAC y obtén la secuencia de teclas con el instante y la duración de cada tono.
- **Decodificador por micrófono:** detecta en tiempo real los tonos que suenan cerca del micrófono.
- **Secuencia:** escribe un número (por ejemplo `*123#`), ajusta duración y pausa, escúchalo o descárgalo en WAV.
- **Referencia:** tabla de frecuencias, especificaciones y consejos para retos CTF.

## Cómo detecta los tonos

El audio se analiza en ventanas de 25 ms con el algoritmo de Goertzel, que mide la energía de las ocho frecuencias DTMF. Cada tono se mide en su frecuencia nominal y a ±1,5 %, la tolerancia que exige ITU-T Q.24. Una tecla se acepta solo si:

- su par de frecuencias está 6 dB por encima de las demás de su grupo,
- supera el umbral de nivel (ajustable, −45 dBFS por defecto),
- la diferencia de nivel entre los dos tonos (twist) es menor de unos 9 dB,
- y ambos tonos concentran la mayor parte de la energía de la ventana.

Así se descartan la voz y el ruido. El detector se ha probado con tonos de 40 ms, audio de 8 kHz, dígitos repetidos, ruido blanco, nivel bajo, voz superpuesta, MP3 y tonos desafinados un 1,5 %. Los desafinados un 4 % se rechazan. Para el micrófono, la app pide al navegador que desactive la supresión de ruido y el control automático de ganancia, porque pueden borrar los tonos.

## Privacidad

Todo ocurre en tu navegador: el audio del micrófono y los archivos no salen de tu equipo.

## Estructura

```
index.html   la aplicación (HTML, CSS y JS en un solo archivo)
icono.png    logo de la casa
```

Para probar en local: `python -m http.server` y abre `http://localhost:8000` (el micrófono necesita `localhost` o HTTPS).

## English

**DTMF Codec** generates and decodes telephone dialling tones (ITU-T Q.23) in the browser: a playable 16-key keypad, a sequence generator with WAV export, a real-time microphone decoder and a file decoder (WAV, MP3, OGG, FLAC) that lists each key with its timing. Detection uses the Goertzel algorithm with ±1.5% frequency tolerance, twist and energy checks so speech and noise are ignored. Handy for CTF audio challenges. Everything runs locally. Bilingual (ES/EN), light/dark themes.

## Licencia / License

[MIT](LICENSE) © Un Fantasma en el Sistema
