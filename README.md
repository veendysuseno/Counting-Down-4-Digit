# Counting Down 4 Digit

## Description

The Counting Down 4 Digit project demonstrates a countdown timer using a 4-digit 7-segment display. The timer counts down from 100 and displays the countdown on the 7-segment display. The display alternates between showing the tens and units digits.

## Components

- Arduino (e.g., Arduino Uno)
- 4-Digit 7-Segment Display
- Jumper Wires
- Resistors (if required for 7-segment display)

## Pin Configuration

| Segment Pin    | Arduino Pin |
| -------------- | ----------- |
| 1              | 2           |
| 2              | 3           |
| 3              | 4           |
| 4              | 5           |
| 5              | 6           |
| 6              | 7           |
| 7              | 8           |
| Common Anode   | 9           |
| Digit Select 1 | 10          |
| Digit Select 2 | 11          |

## Code

```cpp
// Counting-Down-4-Digit
byte nilai,i;
byte seven_seg_digits[10][7] = { { 0,0,0,0,0,0,1 },  // = 0
                                 { 1,0,0,1,1,1,1 },  // = 1
                                 { 0,0,1,0,0,1,0 },  // = 2
                                 { 0,0,0,0,1,1,0 },  // = 3
                                 { 1,0,0,1,1,0,0 },  // = 4
                                 { 0,1,0,0,1,0,0 },  // = 5
                                 { 0,1,0,0,0,0,0 },  // = 6
                                 { 0,0,0,1,1,1,1 },  // = 7
                                 { 0,0,0,0,0,0,0 },  // = 8
                                 { 0,0,0,0,1,0,0 }   // = 9
                                  };

void setup() {
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(10, OUTPUT);
  pinMode(11, OUTPUT);
  digitalWrite(9,HIGH);
  nilai=100;
}

void sevenSegWrite(byte segment) {
  byte pin = 2;
  for (byte segCount = 0; segCount < 7; ++segCount) {
    digitalWrite(pin, seven_seg_digits[segment][segCount]);
    ++pin;
  }
}

void loop() {
  nilai--;
  for(i=0;i<100;i++){
      digitalWrite(10,LOW);
      digitalWrite(11,HIGH);
      sevenSegWrite(nilai/10);
      delay(5);
      digitalWrite(10,HIGH);
      digitalWrite(11,LOW);
      sevenSegWrite(nilai%10);
      delay(5);
  }
  if(nilai==0) nilai=100;
}
```

## How It Works

1. Initialization:
   - The setup() function configures the pins connected to the 7-segment display as outputs.
   - The initial countdown value is set to 100.
2. Countdown Operation:
   - The loop() function continuously decrements the countdown value.
   - The display alternates between showing the tens and units digits with a brief delay.
   - When the countdown reaches 0, it resets to 100 and continues.
3. Display Control:
   - The sevenSegWrite() function sends the appropriate signals to the 7-segment display to show the correct digit.

## Usage

1. Connect the 4-digit 7-segment display to the Arduino using the specified pin configuration.
2. Upload the code to the Arduino.
3. Observe the countdown on the display, which will repeat from 100 to 0.

## Notes

• Ensure that the 7-segment display is properly connected and that resistors are used if needed.
• The display may need to be adjusted depending on the specific 7-segment display model used.
