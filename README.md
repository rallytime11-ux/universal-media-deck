# universal-media-deck
What I am trying to do? It's a wireless, Bluetooth controller for listening to music/general media playing in desktop. It allows me to control volume and skip tracks without pressing alt-tab or closing tab when I am doing another task. Unlike standard macro pads/controller, this can rotary encoder for volume and an integrated LCD screen.

My planning: I will use an ESP32-C3 or S3 microcontroller. It will broadcast itself as a Bluetooth HID.
It can volume up and down with the knob. Media next/prev/pause using the buttons. A small screen provide visual feedback.

| Part | Est. Cost ($USD) | Purpose |
| :--- | :--- | :--- |
| **Seeeduino XIAO ESP32S3** | ~$10 | Microcontroller with **Bluetooth HID** and high performance for driving the screen. |
| **1.28" Round LCD (GC9A01)** | ~$15 | Display for real-time visual feedback (volume/status). |
| **Rotary Encoder (EC11)** | ~$3 | **Through-hole** infinite rotation knob for volume control; includes an integrated push-button. |
| **Mechanical Switches (x3)** | ~$3 | **Through-hole** switches for tactile media control (e.g., Next, Previous). |
| **LiPo Battery (500-1000mAh)** | ~$8 | To make my device wireless (independent). |
| **TP4056 Charging Module** | ~$2 | **Module-based charging** for the LiPo battery. (Simplified: Avoids complex on-board charging circuit design). |
| **SPDT Slide Switch** | ~$1 | Physical On/Off switch for power control. |
| **Custom PCB** | ~$20 | To mount all components and modules, eliminating messy wiring. |
| **3D Printed Case** | ~$2 | Enclosure for desktop use. |
|  | $Total Est~ | $70 |


Planning Graph
Schmedic: 
<img width="885" height="705" alt="image" src="https://github.com/user-attachments/assets/799e39c4-3de2-433e-968e-037f7f6ef4fb" />
PCB
2D:
<img width="1035" height="738" alt="image" src="https://github.com/user-attachments/assets/8d200b32-d39f-42ce-9d1e-c4c6bbe3b913" />
3D
Front:
<img width="1132" height="707" alt="image" src="https://github.com/user-attachments/assets/364d5f47-c3c0-473f-bfb5-3afeef045ca0" />
Back:
<img width="929" height="690" alt="image" src="https://github.com/user-attachments/assets/2b1ed037-6c78-425a-b60b-1aa41d9fddcc" />
