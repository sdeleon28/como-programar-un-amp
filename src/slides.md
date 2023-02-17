<div style="height: 100vh; width: 100vh; display: flex; justify-content: center; align-items: center; align-self: center; flex-direction: column;">
  <h1>Cómo programar un amplificador de guitarra?</h1>
  <h2>Santiago de León</h2>
  <img src="https://thmstudio.com/static/ffd528988261cbf00274cbaf1f56e4b5/9d183/me-rockin-out.jpg" style="border-radius: 9999px;" />
</div>

---

# Sobre mí

* Experiencia:
  * <span style="color: green;">Aplicaciones / APIs: Java, Python/Django, PHP</span>
  * <span style="color: green;">Frontend: React</span>
  * <span style="color: green;">Aplicaciones móviles: React Native</span>
  * <span style="color: green;">Tareas de DevOps</span>
  * <span style="color: green;">Guitarra y producción musical</span>
  * <span style="text-decoration: line-through; text-decoration-thickness: 4px; color: red;">C++ / JUCE</span>
  * <stroke style="text-decoration: line-through; text-decoration-thickness: 4px; color: red;">Desarrollo de audio</stroke>
  * <stroke style="text-decoration: line-through; text-decoration-thickness: 4px; color: red;">Electrónica</stroke>
* Github:
  * https://github.com/sdeleon28/

---

# Objetivo

* Funcionalidades:
  * High gain amp
  * Simulación de cabinet
  * Distorsión "creíble"
  * Controles: ganancia, tono y level
  * Hacer un ampli que yo usaría para hacer mis canciones

---

# Objetivo

<img
  src="https://thmstudio.com/static/ignition-b3b86f0fbf2e223a928604a0ffe0a58a.png"
  style="width: 522px; height: 300px;"
/>

---

# Formas de conseguir nuestro objetivo

* Opción 1: Modelado de sistemas analógicos

---

# Modelado de sistemas analógicos

😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰

<img src="https://www.researchgate.net/profile/Daning-Zhang/publication/283661284/figure/fig1/AS:409362775461889@1474611099433/Schematic-diagram-of-an-amplifier-circuit-unit.png" style="max-width: 500px; height: auto;" />

😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰

---

# Formas de conseguir nuestro objetivo

* <stroke style="text-decoration: line-through; text-decoration-thickness: 4px; color: red;">Opción 1: Modelado de sistemas analógicos</stroke>
  * 😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰😰
* <stroke style="color: green;">Opción 2: Técnicas 100% digitales
</stroke>

---

# Clipeo

---

# Clipeo

<div style="display: flex; width: 90%; height: auto; flex-direction: row; justify-content: space-between;">
  <div style="flex: 1;">
    <img src="../assets/funcion-seno.png" />
  </div>
  <div style="flex: 1;">
    <img src="../assets/funcion-clipeo.png" />
  </div>
</div>

---

# Clipeo

<div style="display: flex; width: 90%; height: auto; flex-direction: row; justify-content: space-between;">
  <div style="flex: 1;">
    <img src="../assets/funcion-seno.png" />
  </div>
  <div style="flex: 1;">
    <img src="../assets/funcion-clipeo.png" />
  </div>
  <div style="flex: 1;">
    <img src="../assets/funcion-seno-clipeada.png" />
  </div>
</div>

---

# Clipeo

<div style="display: flex; width: 90%; height: auto; flex-direction: row; justify-content: space-between;">
  <div style="flex: 1;">
    <img src="../assets/funcion-seno-y-funcion-seno-clipeada.png" />
  </div>
</div>

---

# Waveshaper estático

---

# Waveshaper estático

Una función matemática por la que pasa cada uno de tus samples

---

# Waveshaper estático

<img src="https://thmstudio.com/static/76a29caa557c3fd166043f618c525e0f/e9c9b/waveshapers.png" style="max-width: 500px; height: auto;" />

---

# Convolución

* Es la técnica más simple para simular un cab microfoneado
* Se graba una respuesta de impulso (IR) poniendo un micrófono frente al cab de tu amp
* O se puede descargar uno de internet hecho por otra persona
* JUCE trae una clase `Convolution` en su módulo `juce_dsp`

---

# Pre/post énfasis

* Pre-énfasis
  * Filtros posicionados antes del waveshaper para afectar el material a distorsionar
