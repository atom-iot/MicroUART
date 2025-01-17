![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![author](https://img.shields.io/badge/author-AlexGyver-informational.svg)
# MicroUART
Лёгкая реализация UART для ATmega328 и подобных из этого поколения
- Полный аналог Serial
- Опционально работа с буфером/без
- Опционально наследует Print.h
- Опционально наследует Stream.h

### Совместимость
ATmega328 и подобные из этого поколения

## Содержание
- [Установка](#install)
- [Инициализация](#init)
- [Использование](#usage)
- [Пример](#example)
- [Версии](#versions)
- [Баги и обратная связь](#feedback)

<a id="install"></a>
## Установка
- Библиотеку можно найти по названию **MicroUART** и установить через менеджер библиотек в:
    - Arduino IDE
    - Arduino IDE v2
    - PlatformIO
- [Скачать библиотеку](https://github.com/GyverLibs/MicroUART/archive/refs/heads/main.zip) .zip архивом для ручной установки:
    - Распаковать и положить в *C:\Program Files (x86)\Arduino\libraries* (Windows x64)
    - Распаковать и положить в *C:\Program Files\Arduino\libraries* (Windows x32)
    - Распаковать и положить в *Документы/Arduino/libraries/*
    - (Arduino IDE) автоматическая установка из .zip: *Скетч/Подключить библиотеку/Добавить .ZIP библиотеку…* и указать скачанный архив
- Читай более подробную инструкцию по установке библиотек [здесь](https://alexgyver.ru/arduino-first/#%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%B1%D0%B8%D0%B1%D0%BB%D0%B8%D0%BE%D1%82%D0%B5%D0%BA)

<a id="init"></a>
## Инициализация
```cpp
MicroUART uart;
```

<a id="usage"></a>
## Использование
```cpp
void MU_serialEvent();  // вызывается в прерывании при приёме байта (см. пример)
Остальные методы - как у Serial

// дефайны настроек. Прописывать ПЕРЕД подключением библиотеки
#define MU_STREAM     // подключить Stream.h (readString, readBytes...)
#define MU_PRINT      // подключить Print.h (print, println)
#define MU_TX_BUF 64  // буфер отправки. По умолч. 8. Можно отключить (0)
#define MU_RX_BUF 64  // буфер приёма. По умолч. 8. Можно отключить (0)
```

<a id="example"></a>
## Пример
Остальные примеры смотри в **examples**!
```cpp
//#define MU_STREAM     // подключить Stream.h (readString, readBytes...)
#define MU_PRINT      // подключить Print.h (print, println)
//#define MU_TX_BUF 64  // буфер отправки. По умолч. 8. Можно отключить (0)
//#define MU_RX_BUF 64  // буфер приёма. По умолч. 8. Можно отключить (0)

#include <MicroUART.h>
MicroUART uart;

void setup() {
  uart.begin(9600);
  pinMode(13, 1);
}

void loop() {
  while (uart.available()) uart.write(uart.read());
  uart.println("123456789");
  delay(1000);
}

// вызывается в прерывании при приёме байта
void MU_serialEvent() {
  static bool val = 0;
  digitalWrite(13, val = !val);
  //uart.write(uart.read());
}
```

<a id="versions"></a>
## Версии
- v1.0

