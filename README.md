# Motion detection using PIR sensor and STM32G474RE

A simple, interrupt-driven motion detection system built with the STM32 HAL (Hardware Abstraction Layer). This project uses a PIR (Passive Infrared) sensor to trigger an LED.

## 🚀 Overview
The system monitors a PIR sensor input via an External Interrupt (EXTI). When motion is detected, the microcontroller triggers a visual alert (LED) for a predefined duration.

---

## 🛠 Hardware Requirements
* **Microcontroller:** STM32 (configured for high-speed internal clock)
* **Sensor:** PIR Motion Sensor (HC-SR501 or similar)
* **Indicator:** Onboard or External LED
* **Connections:**
    * **PIR Signal:** PA0 (GPIOA)
    * **LED Pin:** PA5 (GPIOA)

---

## 📌 Pin Configuration

| Component | Pin | Port | Mode |
| :--- | :--- | :--- | :--- |
| **PIR Sensor** | PA0 | GPIOA | Interrupt (Rising/Falling Edge) |
| **LED** | PA5 | GPIOA | Push-Pull Output |

---

## ⚙️ How It Works

1. **Initialization:** The system initializes the HAL, configures the System Clock to 170MHz (PLL), and sets up the GPIOs.
2. **Interrupt Detection:** - The PIR sensor is configured on pin **PA0** with interrupts enabled.
   - When motion starts or stops, `HAL_GPIO_EXTI_Callback` is triggered.
   - The status of the sensor is captured in the variable `pirStatus`.
3. **Control Loop:** - The `main` loop checks the `pirStatus` flag.
   - If `pirStatus` is high, the LED on **PA5** turns on for **1000ms**.
   - After the delay, the LED turns off and the flag is reset.

---

## 💻 Code Structure

* **`main.c`**: Primary application logic.
* **`MX_GPIO_Init()`**: Configures the pins for the PIR sensor and LED.
* **`HAL_GPIO_EXTI_Callback()`**: Handles the real-time hardware signal from the sensor.
* **`SystemClock_Config()`**: Sets up the MCU to run at high performance using the HSI (Internal High Speed) oscillator.

---

## 🛠 Setup & Build

1. Open the project in **STM32CubeIDE**.
2. Connect your STM32 board via USB.
3. Connect the PIR sensor VCC to 3.3V/5V, GND to GND, and OUT to **PA0**.
4. Build the project (Ctrl + B).
5. Flash the code (F11).

---

## 📝 License
Copyright (c) 2024 STMicroelectronics. All rights reserved. 
This software is licensed under terms that can be found in the LICENSE file in the root directory.
 
