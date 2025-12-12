# ∿ C Y M A T I C A
### Pro Audio Visualization Engine

![Version](https://img.shields.io/badge/Version-2.0-00ffcc?style=for-the-badge)
![Tech](https://img.shields.io/badge/Three.js-WebGL-white?style=for-the-badge&logo=three.js)
![Audio](https://img.shields.io/badge/Web_Audio_API-High_Fidelity-blue?style=for-the-badge)

> **Cymatica** is a browser-based generative audio engine. It utilizes **WebGL shaders (GLSL)** and the **Web Audio API** to interpret audio frequencies into real-time, physics-based visual phenomena. 

---

## 🌟 Key Features

*   **⚡ Zero Dependencies:** Runs entirely within a single HTML file (imports Three.js via CDN).
*   **🔊 Physics-Based Audio Engine:** Uses spring-mass simulation to give bass hits "weight" and velocity.
*   **🎨 10 Visual Modes:** A diverse collection of skins ranging from abstract to retro.
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

---

## 🎨 Visual Modes (Skins)

Cymatica v10 includes **10 distinctive visual engines**:

| Skin | Description | Audio Reactivity |
| :--- | :--- | :--- |
| **NEON** | **Wireframe Core.** Cyberpunk aesthetic with floating particles. | **Bass:** Pulse. **Treble:** Particle scatter. |
| **VOID** | **Ferrofluid.** Dark, liquid surface with reflective lighting. | **Bass:** Liquid ripples. **Mids:** Distortion. |
| **SOLAR** | **Star Surface.** Turbulent plasma sphere with solar flares. | **Bass:** Ejection flares. **Mids:** Temp color. |
| **QUANTUM** | **Particle Swarm.** 8,000 data points acting as a hive mind. | **Bass:** Magnetic shattering. **Treble:** Jitter. |
| **PLASMA** | **Energy Field.** Volatile electric arcs contained in a field. | **Bass:** Expansion. **Treble:** Lightning. |
| **RETRO** | **Synthwave Grid.** Infinite scrolling landscape with a sun. | **Bass:** Terrain height. **Speed:** BPM. |
| **HELIX** | **DNA Structure.** Double helix points. | **Bass:** Twist intensity. |
| **CRYSTAL** | **Refraction.** Low-poly shard cluster with flat shading. | **Treble:** Light refraction index. |
| **WAVES** | **Tunnel.** Series of neon rings forming a tunnel. | **Full Spectrum:** Rings react to specific freqs. |
| **GLITCH** | **Artifacts.** A digital sphere that breaks down. | **Treble:** Vertex displacement glitches. |

---

## ⚙️ Technical Architecture

### The Audio Engine
Cymatica performs a **Fast Fourier Transform (FFT)** (Size: 2048) to separate the audio spectrum.
*   **Sub-Bass (20-80Hz):** Drives the physics engine (camera shake, global scale).
*   **Treble (4000Hz+):** Drives particle turbulence and glitch effects.

### Physics Simulation
```javascript
// Spring-mass logic for "Kick" feel
if (bass > threshold) velocity += impact;
velocity -= (scale - 1.0) * springForce;
velocity *= friction;
scale += velocity;
