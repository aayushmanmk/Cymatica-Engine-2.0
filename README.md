# ∿ C Y M A T I C A   -   2 . 0
### Evolved Audio Visualization Engine

![Version](https://img.shields.io/badge/Version-2.0-00ffcc?style=for-the-badge)
![Tech](https://img.shields.io/badge/Three.js-WebGL-white?style=for-the-badge&logo=three.js)
![Audio](https://img.shields.io/badge/Web_Audio_API-High_Fidelity-blue?style=for-the-badge)

> **Cymatica** is a single-file, browser-based generative audio engine. It utilizes **WebGL shaders (GLSL)** and the **Web Audio API** to interpret audio frequencies into real-time, physics-based visual phenomena. Unlike standard visualizers, Cymatica employs a spring-physics model to simulate weight and impact for bass response.

---

## 🌟 Key Features

*   **⚡ Zero Dependencies:** Runs entirely within a single HTML file (imports Three.js via CDN).
*   **🔊 Physics-Based Audio Engine:** Uses spring-mass simulation to give bass hits "weight" and velocity.
*   **🎨 6 Distinct Visual Modes:** From retro landscapes to quantum particle swarms.
*   **🎛️ Pro Audio Tools:** Real-time playback speed control (0.5x - 1.5x), looping, and gain control.
*   **💎 High Fidelity:** Supports FLAC/WAV. Features volumetric lighting, bloom, and chromatic aberration.

---

## 🚀 Quick Start

### Option 1: VS Code (Recommended)
1.  Open the folder containing the file in VS Code.
2.  Install the **"Live Server"** extension.
3.  Right-click the HTML file and select **"Open with Live Server"**.

### Option 2: Python Local Server
Browsers often block the Web Audio API or high-res textures when running directly from `file://` due to CORS policies.
1.  Open your terminal in the project folder.
2.  Run:
    ```bash
    python3 -m http.server
    ```
3.  Navigate to `http://localhost:8000`.

### Option 3: Direct Open
You can simply drag the file into Chrome/Edge/Firefox, though some high-res audio features may be restricted by the browser security policies depending on your local settings.

---

## 🎚️ Control Deck Documentation

The UI is divided into three logical zones inside the collapsible Control Deck.

### 1. Playback
| Control | Description |
| :--- | :--- |
| **Play/Pause** | Toggles audio playback and the main render loop. |
| **Seek Bar** | Scrub through the track timeline. |
| **Time Display** | Shows current time vs total duration. |

### 2. Tools
| Tool | Function |
| :--- | :--- |
| **VOL (Volume)** | Master gain control (0% to 100%). |
| **SPD (Speed)** | Playback rate. **0.8x** for "Chopped & Screwed", **1.2x** for Nightcore. |
| **LOOP** | Toggles infinite looping of the current track. |

### 3. Visual Modes (Skins)
| Skin | Visual Aesthetic | Audio Reactivity |
| :--- | :--- | :--- |
| **NEON** | **Wireframe Core.** Cyberpunk aesthetic with floating data particles. | **Bass:** Core pulse. <br>**Treble:** Particle scatter. |
| **VOID** | **Ferrofluid.** Dark, liquid surface with reflective lighting. | **Bass:** Liquid ripples. <br>**Mids:** Surface tension distortion. |
| **SOLAR** | **Star Surface.** Turbulent plasma sphere with solar flares. | **Bass:** Ejection of solar flares. <br>**Mids:** Surface color temperature. |
| **TERRA** | **Digital Landscape.** Retro-futuristic infinite grid. | **Bass:** Terrain height generation. <br>**Treble:** Scroll speed. |
| **QUANTUM** | **Particle Swarm.** 8,000 individual data points acting as a hive mind. | **Bass:** Magnetic shattering (physics explosion). <br>**Treble:** Particle jitter. |
| **PLASMA** | **Energy Field.** Volatile electric arcs contained in a field. | **Bass:** Containment field expansion. <br>**Treble:** Lightning intensity. |

---

## ⚙️ Technical Architecture

### The Audio Engine
Cymatica does not simply map volume to scale. It performs a **Fast Fourier Transform (FFT)** (Size: 2048) to separate the audio spectrum.

1.  **Frequency Analysis:**
    *   **Sub-Bass (20-80Hz):** Drives the physics engine.
    *   **Mids (250-2000Hz):** Drives color shifting and surface detail.
    *   **Treble (4000Hz+):** Drives particle turbulence and glitch effects.
2.  **Physics Simulation:**
    ```javascript
    // Simplified logic of the internal engine
    if (bass > threshold) velocity += impact;
    velocity -= (scale - 1.0) * springForce;
    velocity *= friction;
    scale += velocity;
    ```

### The Rendering Pipeline
The visual output is constructed using **Three.js** with a custom post-processing stack:
1.  **Scene Render:** The base geometry and shaders.
2.  **UnrealBloomPass:** Adds the glowing, ethereal atmosphere.
3.  **RGBShiftShader:** Splits the Red, Green, and Blue channels based on the calculated physics velocity to simulate a camera lens impact during bass hits.

---

## 🛠️ Configuration
You can tweak the internal `CONFIG` object at the top of the `<script>` tag to adjust performance or visuals:

```javascript
const CONFIG = {
    fftSize: 2048,      // Audio resolution (Powers of 2: 1024, 2048, 4096)
    bloomStrength: 0.6, // Intensity of the glow
    bloomRadius: 0.6,   // Spread of the glow
    bloomThreshold: 0.15 // Brightness required to trigger glow
};
