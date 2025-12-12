# universal-media-deck
What I am trying to do? It's a wireless, Bluetooth controller for listening to music/general media playing in desktop. It allows me to control volume and skip tracks without pressing alt-tab or closing tab when I am doing another task. Unlike standard macro pads/controller, this can rotary encoder for volume and an integrated LCD screen.

My planning: I will use an ESP32-C3 or S3 microcontroller. It will broadcast itself as a Bluetooth HID.
It can volume up and down with the knob. Media next/prev/pause using the buttons. A small screen provide visual feedback.

| Part | Est. Cost | Purpose |
| :--- | :--- | :--- |
| **ESP32-S3 Dev Board** | ~$10 | Microcontroller with bluetooth and high performance for driving the screen. |
| **1.28" Round LCD (GC9A01)** | ~$15 | =Display for visual feedback |
| **Rotary Encoder (EC11)** | ~$5 | Infinite rotation knob for volume control. |
| **Mechanical Switches (x3)** | ~$5 | Switches for tactile media control. |
| **LiPo Battery (1000mAh)** | ~$8 | To make my device wireless (independent). |
| **TP4056 Charging Module** | ~$2 | USB-C charging logic for the battery. |
| **Custom PCB** | ~$20 | To mount components and avoid messy wiring. |
| **3D Printed Case** | ~$2 | I will print the enclosure to sit at a 45-degree angle on the desk. |\

Planning for PCB board
2D:
<img width="739" height="537" alt="image" src="https://github.com/user-attachments/assets/d891aa1a-e853-4c75-91cb-c246aa6cef67" />
3D
Front:
<img width="987" height="720" alt="image" src="https://github.com/user-attachments/assets/9e2a5d8a-6879-4938-9902-eda8dce37d42" />
Back:
<img width="962" height="682" alt="image" src="https://github.com/user-attachments/assets/75420071-a103-44b8-b553-705ab83d0c9d" />


Code(C++ with the `BleKeyboard` library.):
```cpp
// Pseudo-code concept
if (encoder.turnedRight()) {
    ble.send(KEY_MEDIA_VOLUME_UP);
    display.animateVolumeBar(UP);
}
if (buttonPlay.pressed()) {
    ble.send(KEY_MEDIA_PLAY_PAUSE);
    display.showIcon("PAUSE");
}
