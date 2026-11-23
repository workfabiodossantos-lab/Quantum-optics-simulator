# Quantum Optics Bench

An interactive 2D optical table that runs entirely in your browser. Place light sources, lenses, mirrors, wave plates and sensors, chain them together, and watch the light propagate in real time. You can work with classical laser beams or with **single photons**, which lets you build and measure **photonic qubits**.

The whole application is a single HTML file. It has no dependencies, needs no installation and no server, and works offline. The interface is available in **English and French**.

---

## Getting started

1. Download `banc-optique-quantique.html`.
2. Open it in a recent browser (Chrome, Edge, Firefox or Safari).
3. Pick an experiment from the **📚 Experiments…** menu, or start from an empty table with **New**.

Switch the interface language with the **FR | EN** buttons next to the title.

**Optional: open it like a desktop app.**
- **Chrome:** ⋮ menu → *Cast, save and share* → *Create shortcut…* → tick *Open as window*.
- **Edge:** ⋯ menu → *Apps* → *Install this site as an app*.

---

## Features

### Physics engine
| Domain | What is simulated |
|---|---|
| **Geometric optics** | Reflection, refraction (Snell's law), total internal reflection, thin lenses, curved mirrors |
| **Dispersion** | Wavelength-dependent refractive index (Cauchy law) for BK7, F2, SF11, fused silica, water and diamond, plus a custom index |
| **Wave optics** | Every beam carries a complex amplitude and phase `e^{ikL}` along its optical path. Sensors sum the *fields* of coherent beams, not their intensities, so interference emerges naturally |
| **Gaussian beams** | Complex beam parameter `q`: waist, divergence, focusing and wavefront curvature |
| **Diffraction** | Slits act as rows of Huygens secondary sources; gratings split light into orders `m` |
| **Polarization** | Full Jones calculus, plus s/p Fresnel coefficients at glass interfaces (Brewster angle) |
| **Quantum** | Single-photon mode: the probability amplitude takes every path, and exactly one detector clicks, drawn at random with the Born rule `P = \|ψ\|²` |

### Components
- **Sources:** laser (monochromatic, RGB or white light; any polarization), wide collimated beam, point source, single-photon source
- **Mirrors & splitters:** flat mirror, curved mirror, beam splitter with adjustable reflectivity, polarizing beam splitter (PBS)
- **Lenses & glass:** thin lens, glass block, prism
- **Polarization & phase:** polarizer, half-wave plate, quarter-wave plate, variable retarder, Faraday rotator, phase shifter
- **Filters & diffraction:** band-pass filter, neutral density filter, iris, single slit, double slit (Young), diffraction grating, beam dump

### Sensors
- **Photodiode / power meter:** optical power and photon flux
- **Single-photon detector (SPAD):** click counts, quantum efficiency, dark counts
- **Screen / CCD camera:** intensity profile; in photon mode, impacts build up one by one
- **Spectrometer:** power per wavelength
- **Polarimeter:** Stokes parameters, polarization ellipse, Poincaré sphere
- **Quantum state probe:** reads the state *without* disturbing it and shows it on the Bloch sphere. This is a simulation tool and does not exist as a physical device.

---

## Photonic qubits

Encoding: polarization **H = |0⟩**, **V = |1⟩**, D = |+⟩, R = |+i⟩.

| Quantum gate | Optical element |
|---|---|
| Hadamard (H) | Half-wave plate, θ = 22.5° |
| X (NOT) | Half-wave plate, θ = 45° |
| Z | Half-wave plate, θ = 0° |
| S (phase i) | Quarter-wave plate, θ = 0° |
| Any rotation | Variable retarder (θ, δ) or rotator |
| Measurement in the Z basis | PBS + two SPADs |

**Path qubits:** a 50/50 beam splitter creates a superposition of two paths, and a phase shifter sets the relative phase. A Mach-Zehnder interferometer implements a full single-qubit rotation. Place two probes with the same name, one in *rail |0⟩* mode and one in *rail |1⟩* mode, to see the path qubit on the Bloch sphere together with its coherence `|r|`. A value of `|r| < 1` means the qubit is entangled with another degree of freedom.

---

## Built-in experiments

| Experiment | What it shows |
|---|---|
| Mach-Zehnder: path qubit | Single-photon interference controlled by a phase shifter |
| "Which-path" information and quantum eraser | Decoherence through polarization tagging, and its erasure |
| Polarization qubit: Hadamard gate and measurement | Preparing \|+⟩ and measuring 50/50 |
| Gate chain: H · Z · H = X | A small quantum circuit built from wave plates |
| Young's slits, photon by photon | The interference pattern building up from random impacts |
| Young's slits (laser) | Fringe spacing λD/d under the diffraction envelope |
| Michelson interferometer | Tilt fringes and path-length sensitivity |
| Dispersion by a prism | White light split into a spectrum |
| Diffraction grating | Spectral orders focused by a lens |
| Lenses: Keplerian telescope | Beam reduction with f₁ / f₂ |
| Image formation (2f – 2f) | Sharp imaging of a point source |
| Malus's law | I = I₀ cos²θ |
| Brewster angle and Fresnel | Polarization by reflection |
| Fabry-Pérot cavity | Multiple-beam interference and resonances |

---

## Controls

| Action | Control |
|---|---|
| Add a component | Click it in the palette, or drag it onto the table |
| Move | Drag the component; arrow keys nudge it (Shift = 10 mm) |
| Rotate | Drag the blue ↻ handle (Shift = free angle), or `R` / `E` for ±15° (Shift = ±1°) |
| Edit parameters | Select the component and use the right-hand panel |
| Delete / duplicate / undo | `Del` · `Ctrl+D` · `Ctrl+Z` |
| Zoom / pan | Mouse wheel · drag the background |
| Emit one photon | `Space`, or the buttons in the quantum bar (×100, ×10 000, continuous stream) |

Your setup is saved automatically in the browser. Use **Export** and **Import** to keep setups as `.json` files or share them.

---

## Limitations

- The table is 2D, and lenses are paraxial, so there are no aberrations.
- Only one photon is simulated at a time. There are no entangled photon pairs (SPDC), Hong-Ou-Mandel effect or two-photon coincidences yet.
- Light diffracted by a slit is not refocused by a lens placed after it; it goes straight to the sensors.
- Matter is described only by its refractive index and transmission. There are no atoms, energy levels or resonant absorption.

---

## Roadmap ideas

- Photon-pair source (SPDC) and coincidence counter for entanglement, Bell tests and Hong-Ou-Mandel
- Multi-qubit circuits (CNOT with polarization and path)
- BB84 quantum key distribution scenario
- Desktop build with Electron

---

## Tech

Plain HTML, CSS and vanilla JavaScript, all contained in a single file. Rendering uses the Canvas 2D API. The code has no frameworks and no external libraries.