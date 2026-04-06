
🖐️ Peel It
A solo Unreal Engine 5 "Vignette" project developed in 7 days.

📋 Project Overview
Peel It is a tactile, first-person interaction game set in a deserted school canteen. The player is tasked with the oddly satisfying—yet frustrating—job of removing stubborn stickers from plastic cafeteria furniture. The core gameplay loop focuses on the "struggle" of the peel, using physical camera feedback and shader manipulation to simulate the tension of old adhesive.

Theme: Vignette (A focused, atmospheric slice of a canteen)

Engine: Unreal Engine 5.3

Developer: Solo (CS Student)

⚙️ Technical Highlights
Since this was a solo technical challenge, the architecture focuses on optimization and dynamic systems:

Custom Primitive Data (CPD) Workflow: To animate the peeling effect efficiently, I utilized CPD. This allows the engine to send "Peel Intensity" values directly to the GPU's primitive buffer. This avoided the overhead of creating unique Dynamic Material Instances for every sticker, keeping the draw calls low.

Dynamic UI Catalog: The collection menu is built procedurally. A For Each Loop iterates through a texture array, instantiates "Icon Widgets" with Exposed on Spawn variables, and injects them into a Horizontal Box.

Input State Machine: Implemented a hybrid Game and UI Input Mode. This allows the mouse to be captured for the 3D "struggle" mechanic while releasing it seamlessly for UI navigation when the catalog is toggled.

Resolution & Aspect Constraint: To ensure the "Vignette" remained visually consistent across various hardware, I forced a 16:9 Aspect Ratio and a fixed 1920x1080 resolution via console commands.

🚧 Solo Developer Hurdles (Post-Mortem)
Building a project alone in a week required rapid troubleshooting of engine-specific quirks:

The "Invisible" CPD Variable: * Issue: Parameters disappear from Material Instances when "Use Custom Primitive Data" is enabled.

Solve: Realized CPD bypasses the standard Material Instance UI; refactored logic to address the Primitive Data Index directly within the Mesh Component's memory buffer.

UI Reference Overwriting:

Issue: Attempting to add a single widget reference to the Horizontal Box multiple times resulted in only one icon appearing.

Solve: Fixed the logic to Create Widget (instantiate) a new object for every array element, ensuring each sticker had a unique parent-child relationship.

Viewport Stretching:

Issue: The "Free Aspect" nature of the editor caused UI drifting and camera distortion.

Solve: Used Constrain Aspect Ratio on the Camera Component and locked the viewport size using r.setres to maintain the intended framing.

🎮 How to Play
Download the Peel It build folder.

Launch PeelIt.exe.
