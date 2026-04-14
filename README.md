# L476-PJ13-Four7SegmentDisplay

This project demonstrates how to control a **4-digit 7-segment display** using an STM32 microcontroller with multiplexing.

---

## 📌 Features

- Display a 4-digit number (e.g., `1234`)
- Multiplexing technique for digit scanning
- Uses GPIO direct register (`ODR`) for fast output
- Adjustable refresh rate

---

## 🧠 How It Works

The number is split into four digits:

- MSD (Most Significant Digit)
- MID2
- MID1
- LSD (Least Significant Digit)

Example: Count = 1234
MSD = 1
MID2 = 2
MID1 = 3
LSD = 4


Each digit is displayed one at a time very quickly (multiplexing), creating the illusion that all digits are ON simultaneously.

---

## ⚙️ Hardware Setup

| Segment | Pin |
|--------|-----|
| a–g    | PC0–PC6 |
| Digit1 | PC7 |
| Digit2 | PC8 |
| Digit3 | PC9 |
| Digit4 | PC10 |

---

## 💻 Code Overview

### Segment Mapping

```c
uint16_t LEDS[] = {
  0x3F, // 0
  0x06, // 1
  0x5B, // 2
  0x4F, // 3
  0x66, // 4
  0x6D, // 5
  0x7D, // 6
  0x07, // 7
  0x7F, // 8
  0x6F  // 9
};

Main Loop (Multiplexing)

GPIOC->ODR = (GPIOC->ODR & 0xFF80) | LEDS[MSD];
HAL_GPIO_WritePin(GPIOC, digit1, GPIO_PIN_SET);
HAL_Delay(5);
HAL_GPIO_WritePin(GPIOC, digit1, GPIO_PIN_RESET);

--

## ⚙️ Result

![demo](./images/IMG_demo.jpg)


🛠️ Future Improvements
Use Timer Interrupt instead of HAL_Delay
Add button input to change number
Support hex display (A–F)
Brightness control using PWM
