# 🖐️ Peel It
> **Theme:** Vignette (A focused, atmospheric slice of a canteen)  
> **Platform:** PC (Windows)  
> **Role:** Solo Developer (CS Student)

## 📋 Project Overview
**Peel It** is a tactile, first-person interaction game set in a deserted school canteen. The player is tasked with the oddly satisfying—yet frustrating—job of removing stubborn stickers from plastic cafeteria furniture. 

The core gameplay loop focuses on the "struggle" of the peel, using physical camera feedback and shader manipulation to simulate the tension and resistance of old adhesive.

---

## ⚙️ Technical Highlights
Since this was a solo technical challenge, the architecture focuses on optimization and dynamic systems:

* **Custom Primitive Data (CPD) Workflow:** To animate the peeling effect efficiently, I utilized **CPD**. This allows the engine to send "Peel Intensity" values directly to the GPU's primitive buffer, avoiding the overhead of unique Dynamic Material Instances for every sticker.
* **Procedural UI Catalog:** The collection menu is built procedurally at runtime. A `For Each Loop` iterates through a texture array, instantiates "Icon Widgets" with **Exposed on Spawn** variables, and injects them into a **Horizontal Box**.
* **Input State Machine:** Implemented a hybrid **Game and UI Input Mode**. This ensures the mouse is captured for the 3D "struggle" mechanic but released for UI navigation when the catalog is toggled.
* **Resolution & Aspect Constraint:** To ensure the "Vignette" framing remained consistent, I forced a **16:9 Aspect Ratio** and a fixed **1920x1080** resolution via console commands.

---

## 🚧 Solo Developer Hurdles (Post-Mortem)
Building a project alone in a 7-day sprint required rapid troubleshooting of engine-specific quirks:

### 1. The "Invisible" CPD Variable
* **Issue:** Parameters disappear from Material Instances when "Use Custom Primitive Data" is enabled.
* **Solve:** Realized CPD bypasses the standard Material Instance UI; refactored logic to address the **Primitive Data Index** directly within the Actor’s Mesh Component memory buffer.

### 2. UI Reference Overwriting
* **Issue:** Attempting to add a single widget reference to the Horizontal Box multiple times resulted in only one icon appearing.
* **Solve:** Fixed logic to **Create Widget** (instantiate) a new object for every array element, ensuring unique parent-child relationships for every sticker icon.

### 3. Viewport Stretching
* **Issue:** The "Free Aspect" nature of the editor caused UI drifting and camera distortion.
* **Solve:** Used **Constrain Aspect Ratio** on the Camera Component and locked the viewport size using the following command on `BeginPlay`:
    ```cpp
    r.setres 1920x1080w
    ```

---

## 🎮 How to Play
1.  Download the **Peel It** build folder.
2.  Launch `PeelIt.exe`.
3.  **Controls:**
    * **Left Mouse (Hold):** Struggle / Peel the sticker.
    * **Mouse Move:** Control pull direction and camera.
    * **Tab:** Open/Close Sticker Catalog.

---

## 🎓 Reflection
This project was an intensive deep-dive into the UE5 pipeline. It required mastering the communication between Blueprints and Shaders while handling the full stack: from **Quixel Bridge** asset integration in the canteen environment to the final **Shipping Build** packaging. It stands as a testament to solving complex architectural problems under a strict "Game Jam" deadline.
