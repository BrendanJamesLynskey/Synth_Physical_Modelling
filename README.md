# Physical Modelling Synthesiser

A browser-based **physical modelling synthesiser** that simulates vibrating strings, tubes, membranes, bars, and resonant bodies using real-time audio synthesis. Built entirely with the Web Audio API — no dependencies, no frameworks.

**[Launch the synth](https://brendanjameslynskey.github.io/Synth_Physical_Modelling/)**

---

## Features

- **5 Physical Models** — String (Karplus-Strong), Tube (waveguide), Membrane (circular modes), Bar (beam partials), and Modal (resonant body) synthesis
- **6 Excitation Types** — Pluck, Strike, Bow, Blow, Noise, and Impulse
- **30+ Presets** — From acoustic guitar and violin to tabla, gamelan, and singing bowls
- **Real-time Waveform Visualisation** — Watch the vibration modes animate as you play
- **Effects** — Reverb, chorus, and delay
- **Body Resonance** — Simulate sympathetic strings, body size, and tonal shaping
- **Desktop & Mobile** — Full keyboard interface on desktop, touch pad interface on mobile
- **QWERTY Keyboard Support** — Play notes using your computer keyboard
- **Zero Dependencies** — Pure HTML, CSS, and JavaScript

---

## A History of Physical Modelling Synthesis

### The Idea: Sound From First Principles

Physical modelling synthesis generates sound by simulating the **physics of how real instruments vibrate**. Rather than playing back recordings (sampling) or stacking sine waves (additive synthesis), physical modelling solves the mathematical equations that describe vibrating strings, columns of air, struck membranes, and resonating bodies. The result is sound that behaves like a real instrument — responding naturally to changes in how it is excited, dampened, and shaped.

The dream of synthesising sound from physical principles is almost as old as the science of acoustics itself. In the 19th century, **Hermann von Helmholtz** published *On the Sensations of Tone* (1863), laying the groundwork by describing how the physics of vibrating bodies produces the harmonic series we hear as musical timbre. Lord Rayleigh's *The Theory of Sound* (1877) formalised the mathematics of vibrating strings, membranes, and air columns — the very equations that physical modelling synthesis would later solve in real time.

### Early Computational Approaches (1960s–1970s)

The earliest computer music experiments at Bell Labs in the late 1950s and 1960s, led by **Max Mathews**, used direct digital synthesis but did not yet model physical systems. However, the MUSIC series of programs (MUSIC I through MUSIC V) established the paradigm of unit generators — modular building blocks for synthesis — that would later prove essential.

In 1971, **Lejaren Hiller** and **Pierre Ruiz** at the University of Illinois published a landmark paper, *Synthesizing Musical Sounds by Solving the Wave Equation*, in the *Journal of the Audio Engineering Society*. This was arguably the first true physical modelling synthesis: they numerically solved the wave equation for a vibrating string on a computer, producing sounds by simulating the physics directly. The computation was enormously expensive for the era, taking far longer than real time, but the principle was proven.

### The Karplus-Strong Algorithm (1983)

The breakthrough that made physical modelling practical came from an unexpected direction. In 1983, **Kevin Karplus** and **Alex Strong** at Stanford University published a deceptively simple algorithm: fill a delay line with random noise, then repeatedly cycle through it while applying a simple averaging filter. The result was a strikingly realistic plucked string sound.

The Karplus-Strong algorithm works because it is, in fact, a simplified physical model. The delay line represents the length of the string (determining pitch), the initial noise represents the broadband excitation of a pluck, and the averaging filter simulates the energy loss at the string's bridge and nut — higher frequencies lose energy faster than lower ones, just as they do on a real string. The sound evolves naturally from bright attack to mellow sustain.

What made this revolutionary was its **computational efficiency**. Unlike Hiller and Ruiz's approach, which required solving differential equations at every time step, Karplus-Strong needed only a delay line and a simple filter — operations trivially cheap even on 1980s hardware. A convincing plucked string could be generated with a fraction of the computation required by other synthesis methods.

### Digital Waveguides: Julius O. Smith III (1980s–1990s)

**Julius O. Smith III**, also at Stanford's Center for Computer Research in Music and Acoustics (CCRMA), recognised that the Karplus-Strong algorithm was a special case of something much more general. Throughout the 1980s and into the 1990s, he developed **digital waveguide synthesis** — a comprehensive framework for modelling wave propagation in one-dimensional structures like strings and tubes.

Smith showed that the d'Alembert solution to the wave equation — which describes a vibrating string as two travelling waves moving in opposite directions — could be efficiently implemented using a pair of delay lines. By placing filters at the boundaries (representing the bridge, nut, finger position, or the bell of a wind instrument), extraordinarily realistic simulations of stringed and wind instruments could be achieved at minimal computational cost.

The digital waveguide framework elegantly unified several phenomena:
- **Plucked strings**: Initial broadband excitation decaying through filtered delay
- **Bowed strings**: Continuous excitation modulated by the nonlinear friction between bow and string
- **Wind instruments**: Standing waves in tubes, with the excitation mechanism (reed, lip, air jet) modelled at one end
- **Percussion**: Coupled waveguide networks for plates, bars, and membranes

Smith's work earned him wide recognition, and his freely published online textbook, *Physical Audio Signal Processing*, remains the definitive reference in the field.

### The Yamaha VL1: Physical Modelling Goes Commercial (1994)

In **1994**, Yamaha released the **VL1** (Virtual Lead), the first commercially available physical modelling synthesiser. Developed in collaboration with Stanford (based on Smith's waveguide research), the VL1 was a two-voice keyboard that modelled wind and string instruments with unprecedented realism.

The VL1 was a revelation. Players could control the sound with breath controllers and aftertouch in a way that felt organic — because the underlying model responded to continuous excitation just as a real instrument would. Blowing harder into a virtual clarinet didn't just make it louder; it changed the timbre, the overtone balance, and the onset characteristics in the same way a real clarinet responds. The instrument won the Technical Grammy Award.

However, the VL1 was expensive (approximately $5,000 USD at launch) and limited to two voices. Physical modelling's computational demands meant that polyphony was severely constrained by 1990s DSP hardware.

Yamaha followed with the **VL1m** (rackmount), **VL7** (more affordable, single-voice), and the **VP1** — a prototype 64-voice instrument shown at trade shows but never commercially released due to its extraordinary cost.

### Expanding the Field (1990s–2000s)

The 1990s saw an explosion of research and commercial interest in physical modelling:

**Korg** released the **Prophecy** (1995) and **Z1** (1997), which included physical modelling alongside other synthesis methods. The Z1's "MOSS" (Multi-Oscillator Synthesis System) engine offered plucked string, bowed string, organ pipe, and electric piano models.

**Technics** (Matsushita/Panasonic) developed the **WSA1** (1995), which used a different approach — modelling the resonant body separately from the excitation, allowing mix-and-match combinations.

**Applied Acoustics Systems** (AAS), founded in 1998 in Montreal, developed software-based physical modelling instruments. Their products — **Tassman**, **Lounge Lizard** (electric piano), **Strum** (guitar), **Chromaphone** (percussion), and **Ultra Analog** — demonstrated that physical modelling could thrive as software as desktop computers grew more powerful.

**Arturia** entered the field with the **Brass** plugin (2004), modelling brass instruments, though it received mixed reviews for playability.

### Modal Synthesis and Beyond

While waveguide synthesis excels at one-dimensional structures (strings, tubes), other approaches emerged for more complex resonating bodies:

**Modal synthesis** represents an object as a collection of resonant modes — each with its own frequency, amplitude, and decay rate. When excited, these modes ring simultaneously, producing the characteristic sound of bells, gongs, cymbals, and other metallic objects. The advantage of modal synthesis is that it naturally handles the **inharmonic** partial structures of these instruments, which waveguide synthesis struggles with.

**Finite element methods** (FEM) and **finite difference methods** (FDM) solve the wave equation on 2D and 3D grids, allowing simulation of drum heads, plates, and room acoustics. These are computationally expensive but increasingly feasible on modern hardware.

**Mass-spring models** represent an object as a network of masses connected by springs, with damping at each node. This approach can model arbitrary geometries but requires careful tuning.

### The Software Era (2000s–Present)

As computers grew exponentially more powerful, physical modelling moved decisively into software:

- **Pianoteq** (Modartt, 2006) — Perhaps the most celebrated physical modelling instrument, Pianoteq models the entire piano: strings, hammer hardness, soundboard, frame, and pedal mechanisms. Updated continuously, it is widely regarded as producing the most realistic piano sounds of any synthesis method.
- **Sculpture** (Apple, 2004) — Included in Logic Pro, Sculpture offers a component-based physical modelling system with multiple objects, exciters, and body resonances.
- **Kaivo** (Madrona Labs, 2013) — Combines granular synthesis with physical modelling resonators, allowing any sound source to excite physical models.
- **Collision** (Ableton, 2009) — Included in Ableton Live, Collision models struck and bowed mallet instruments using modal synthesis.
- **Chromaphone** (Applied Acoustics Systems, 2010) — Models a wide range of percussion using coupled resonators.
- **SWAM** instruments (Audio Modelling) — Highly expressive physical models of orchestral instruments, designed for real-time performance with continuous controllers.

### Web Audio and the Browser (2010s–Present)

The introduction of the **Web Audio API** in the early 2010s brought synthesis directly into the web browser. While initially limited, the API now provides the building blocks — oscillators, filters, delay lines, and scriptable audio processing via AudioWorklets — to implement physical modelling synthesis without plugins or downloads.

This synthesiser uses the Web Audio API to implement:
- **Karplus-Strong** plucked string synthesis via filtered harmonic series with natural decay
- **Waveguide-inspired** tube and pipe models with standing wave behaviour
- **Modal synthesis** for bells, gongs, and metallic percussion
- **Membrane models** based on circular membrane mode ratios (Bessel function zeros)
- **Bar/beam models** using the characteristic squared-frequency partial series

### The Future

Physical modelling continues to advance on multiple fronts:

- **Machine learning** is being used to learn physical model parameters from recordings of real instruments, automating the traditionally painstaking process of hand-tuning models
- **GPU-accelerated** finite difference solvers enable real-time simulation of complex 3D geometries
- **Haptic feedback** controllers allow performers to feel the resistance and vibration of virtual instruments
- **Hybrid approaches** combine physical modelling with other synthesis methods — using ML-generated excitation signals, or feeding sampled sounds through physical resonators

The fundamental appeal of physical modelling endures: it produces sound from **cause and effect**, not from stored data. A physical model doesn't just sound like a violin — it *behaves* like one. And as computational power continues to grow, the fidelity and complexity of these simulations will only increase.

---

## Technical Details

### Models Implemented

| Model | Technique | Partial Structure |
|-------|-----------|-------------------|
| **String** | Karplus-Strong / harmonic series with pickup simulation | Harmonic (1, 2, 3, 4...) with inharmonicity from stiffness |
| **Tube** | Waveguide-inspired, open/closed pipe simulation | Open: all harmonics; Closed: odd harmonics only |
| **Membrane** | Circular membrane mode simulation | Inharmonic (1.000, 1.593, 2.136, 2.296, 2.653...) |
| **Bar** | Euler-Bernoulli beam model | Inharmonic squared series (1, 2.76, 5.40, 8.93...) |
| **Modal** | Modal resonance with tuneable partials | Bell-like (1, 2, 3, 4.2, 5.4, 6.8, 8.1...) |

### Parameters

- **Damping** — Rate of high-frequency energy loss (simulates material absorption)
- **Brightness** — Number and amplitude of upper partials
- **Pickup Position** — Where along the string/body the sound is sampled (affects harmonic balance)
- **Stiffness** — Introduces inharmonicity (partials shift progressively sharp)
- **Decay Time** — Overall sustain duration
- **Body Size / Tone** — Resonant body characteristics
- **Sympathetic** — Sympathetic resonance from adjacent strings/modes

---

## Running Locally

```bash
git clone https://github.com/BrendanJamesLynskey/Synth_Physical_Modelling.git
cd Synth_Physical_Modelling
python3 -m http.server 8000
# Open http://localhost:8000
```

No build step, no dependencies. Just a web server and a browser.

---

## Browser Support

- Chrome / Edge (recommended)
- Firefox
- Safari (iOS 14.5+)

---

## References

- Karplus, K. and Strong, A. (1983). "Digital Synthesis of Plucked-String and Drum Timbres." *Computer Music Journal*, 7(2).
- Smith, J.O. III. *Physical Audio Signal Processing*. Online book, CCRMA, Stanford University.
- Hiller, L. and Ruiz, P. (1971). "Synthesizing Musical Sounds by Solving the Wave Equation for Vibrating Objects." *Journal of the Audio Engineering Society*, 19(6).
- Rossing, T.D. (2000). *Science of Percussion Instruments*. World Scientific.
- Fletcher, N.H. and Rossing, T.D. (1998). *The Physics of Musical Instruments*. Springer.

---

Web Audio API · Canvas · No dependencies

[Source on GitHub](https://github.com/BrendanJamesLynskey/Synth_Physical_Modelling)
