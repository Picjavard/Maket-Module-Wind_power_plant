# Maket-Module-Wind_power_plant
 Модуль ветряной электростанции для макета демонстрации альтернативных источников электроэнергии

## Список компонентов

* Моторчик 3V
* Микроконтроллер Arduino
* OLED-дисплей (1306 128x64, I2C) - https://sl.aliexpress.ru/p?key=LR1dsBY
* Резистор 220Ом - 1 шт.

## 3D-модели для печати

Thingiverse: https://www.thingiverse.com/thing:6749869

![Ветряк v14](https://github.com/user-attachments/assets/2c5b436e-3aa5-409a-82d8-794be2f303d0)

## Подключение


### OLED-дисплей

| OLED-дисплей	| Arduino Nano |	Arduino Micro / Pro Micro |
| :---:| :---:| :---:|
| GND	| GND |	GND |
| VCC	| 5V |	5V |
| SCL	| A5 | 3 |
| SDA	| A4 |	2 |

### Моторчик

![circuit (4)](https://github.com/user-attachments/assets/6fe67ea1-b18c-46a8-8df1-530ae1aedb67)

## Код

```cpp
#include <GyverOLED.h>
GyverOLED<SSD1306_128x64, OLED_NO_BUFFER> oled;

#include <TimerMs.h>
// (период, мс), (0 не запущен / 1 запущен), (режим: 0 период / 1 таймер)

TimerMs tmrDisplay(1000, 1, 1);

void setup() {
  //Serial.begin(9600);
  oled.init();  // инициализация
  oled.clear();
  oled.autoPrintln(false);
  oled.setScale(4);
  oled.setCursor(0, 0);
  oled.print("Init");
  oled.update();

  delay(1000);

  tmrDisplay.setPeriodMode();
}

void loop() {
  if (tmrDisplay.tick()) {
    oled.clear();
    oled.setCursor(0, 0);
    float voltage = (float)(analogRead(0) * 5.0) / 1024;
    oled.setCursor(0, 4);
    oled.print(voltage);
    oled.print("кВт");
    oled.update();
    //Serial.println(voltage);
  }
}
```
