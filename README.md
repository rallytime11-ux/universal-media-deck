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
|  | ~$Total Est~ | 70 |


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

Code(C++):
#include <BleKeyboard.h>
#include <TFT_eSPI.h>
#include <RotaryEncoder.h>

// 1. Initialization
BleKeyboard bleKeyboard("Media Deck", "Maker Name", 100);
TFT_eSPI display = TFT_eSPI();

// Define pins for Encoder, its button (SW), and the 3 media buttons
RotaryEncoder encoder(ENCODER_CLK_PIN, ENCODER_DT_PIN, RotaryEncoder::LatchMode::FOUR3);
const int ENCODER_SW_PIN = 10;
const int BTN_NEXT_PIN = 11;
const int BTN_PREV_PIN = 12;
const int BTN_PAUSE_PIN = 13;

void setup() {
    // Start Bluetooth
    bleKeyboard.begin();
    // Initialize Display
    display.init();
    display.fillScreen(TFT_BLACK);
    display.setRotation(1); 
    // Initialize Encoder Pins
    pinMode(ENCODER_SW_PIN, INPUT_PULLUP);
    // Initialize Button Pins (using pullup resistors)
    pinMode(BTN_NEXT_PIN, INPUT_PULLUP);
    // ... Initialize PREV and PAUSE pins ...

    // Display welcome screen
    display.drawString("Deck Ready", 10, 10, 4);
}

// 2. Main Loop Logic
void loop() {
    // Check if the device is connected via Bluetooth
    if (bleKeyboard.isConnected()) {
        
        // --- Encoder (Volume Control) ---
        encoder.tick(); // Update encoder state
        int newPosition = encoder.getPosition();
        static int lastPosition = 0;

        if (newPosition != lastPosition) {
            if (newPosition > lastPosition) {
                // Volume Up (Turned Right)
                bleKeyboard.write(KEY_MEDIA_VOLUME_UP);
            } else {
                // Volume Down (Turned Left)
                bleKeyboard.write(KEY_MEDIA_VOLUME_DOWN);
            }
            display.updateVolumeBar(newPosition); // Function to update visual bar
            lastPosition = newPosition;
        }

        // --- Encoder Button (Play/Pause/Mute) ---
        if (digitalRead(ENCODER_SW_PIN) == LOW) { // Button is pressed
            // Debounce delay here
            bleKeyboard.write(KEY_MEDIA_PLAY_PAUSE);
            display.showIcon("PLAY / PAUSE");
        }

        // --- Dedicated Buttons (Next/Previous) ---
        if (digitalRead(BTN_NEXT_PIN) == LOW) {
            // Debounce delay here
            bleKeyboard.write(KEY_MEDIA_NEXT_TRACK);
            display.showIcon("NEXT");
        }
        // ... Logic for BTN_PREV and BTN_PAUSE ...

    } else {
        // Display "DISCONNECTED" on the screen
        display.drawString("Disconnected", 10, 50, 2);
    }
}