* Post-énfasis
  * Filtros posicionados después del waveshaper para moldear el tono de la señal distorsionada

---

# Pre/post énfasis - Frequalizer

<img src="https://foleysfinest.com/img/plugins/FrequalizerFree.png" style="max-width: 700px; height: auto;" />

https://foleysfinest.com/plugins/frequalizer/

---

# Waveshaper paramétrico

---

# Waveshaper paramétrico

```
f(x, parameter) = (x * (abs(x) + parameter) / (x * x + (parameter - 1) * abs(x) + 1)) * 0.7
```

---

# Waveshaper paramétrico

Pidamos ayuda a ChatGPT para graficar esto:

<img src="../assets/chatgpt-prompt-1.png" style="max-width: 800px; height: auto;" />

---

# Waveshaper paramétrico

Su respuesta:

<img src="../assets/chatgpt-response-1.png" style="max-width: 500px; height: auto;" />

---

# Waveshaper paramétrico

Instalar librerías nunca fue tan fácil:

<img src="../assets/chatgpt-prompt-response-2.png" style="max-width: 800px; height: auto;" />

---

# Waveshaper paramétrico

<video controls width="600" height="auto" name="Parametric waveshaper graph">
  <source src="../assets/colab-video.mov"></source>
</video>

---

# Waveshaper dinámico

---

# Waveshaper dinámico

* Waveshaper dinámico:
  * Envelope follower
  * Waveshaper paramétrico
* <img
  src="https://thmstudio.com/static/488ed9a778779c1c47bbc7887ac1a23c/d72d4/env-follower.png"
  style="width: 522px; height: 300px;"
/>

---

# Waveshaper dinámico

<img src="../assets/dynamic-waveshaper.png" style="max-width: 1154px; height: auto;" />

---

# Problema: Aliasing

<img src="https://varietyofsound.files.wordpress.com/2011/02/tanh_plot_harmonics.png" style="max-width: 500px; height: auto;" />

---

# Solución: Oversampling

```cpp
auto ovBlock = oversampler.processSamplesUp (mainContext.getInputBlock());
dsp::ProcessContextReplacing<float> waveshaperContext(ovBlock);
waveshaper.process(waveshaperContext);
oversampler.processSamplesDown (mainContext.getOutputBlock());
```

---

# Control de tono

<img
  src="https://thmstudio.com/static/ignition-b3b86f0fbf2e223a928604a0ffe0a58a.png"
  style="width: 522px; height: 300px;"
/>

* Diferentes diseños posibles:
  * Conectar perilla de TONE a la ganancia del filtro
  * Hacer un low shelf y un high shelf y hacerlos moverse como los platos de una balanza ⚖️

---

# Vista aérea

<img src="../assets/amp-diagram.png" style="max-width: 1504px; height: auto;" />

---

# Ignition

<img
  src="https://thmstudio.com/static/ignition-b3b86f0fbf2e223a928604a0ffe0a58a.png"
  style="width: 522px; height: 300px;"
/>

Code available at https://github.com/sdeleon28/IgnitionGuitarAmp

Demo:

<audio controls>
  <source src="https://thmstudio.com/ignition-demo.mp3" type="audio/mpeg"></source>
</audio>

---

# Links

* The Audio Programmer -> https://www.youtube.com/@TheAudioProgrammer
* Tutoriales oficiales de JUCE -> https://juce.com/learn/tutorials/
* JUCE Class Index -> https://docs.juce.com/master/index.html
* Ivan Cohen - Fifty shades of distortion (ADC'17) -> https://youtu.be/oIChUOV_0w4
* Blue Mangoo Software - Comparing waveshaping functions for guitar amp modeling -> https://youtu.be/2fb47zQdLy0
* Frequalizer -> https://foleysfinest.com/plugins/frequalizer/
* RS-MET -> https://github.com/RobinSchmidt/RS-MET

---

# Más links

* Post en mi blog -> https://thmstudio.com/blog/how-i-made-a-guitar-amp-plugin/
* Estas slides -> https://github.com/sdeleon28/como-programar-un-amp
* Repo de Ignition -> https://github.com/sdeleon28/IgnitionGuitarAmp

---

<div style="height: 100vh; width: 100vh; display: flex; justify-content: center; align-items: center; align-self: center; flex-direction: column;">
  <h1>Preguntas?</h1>
</div>

<script type="text/javascript" src="https://livejs.com/live.js"></script>
