# STM32 DHT11 Temperature and Humidity Monitoring

## Project Overview

This project measures real-time temperature and humidity using a DHT11 sensor interfaced with the STM32 NUCLEO-F446RE development board.

The DHT11 sensor collects temperature and humidity data from the surrounding environment and sends it to the STM32 microcontroller. The STM32 processes the sensor readings and transmits the measured values to a computer through USART2 UART serial communication at 115200 baud.

Windows PowerShell is used to display the temperature and humidity readings in real time. The onboard LD2 LED blinks whenever a valid sensor reading is received.

## Hardware and Software Requirements

### Hardware

- STM32 NUCLEO-F446RE development board
- DHT11 temperature and humidity sensor
- Breadboard
- Jumper wires
- USB cable for programming and serial communication

### Software

- STM32CubeMX
- Keil µVision
- Windows PowerShell
- ST-LINK Virtual COM Port support

## Pin Configuration

| Component / Signal | STM32 NUCLEO-F446RE |
|---|---|
| DHT11 DATA | PA0 |
| DHT11 VCC | 3.3 V or supported module supply |
| DHT11 GND | GND |
| Onboard LD2 LED | PA5 |
| USART2 TX | PA2 |
| USART2 RX | PA3 |
| Serial Baud Rate | 115200 |

**Note:** Ensure the DHT11 DATA line has an appropriate pull-up resistor. Check the power requirements of your particular DHT11 sensor or module before connecting it.

## Project Implementation

### 1. Pinout and GPIO Configuration

The DHT11 DATA pin is connected to PA0 of the STM32 NUCLEO-F446RE board. The GPIO pin is configured to communicate with the sensor. PA5 is configured as an output to control the onboard LD2 LED.

![DHT11 Pinout and Configuration](DHT11_pinout&configuartion_window_image.jpeg)

### 2. STM32CubeMX Project Manager

STM32CubeMX is used to configure the required GPIO and USART2 peripherals. The project is configured to generate Embedded C code for the Keil MDK-ARM toolchain.

![DHT11 Project Manager Configuration](DHT11_projectmanager_window_image.jpeg)

### 3. Keil µVision Project Window

The generated STM32 project is opened in Keil µVision. The Embedded C firmware is developed, compiled, and built to interface with the DHT11 sensor, process its readings, and transmit the data through UART.

![Keil µVision Project Window](DHT11_keil-uVision_project_window_image.jpeg)

### 4. Temperature and Humidity Output in PowerShell

The DHT11 sensor measures the surrounding temperature and relative humidity. The STM32 microcontroller reads the sensor data and transmits the measured values through USART2 UART communication.

Windows PowerShell receives and displays the data in the terminal.

Example output:

```text
DHT11 reading started
Temperature: 28 C   Humidity: 65 %
Temperature: 29 C   Humidity: 64 %
```

*Note: These are example readings. Actual temperature and humidity values depend on the surrounding environment.*

#### PowerShell Command

The following PowerShell commands open the STM32 board's serial port and continuously display the incoming data.

```powershell
$p = New-Object System.IO.Ports.SerialPort COM26,115200,None,8,one
$p.Open()
while ($true) { $p.ReadLine() }
```

**Command explanation:**

- `COM26` — The serial COM port assigned to the STM32 board. Replace it with your actual port.
- `115200` — UART baud rate.
- `None` — No parity.
- `8` — Eight data bits.
- `one` — One stop bit.
- `$p.ReadLine()` — Reads incoming serial data one line at a time.

**Important:** Close other serial monitors using the same COM port before running the command. The UART settings in the STM32 firmware must match the PowerShell serial configuration.

![DHT11 PowerShell Output](DHT11_powershell_window_output_image.jpeg)

### 5. Hardware Setup and Output

The DHT11 sensor is connected to the STM32 NUCLEO-F446RE board using a breadboard and jumper wires. The board is powered and programmed through USB.

The measured temperature and humidity values are displayed in the PowerShell window. The onboard LD2 LED blinks whenever the firmware receives a valid sensor reading.

![DHT11 Hardware Setup and Output](DHT11_hardware_output_image.jpeg)

## Key Concepts Learned

- Temperature and relative humidity measurement using DHT11
- Sensor interfacing with STM32
- GPIO configuration using STM32CubeMX
- Embedded C programming using STM32 HAL
- Timing-based digital sensor communication
- USART2 UART serial communication
- Displaying sensor readings using Windows PowerShell
- Onboard LED control using GPIO
- Sensor communication debugging

## Conclusion

This project demonstrates real-time temperature and humidity measurement using the DHT11 sensor and STM32 NUCLEO-F446RE development board. The measured values are transmitted through UART and displayed in Windows PowerShell. The project provides practical experience in sensor interfacing, Embedded C programming, GPIO configuration, and serial communication.

## Future Improvements

- Add an LCD or OLED display to show readings without a computer.
- Save temperature and humidity measurements to a file.
- Add alerts when temperature or humidity crosses a predefined threshold.
- Use hardware timers to schedule periodic sensor measurements.
