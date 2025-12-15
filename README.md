# universal-media-deck
What I am trying to do? It's a wireless, Bluetooth controller for listening to music/general media playing in desktop. It allows me to control volume and skip tracks without pressing alt-tab or closing tab when I am doing another task. Unlike standard macro pads/controller, this can rotary encoder for volume and an integrated LCD screen.

My planning: I will use an ESP32-C3 or S3 microcontroller. It will broadcast itself as a Bluetooth HID.
It can volume up and down with the knob. Media next/prev/pause using the buttons. A small screen provide visual feedback.

| Part | Est. Cost ($USD) | Purpose |
| :--- | :--- | :--- |
| **Seeeduino XIAO ESP32S3** | ~$10 | Microcontroller with **Bluetooth HID** and Wi-Fi capabilities to drive the screen and handle inputs. |
| **1.28" Round LCD (GC9A01)** | ~$15 | High-resolution circular display for visual feedback (volume levels, layer status, animations). |
| **Rotary Encoder (EC11)** | ~$3 | **Through-hole** infinite rotation knob for volume control; includes an integrated push-button (Mute/Play). |
| **Mechanical Switches (x3)** | ~$3 | **Through-hole** tactile switches for media controls (Previous, Play/Pause, Next). |
| **LiPo Battery (500-1000mAh)** | ~$8 | Rechargeable power source to make the device completely wireless. |
| **TP4056 Charging Module** | ~$2 | Integrated circuit to safely charge the LiPo battery via USB. |
| **SPDT Slide Switch** | ~$1 | Physical toggle switch to cut power from the battery when not in use. |
| **3D Printed Case** | ~$2 | Enclosure to house the electronics, hold the screen at a 45° angle (Required for T4/T5). |
| **Custom PCB** | ~$20* | Connects all components without messy wiring. *(Not sure if I can get voucher to buy the pcb).* |
| **Total Parts Cost (Cash)** | **~$44**(without Custom PCB) | **This fits into the Tier 4 budget ($50).** |

Planning Graph
Schmedic: 
<img width="885" height="705" alt="image" src="https://github.com/user-attachments/assets/799e39c4-3de2-433e-968e-037f7f6ef4fb" />
PCB
2D:
<img width="722" height="715" alt="image" src="https://github.com/user-attachments/assets/33544bb3-50f6-4952-956a-966493a25d2d" />
3D
Front:
<img width="873" height="903" alt="image" src="https://github.com/user-attachments/assets/8fe7a115-e5f0-4532-8c2e-c1492db3e562" />
Back:
<img width="946" height="908" alt="image" src="https://github.com/user-attachments/assets/3b03dd72-2599-4b18-a04e-d0250702009e" />
