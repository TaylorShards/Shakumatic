tzz. I will be changing this to 5 finger hole calcuator. For end-blown flutes. The Japanese Shakuhachi penatonic minor scale (5 holes). I might add options for other scales...

# Flutomat NG - Modernized Flute Calculator

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) <!-- Link to your LICENSE file -->

A web-based calculator for determining the embouchure and finger hole positions for a transverse flute based on acoustic principles. This project is a modernized implementation (**Next Generation**) of calculation methods widely used by instrument makers and enthusiasts, preserving valuable acoustic modeling techniques in an accessible format.

## 🌐 Online version

Check out the Flutomat here:  (works in landscape view on the phone)
👉 [https://unityrobot.github.io/Flutomat/](https://unityrobot.github.io/Flutomat/)

## Features

*   Calculates finger hole and embouchure positions based on the **Benade acoustic model** for cylindrical transverse flutes.
*   Accounts for **temperature variations** affecting the speed of sound.
*   Supports both **`cm`** and **`inches`** units.
*   Allows input of target frequencies directly or selection via a **musical key** (populates frequencies based on a major scale using correct MIDI reference A4=69).
*   Implements standard **acoustic corrections**:
    *   Open End Correction (`C_end`)
    *   Closed Hole Correction (`C_c`)
    *   Effective Hole Height (`t_e`)
    *   Embouchure Correction (using Kosel's empirical fit)
*   Uses a non-iterative **quadratic solution** for calculating hole positions.
*   Modern, user-friendly web interface built with standard HTML5, CSS3, and ES6+ JavaScript (Class-based, no global scope pollution).
*   Includes helpful notes and assumptions directly in the interface.
*   Input validation and clear display of results.

## How to Use

1.  **Download or Clone:** Get the project files (`flutomat.html`, `flutomat.css`, `flutomat.js`).
2.  **Open:** Open the `flutomat.html` file in your web browser.
3.  **Input Parameters:**
    *   Select measurement `Units` (cm or inches).
    *   Enter the ambient `Temperature` and select its unit (°C or °F). The calculated speed of sound will update automatically.
    *   Enter the flute's `Inside Bore Diameter` and `Wall Thickness`.
    *   Choose a `Key` from the selector to automatically populate target frequencies for a standard 6-hole major scale flute, *or* manually enter the `Target Frequency (Hz)` for the fundamental note (all holes closed) and for each finger hole note (when it's the first open hole).
    *   Enter the desired `Diameter` for the `Embouchure` hole and each `Finger Hole`.
4.  **Calculate:** Click the "Calculate Positions" button.
5.  **View Results:** The calculated physical distances of the hole centers from the open end of the flute tube will appear in the "Calculated Distance from Open End" column. The end of the flute is defined as 0.000.

## Technical Details & Acoustic Model

This calculator employs a simplified one-dimensional acoustic model suitable for cylindrical bore transverse flutes, largely based on the work of **Arthur H. Benade** ("Fundamentals of Musical Acoustics") and subsequent refinements found in practical tools. Key aspects include:

*   **Speed of Sound:** `V = 331.3 * sqrt(1 + TempC / 273.15)` m/s, converted to selected units.
*   **Acoustic Length:** The fundamental relationship `Frequency = SpeedOfSound / (2 * AcousticLength)` is used as a starting point.
*   **Corrections:** Various lengths are added or subtracted to the theoretical acoustic length to account for real-world effects, consistent with Benade's model:
    *   **End Correction (`C_end`):** `0.6133 * BoreRadius` accounts for the air extending slightly beyond the physical end.
    *   **Closed Hole Correction (`C_c`):** `0.25 * WallThickness * (HoleDiameter / BoreDiameter)^2` accounts for the small volume added by closed holes above the first open one.
    *   **Effective Hole Height (`t_e`):** `WallThickness + 0.75 * HoleDiameter` represents the effective acoustic height of an open hole's chimney.
    *   **Embouchure Correction (`C_emb`):** Kosel's empirical fit `(Bore/Demb)^2 * 10.84 * Wall * Demb / (Bore + 2*Wall)` is used to find the acoustic distance from the theoretical start of the air column to the embouchure.
*   **Position Calculation:** The positions are determined by solving impedance-matching equations derived by Benade. This implementation uses the direct quadratic solution method found in the original script (solving for acoustic positions `Xf`) as it avoids potential instabilities of iterative methods. Physical positions are then derived relative to the calculated effective acoustic end (`Xend`).

## Historical Context & Significance

The original script, **"Flutomat Javascript Flute Designer"**, was created by **Peter H. Kosel**. An archived version can be found here:
[http://web.archive.org/web/20110611151055/http://www.cwo.com/~ph_kosel/flutomat.html](http://web.archive.org/web/20110611151055/http://www.cwo.com/~ph_kosel/flutomat.html)

This original script, like others based on similar acoustic principles (especially from **Arthur H. Benade**), was foundational. It brought complex calculations to instrument makers via the web using early JavaScript (`JavaScript1.2`, detected as generated by `Netscape 4.7`). Such tools were invaluable before sophisticated modeling software became widespread.

**Flutomat NG (Next Generation)** aims to:

1.  **Preserve:** Keep a functional, understandable implementation of these important acoustic calculations available, as many original tools may be lost or incompatible.
2.  **Modernize:** Present the calculator using standard HTML5, CSS3, and modern JavaScript (ES6+ Classes, proper scope management, event listeners), removing outdated practices (like `with`, inline JS, table layouts for non-tabular data).
3.  **Enhance:** Improve upon the original by:
    *   Adding temperature-dependent speed of sound calculation.
    *   Correcting the MIDI-to-frequency calculation (using A4=69 standard).
    *   Implementing input validation and better user feedback.
    *   Improving code clarity with better variable names and structure.
4.  **Educate:** Provide a tool that demonstrates the practical application of acoustic principles in instrument design.

This revised version respects the original logic and acoustic formulas while making the tool more robust, maintainable, and user-friendly for today's web environment. It serves as a functional tool and a tribute to the early integration of physics and web technology for practical craft.

## Assumptions & Limitations

*   Assumes a **cylindrical bore**. Tapered bores require different, more complex calculations.
*   The model is **one-dimensional**, neglecting some complex 3D acoustic effects.
*   Assumes **standard transverse flute** acoustics.
*   Hole interactions are simplified based on the Benade model. Accuracy may decrease for very closely spaced holes or at very high frequencies (approaching hole cutoff frequencies).
*   The **cork/stopper position** is not calculated but is typically placed 1 to 1.5 times the embouchure diameter *towards the closed end* from the embouchure center, relative to the calculated `resultEmbouchure` position. This often requires fine-tuning.
*   Physical construction variables (chamfering, undercutting, pad height) are not explicitly modeled but are implicitly included in the empirically derived constants.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


## Contributing

Contributions, bug reports, or suggestions are welcome! Please feel free to open an issue or submit a pull request.
