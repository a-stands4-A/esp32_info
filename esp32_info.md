SoC - мозги и сердце IoT
-
[1](https://auroraevernet.ru/articles/soc-sistema-na-kristalle-ustrojstvo-osobennosti-otlichie-ot-cpu/)

SoC (англ. System on a Chip) - в русской аббревиатуре СнК – система на кристалле – это автономный неразборный 
чип (электронная схема), выполняющий определённую функцию. Данная система может принимать и обрабатывать цифровые, 
аналоговые, радиосигналы или работать в аналого-цифровом режиме, объединив на кристалле процессор (или несколько), 
устройство ввода-вывода, блок оперативной и долговременной памяти. 

SoC - это CPU с "обвесами". Помимо вычислительного блока, в котором может быть несколько ядер, SoC включает в себя, в зависимости от наполнения:
 - блок отрисовки графики;
 - протоколы (интерфейсы) для связи с внешними устройствами;
 - оперативную и постоянную память;
 - модема для подключения к беспроводным системам;
 - аналого-цифровые преобразователи;
 - цифро-аналоговые преобразователи;
 - таймеры, счётчики;
 - источников опорной частоты;
 - регуляторов напряжения;
 - системные контролёры:
   - северный мост (внутреннее взаимодействие);
   - южный мост (внешнее взаимодействие);

---

ESP - аналог Arduino, Raspberry Pico
-
[params](https://docs.espressif.com/projects/esp-idf/en/release-v5.0/esp32/hw-reference/chip-series-comparison.html)
[2](https://narodstream.ru/esp32-urok-36-rmt-rabota-s-ik-pultom/)

Для начала определим, о чем именно говорится в datasheet`ах:

|                     Param                      |                                 Description                                  |
|:----------------------------------------------:|:----------------------------------------------------------------------------:|
|                      Core                      |                             Вычислительный блок                              |
|          Wi-Fi protocols, Bluetooth®           |                Модемы для подключения к беспроводным системам                |
|               Typical frequency                |    Стандартная частота работы (влияет на производительность и потребление    |
|                      SRAM                      |                 Оперативная память (энергозависимая) \[ОЗУ\]                 |
|                      ROM                       |       Постоянная память (энергонезависимая, для загрузки BIOS) \[ПЗУ\]       |
|                 Embedded flash                 |       Флеш-память (EEPROM) \[ максимальный объем флешки в виде чипа \]       |
|                 External flash                 |              Возможность увеличения объема ОЗУ внешними чипами               |
|                     Cache                      |                                 Кеширование                                  |
|                      ADC                       |                    Аналого-цифровые преобразователи (АЦП)                    |
|                      DAC                       |                    Цифро-аналоговые преобразователи (ЦАП)                    |
|                     Timers                     |                                   Таймеры                                    |
|               Temperature sensor               |                        Наличие температурного сенсора                        |
|                  Touch sensor                  |                             Датчик прикосновения                             |
|                  Hall sensor                   |                     Наличие датчика Холла (магнитометр)                      |
|      GPIO (General-purpose input/output)       |       Пины, которые можно запрограммировать на ввод и вывод информации       |
|                      SPI                       |                Количество настраиваемых линий интерфейса SPI                 |
|                 LCD interface                  |                       Возможность вывода на LCD экраны                       |
|                      UART                      |                Количество настраиваемых линий интерфейса UART                |
|                      I2C                       |                Количество настраиваемых линий интерфейса I2C                 |
|                      I2S                       |                Количество настраиваемых линий интерфейса I2S                 |
|                Camera interface                |                         Возможность работы с камерой                         |
|           DMA (Direct memory access)           | Возможность обмена данными между SoC и памятью без участия  CPU компа (???)  |
|              RMT (Remote Control)              |    Возможность применения инфракрасных сигналов дистанционного управления    |
|                 Pulse counter                  |               Возможность подсчета изменения значения сигнала                |
|                    LED PWM                     |                   Возможность ШИМ модуляции для освещения                    |
|                     MCPWM                      |                              Какой-то ШИМ (???)                              |
|                    USB OTG                     |         Возможность работать как USB устройство (мышь, клава, проч)          |
| TWAI® controller (compatible with ISO 11898-1) | Возможность применения протокола для автомобильных и промышленных приложений |
|          SD/SDIO/MMC host controller           |                   Возможность работать с картами памяти SD                   |
|             SDIO slave controller              |          Возможность работать с расширенной формой SD-карты (SDIO)           |
|                  Ethernet MAC                  |                Возможность работать с MAC-адресами (интернет)                |
|                      ULP                       |      Наличие сопроцессора для работы с датчиками в режиме глубокого сна      |
|                  Secure boot                   |                        Защита от взломов при запуске                         |
|                Flash encryption                |                           Криптография флеш памяти                           |
|                      OTP                       |                       Размер одноразового пароля (???)                       |
|                      AES                       |                        Поддержка стандарта шифрования                        |
|                      HASH                      |                            Поддержка хеширования                             |
|                      RSA                       |                    Поддержка криптографического ключа RSA                    |
|        RNG (Random Number Generation )         |             Возможность генерации действительно случайных чисел              |
|                      HMAC                      |              Возможность аутентификации при помощи хеш функции               |
|               Digital signature                |                 Возможность подписи сообщений при помощи RSA                 |
|                      XTS                       |                        Возможность шифрования файлов                         |
|   Deep-sleep (ULP sensor-monitored pattern)    |                    Токопотребление в режиме глубокого сна                    |

---
Плата разработчика (отладочная плата) (devkit)
-
Вычислительный блок (микросхема) с "обвесами" устанавливается на миниатюрную печатную плату => получается SoC (модуль).
Модуль (SoC) паяется к печатной плате, позволяющей использовать возможности SoC => Готовый devkit.

[Состав платы разработчика ESP32](https://docs.espressif.com/projects/esp-idf/en/v5.1.1/esp32/hw-reference/esp32/get-started-devkitc.html):
- SoC (с распаянной PCB-антенной WiFi/Bluetooth или без);
- Программатор (CP21XX, CH34XX) - микросхема для записи инструкций в память вычислительного блока;
- Индикаторы питания, отладочные светодиоды;
- Регулятор напряжения - для питания от USB и пина питания 5V (LDO DC-DC 5V to 3.3V);
- Кнопки сброса (Reset) и кнопка режима загрузки прошивки (Boot);
- [Порт `USB Micro-B` или `USB Type-С`;](https://webznam.ru/blog/porty_usb_razlichnykh_tipov/2022-10-29-2174)
- Выводы (пины) для подключения периферии, датчиков.
---
[Товарный ряд ESP](https://www.espressif.com/en/products/socs)
-

| SoC Series | RISC-V |              Core              | Bits | Frequency, MHz | SRAM, KB | ROM, KB |  WiFi   |    Bluetooth     | Zigbee |                           Additional                           |
|:----------:|:------:|:------------------------------:|:----:|:--------------:|:--------:|:-------:|:-------:|:----------------:|:------:|:--------------------------------------------------------------:|
|     S3     | False  |  Xtensa® 32-bit LX7 Dual-core  |  32  |   up to 240    |   512    |   384   | 2.4 GHz | Bluetooth 5 (LE) | False  | Vector instructions, <br/>connection to flash and external RAM |
|     S2     | False  | Xtensa® 32-bit LX7 Single-Core |  32  |   up to 240    |   320    |   128   | 2.4 GHz |      False       | False  |                  Ultra-low-power performance                   |
|     C6     |  True  |   Single-core microprocessor   |  32  |   up to 160    |   512    |   320   | 2.4 GHz | Bluetooth 5 (LE) |  True  |                   Works with external flash                    |
|     C3     |  True  |   Single-core microprocessor   |  32  |   up to 160    |   400    |   384   | 2.4 GHz | Bluetooth 5 (LE) | False  |                   Allow connection to flash                    |
|     C2     |  True  |   Single-core microprocessor   |  32  |   up to 120    |   272    |   576   | 2.4 GHz | Bluetooth 5 (LE) | False  |                      16 KB for cache SRAM                      |
|     H2     |  True  |   Single-core microprocessor   |  32  |    up to 96    |   320    |   128   |  False  | Bluetooth 5 (LE) |  True  |                         4 KB LP Memory                         |
---
RISC-V 
-

[1](http://digitrode.ru/computing-devices/mcu_cpu/3414-chto-iz-sebya-predstavlyaet-arhitektura-risc-v-i-pochemu-ona-mozhet-byt-zamenoy-arm.html)
&nbsp;
[2](https://www.osp.ru/os/2020/02/13055471)
&nbsp;
[3](https://tproger.ru/articles/processors-architectures-review)

Архитектура (микро-)процессора - или набор команд для работы над битами или подходы к физической реализации данного набора (как именно гоняют электроны в ячейках памяти (регистрах)).

RISC-V - команды проще, короче, быстрее в выполнении, но их относительно мало и они не оптимизированы под конкретные задачи, особенности физической реализации.

---
Важные параметры для выбора SoC
-


   

---

