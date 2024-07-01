# Badge Connect library (Binary version)

This library is designed to provide a simple API in order to communicate electronic badges over a WiFi mesh network. It works using the [ESPNOW protocol](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-reference/network/esp_now.html) developed by Espressif Systems.

## Features

- Send and receive messages between badges (messages can be of any data type)
- Set the badge's type (e.g. "BSides", "DragonJAR", "Ekoparty", and "BugCON")
- Get the badge's type

## Requirements

- At least two ESP32 development boards
- ESP-IDF installed in your computer
- `make` installed in your computer (optional)

## Installation

Add badge_connect_bin as a dependency in the `idf_component.yml` file of your badge project.

```yml
  badge_connect:
    git: https://github.com/ElectronicCats/badge_connect_bin
    version: "1.0.0"
```

> Replace the version with the latest release.

## Usage

1. Add the root of this repository to the component search path of your `CMakeLists.txt` file in your project.

```cmake
set(EXTRA_COMPONENT_DIRS "/path/to/badge_connect_src")
```

> Check how this is made in the examples.

2. Include the library in your source code.

```c
#include "badge_connect.h"
```

3. Initialize the library in your code.

```c
badge_connect_init();
```

4. Implement the callback function that will be called when a message is received.

```c
void receive_data_cb(badge_connect_recv_msg_t* msg) {
    // Do something with the received message
}
```

5. Register the callback function.

```c
badge_connect_register_recv_cb(receive_data_cb);
```

6. Set the badge's type, choose one of the following:

```c
badge_connect_set_bsides_badge();
badge_connect_set_dragonjar_badge();
badge_connect_set_ekoparty_badge();
badge_connect_set_bugcon_badge();
```

7. Send a message to another badge.

```c
char* data = "Hello, world!";
badge_connect_send(data, strlen(data));
```

8. Compile and flash!

## Examples

There is a folder called `examples` in this repository, you can use the `Makefile` in each example to compile and flash the firmware.

1. Get `idf.py` to your terminal session, if you followed the Espressif IDF installation guide, use `get_idf`.

```bash
get_idf
```

2. Go to the example folder you want to compile. For example, the `send_int` one.

```bash
cd examples/send_int
```

3. Set the board type you are using, skip if you are using an `ESP32`. For example, `ESP32-C6`.

```bash
idf.py set-target esp32c6
```

4. Set the serial port where the board is connected. For example, `/dev/ttyUSB0`.

```bash
export PORT=/dev/ttyUSB0
```

5. Compile, flash, and monitor the output.

```bash
make all
```

## License

Electronic Cats invests time and resources in providing this open-source design, please support Electronic Cats and open-source hardware by purchasing products from Electronic Cats!

Designed by Electronic Cats.

This library is released under a GNU AGPL v3.0 license. See the [LICENSE](LICENSE) file for more information.

Electronic Cats is a registered trademark, please do not use if you sell these PCBs.

June 2024
