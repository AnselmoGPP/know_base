# Embedded software with C


## Table of Contents

* [References](#references)
* [Embedded systems](#embedded-systems)
* [C programming](#c-programming)
* [ARM Cortex (STM32) fundamentals: Building embedded systems](#arm-cortex-stm32-fundamentals-building-embedded-systems)
* [ARM Cortex (STM32) deep dive: Mastering embedded systems](#arm-cortex-stm32-deep-dive-mastering-embedded-systems)


## References

- EDUCBA (n.d.) [_**Embedded software with C specialization**_](https://www.coursera.org/specializations/embedded-software-development-with-c).


## Embedded systems

### Introduction

**Embedded**: Refers to something that is joined (or combined) to another entity.

**Microcontroller unit** (MCU): Small computer on a single integrated circuit. It contains: processor core/s, memory, and programmable input/output peripherals. Example: mouse of a PC, or camera of a mobile phone.

**Embedded system** (ES): Computer hardware system with software embedded in it. Microcontroller or microprocessor based system that is intended to carry out a certain function (like a fire alarm that only detects smoke). Small application which is combined to create into another entity. They power many devices (smarthphones, household appliances, industrial machinery, automotive systems…).

- **Types**:

  - **Standalone unit**: It operates independently, executing predefined tasks without external communication.
  - **Networked/embedded system**: Component of a larger system. It connects to other devices or networks to exchange data, enabling functionalities like remote monitoring and control.

- **Main components**:

  - **Hardware**: Like microcontrollers or microprocessors.
  - **Application**: Available for the hardware.
  - **RTOS** (Real Time Operating System): Manages the application software and offers a way to schedule and allow the processor to execute a process by adhering to a latency control plan. However, some ESs may operate without OS.

- **Characteristics**: 

  - **Single-functioned**: It typically carries out a single, specialized task once (pager, camera…).
  - **Tightly confined/coupled** (as oppossed to loose coupled): Design metrics are subject to very strict restrictions. Design metric quantify the attributes of an implementation, including its price, size, power, memory, energy consumption, and effectiveness. It needs to be small enough to fit on a single chip, operate quickly enough to process data instantly, and use as little power as possible to prolong battery life.
  - **Reactive and Real-time**: It often has to compute specific outcomes instantly in real-time and constantly respond to cahnges in their surroundings (like an automobile cruise control unit).

- **Advantages**: 

  - Simple to tailor
  - Minimal power use
  - Low price
  - Improved outputs
  
- **Disadvantages**:

  - High level of development
  - Longer time to market

### Embedded C programming

**C language**: It's preferred for embedded systems due to its efficiency, low-level access to hardware, extensive toolchain support, syntax (it allows for precise control over memory and hardware resources), and close-to-the-hardware nature.

**Key concepts**:

- **Memory management**: ESs often have limited memory resources. C allows efficient memory management (pointers, dynamic memory allocation…), but requires careful memory management to avoid issues (memory leaks, buffer overflows…) which can lead to system instability or security vulnerabilities.
- **Peripheral access**: ESs interact with various peripherals (sensors, actuators, communication interfaces…). C allows direct access to hardware registers (enabling precise control over peripherals) through memory-mapped I/O, where hardware registers are accessed as if they were regular memory locations.
- **Real-time programming**: ESs often require real-time responsiveness, where tasks must be completed within strict timing constraints. C offers deterministic behavior and low-level control (interrupt handling, task scheduling…). 
- **Portability**: ESs are often designed for specific platforms, but portability remains essential for code reuse and maintainability. C's standardized syntax and well-defined behavior makes it relatively portable across different architectures and compilers, but developers must be mindful of platform-specific considerations when writing portable code.

**Development tools**:

- **IDEs** (Integrated Development Environments) (like Eclipse, Keil µVision, Visual Studio Code, STM32CubeIDE): Comprehensive environment for writing, compiling, debugging, and deploying embedded C code.
- **Compilers** (like GCC, Clang, IAR Embedded Workbench): Translate C code into machine-readable instructions for the target platform.
- **Debuggers** (like GDB and JTAG-based tools): Help diagnose and fix issues in embedded software.
- **Simulators**: Allow testing code in a virtual environment, reducing the need for physical hardware during development.

**Programming best practices**: They ensure the reliability, efficiency, and maintainability of embedded systems code.

- **Modularity**: Divide code into modular components with well-defined interfaces to promote code reuse and facilitate maintenance.
- **Optimization**: Optimize code for performance, size, and power consumption without sacrificing readability or reliability. Profile code to identify bottlenecks and optimize critical sections.
- **Error handling**: Implement robust error handling mechanisms to gracefully recover from unexpected conditions and prevent system failures.
- **Documentation**: Document code thoroughly, including comments, function descriptions, and usage examples, to aid understanding and future modifications.
- **Testing**: Conduct rigorous testing, including unit tests, integration tests, and system tests, to verify functionality, performance, and reliability under various conditions.

### Components and structure

**Hardware components**:

- **Power supply**: ESs require a stable and reliable power supply to operate correctly. The system will either have one, or will draw power from the larger host system. Power management circuits regulate voltage levels, manage power consumption, and provide protection against electrical anomalies (overvoltage, undervoltage, power surges…).
- **Processor**: Executes program instructions and controls system operations. There're different types (general processor, digital sensor processor, media processor, application specific processor, microprocessor, microcontroller, embedded processor, and application specific instruction processor).
  - **Microcontroller (MCU)**: Integrated circuits containing a CPU, memory, I/O peripherals, and other essential components on a single chip. It allows compactness and low power consumption.
  - **Microprocessor (MPU)**: General-purpose CPUs used in more complex systems with higher computational requirements.
- **Clock source** (Timers & Counters): Generates timing signals required for synchronizing the operations of the microcontroller or microprocessor and other system components. It ensures that tasks are executed at precise intervals (like making a led blink) and enables the system to meet timing requirements (especially in real-time applications).
- **Memory**: ESs use various types of memory to store program code, data, and system configurations. This includes:
  - ROM (Read-Only Memory): For storing firmware or boot code.
  - RAM (Random-Access Memory): For runtime data storage.
  - EEPROM (Electrically Erasable Programmable Read-Only Memory): Non-volatile memory for storing persistent data that survives power cycles).
  - Others: Cache, PROM, Flash, etc.
- **Peripherals** (Communication port): External devices/components connected to the microcontroller/microprocessor to enable input, output, and ocmmunication with the external world. Common peripherals:
  - ADC (Analog-to-Digital converter)
  - DAC (Digital-to-analog converter)
  - Serial communication interfaces (UART, SPI, I2C)
  - GPIO (General-Purpose Input/Output) pins
  - Sensors & Actuators
  - Timers
  - Others: CAN, RS232, RS423, RS485, USB, Ethernet, parallel port, etc.

**Development components**:

- **Editor**: Tool for writing, editing, and visualizing code.
- **Emulator**: Enables to use a feature of a system.
- **Assembler**
- **Compiler**
- **Linker**
- **Compiler**

**Software components**:

- **Firmware**: Low-level software stored in ROM or Flash memory. Responsible for booting the system and initializing hardware peripherals. It typically includes a bootloader for loading the main application code from external storage or secondary memory into RAM.
- **Device drivers**: Software modules that interface with hardware peripherals, abstracting their functionality and providing a standardized interface for higher-level software layers. They allow the OS system or application software to communicate with the hardware components without needing to understand their intricate details.
- **Operative system (OS)**: While some ESs operate without OS, may use a RTOS (Real-Time Operating System) or lightweight kernels to manage system resources, schedule tasks, and provide services like inter-process communication, memory management, and device drivers. RTOSs offer deterministic behavior, ensuring timely execution of critical tasks in real-time applications.
- **Application software**: Programs and algorithms specific to the ES's functionality. It interacts with device drivers and OS services to perform tasks (data processing, control algorithms, UI management, communication with external devices or networks…).

**Software structure of an ES**:

- **Hardware Abstraction Layer (HAL)**: Standardized interface between the hardware and software layers, abstracting hardware-specific details and enabling portability across different hardware platforms. Typical components: device drivers, interrupt handlers, low-level peripheral access function, etc.
- **OS kernel**: Core component responsible for managing system resources, scheduling tasks, and providing essential services to applications. Real-time kernels prioritize tasks based on their deadlines and execution requirements, ensuring timely responses to critical events.
- **Middleware and Libraries**: They provide higher-level functionality and services to application software. They may include communication protocols 8TCP/IP, MQTT, etc.), file systems, GUI frameworks, signal processing algorithms, data encryption/decryption routines, …).
- **Application layer**: Software components responsible for implementing the system's specific funtionality (including algorithms, control logic, UIs…). It interacts with lower-level layers (HAL, kernel, middleware) through interfaces provided by them.

**Hardware structure of an ES**:

- **Sensor**: Measures a physical quantity and converts to an electrical signal, which can be read by an observer or any electronic instrument. It can store the quantity in memory or pass it to the A-D converter.
- **A-D converter (ADC)**: Converts Analog data into Digital data (the processor reads digital data). It can store the quantity in memory or pass it to the processor & ASIC.
- **Processor & ASIC** (Application-Specific Integrated Circuit): Processes the data and stores the output data in memory.
- **D-A converter (DAC)**: Converts the Digital data into Analog data.
- **Actuator**: Converts the analog data (from a microcontroller) into physical actions (motion, heat, force…).
- **Memory**: Used to store data. Memory is often used by the sensor, A-D converter, and processor & ASIC.

### Architecture

Architecture dictates how the system function, processes data, and interacts with the environment. There're 2 common embedded systems architectures: MCU and MPU.

**Microcontroller (MCU) architecture**: MCUs are integrated circuits (ICs) that combine a microprocessor core with other components on a single chip: cpu core, memory (programable ROM, SRAM), input/output peripherals, etc. They provide compactness, low power consumption, and cost-effectiveness, but have limited resources. Some key characteristics are:

- **Integrated peripherals**: MCUs typically incorporate various on-chip peripherals, which reduce the need of external components, minimize board space, and simplify design. Peripheral examples: timers, serial communication interfaces (UART, SPI, I2C), ADCs, DACs, general-purpose input/output (GPIO) pins.
- **Low power consumption**: MCUs are optimized for low power consumption, featuring sleep modes, power management circuits, and low-voltage operation to minimize energy usage and extend battery life.
- **Limited resources**: MCUs often have limited processing power, memory, and peripheral capabilities compared to MPUs, so they are suitable for simpler embedded applications with modest computational requirements (home appliances, automotive control systems, consumer electronics…).
- **Application-specific solutions**: MCUs are available in a wide range of configurations tailored to specific application requirements. Different products have varying combinations of CPU cores, memory sizes, peripheral sets, and packaging options, allowing developers to choose the most suitable MCU for their application.
- **Real-time operation**: Many MCUs are designed for real-time operations, where tasks must be executed within strict timing constraints. They often feature built-in hardware timers, interrupts, and dedicated hardware for signal processing, enabling precise timing control and deterministic behavior required in real-time applications.

**Microprocessor (MPU) architecture**: MPUs are standalone CPUs designed for general-purpose computing tasks. They require external support components (memory, I/O interfaces, peripheral controllers…) to form a complete ES. Different types based on their data bit width: 32-bit, 16-bit, 8-bit. They offer superior performance and flexibility, but higher cost and complexity. Some key characteristics are:

- **Modularity and flexibility**: MPUs offer great flexibility and scalability compared to MCUs. Developers can customize the system (choosing from a wide range of CPUs, memory types, and peripheral interfaces) according to specific requirements. This allows designing ESs with varying levels of performance, memory capacity, and connectivity options.
- **External peripheral interface**: MPUs rely on external peripheral controllers to interface with devices (sensors, actuators, displays, communication interfaces…), which provides flexibility in selecting appropriate peripherals and allows for expansion or upgrades.
- **High performance**: MPUs typically feature more powerful CPU cores with higher clock speeds, larger caches, and advanced intruction sets (ISs) compared to MCUs. This makes them suitable for demanding embedded applications (multimedia processing, networking, industrial automation, automotive infotainment systems…).
- **Operating system support**: MPUs are often used in ESs requiring features (multitasking, memory protection, advanced software…) provided by some OSs (Linux, Android, Windows Embedded…). These OSs allow building complex applications with rich UIs, networking capabilities, and support for third-party software libraries.
- **Cost and complexity**: MPUs tend to be more expensive and complex to design compared to MCUs. External support components (memory, power management circuits, peripheral controllers…) add to the system cost and design complexity, and the use of OSs introduces overhead (more memory footprint, boot time, and system resource utilization).

**Choosing between MCU and MPU architecture**: It depend on various factors:

- **Performance requirements**: MPUs are suitable for applications demanding high computational performance (multimetida processing, multitasking capabilities…).
- **Cost constraints**: MCU are more cost-effective, but offer limited processing power and peripherals.
- **Power consumption**: MCUs are more energy-efficient, making them suitable for applications requiring low power consumption or battery operation.
- **System complexity**: The complexity of the application (number and type of peripherals, memory requirements, software complexity…) influences the choice of architecture.
- **Development time**: The availability of development tools, software libraries, and expertise in MCU or MPU programming may impact the choice of architecture.

### Peripheral devices

**Peripheral devices** allow ESs communicate with the external, interface with sensors and actuators, and provide various I/O functionalities. They extended ES's capabilities beyond its CPU. They serve as interfaces between the ES and its environment, allowing it to interact with external devices, humans, and other systems. They enable data acquisition, control, communication, and feedback mechanisms essential for the ES's operation. Without them, ESs would be isolated and unable to perform their intended functions effectively.

**Examples** of peripherals:

- Serial Communication Interfaces (SCI) (RS232, RS-422, RS-485…)
- Synchronous Serial Communication Interfaces (SSCI) (I2C, SPI, SSC, ESSI…)
- Universal Serial Bus (USB)
- Multi Media Cards (SD cards, Compact Flash…)
- Networks (Ethernet, LonWorks…)
- Fieldbuses (CAN-Bus, LIN-Bus, PROFIBUS…)
- Imers (PLLs, Capture/Compare, Time Processing Units…)
- General Purpose I/O (GPIO) (i.e., Discrete IO)
- ADC/DAC (converters)
- Debugging (JTAG, ISP, ICSP, BDM Port, BI TP, DP9 ports…)

**Types** of peripheral devices (based on their functionality and purpose):

- **Input devices**: They capture data from the external environment and provide it to the ES for processing. Examples:

  - **Sensors**: They detect physical parameters (temperature, pressure, humidity, light intensity, motion, proximity…) and convert these analog signals into digital data that the ES can process. 
  - **Switches and Buttons**: They provide binary input signals to the ES. Commonly used for user interaction, control, and configuration.
  - **Keypads and Keyboards**: Matrix of keys or buttons. They enable alphanumeric input for user interaction and data entry. 

- **Output devices**: They display information, provide feedback, or control external devices. Examples:

  - **Actuators**: They convert electrical signals into mechanical motions or physical action (like motors, solenoids, relays, and valves used for controlling movement, positioning, or switching).
  - **Displays**: They present visual information to users (text, graphics, images…). Examples: LCDs, LED, OLED, e-ink displays, etc.
  - **Audio devices**: They produce sound output for multimedia applications, alarms, notifications, and user feedback. Examples: speakers, buzzers, audio transducers, etc.

- **Communication interfaces**: They facilitate data exchange between the ES and other systems (external devices, networks…). Examples:

  - **Serial Communication Interfaces**: Asynchronous or synchronous serial communication. Examples: UART (Universal Asynchronous Receiver-Transmitter), SPI (Serial Peripheral Interface), I2C (Inter-Integrated Circuit), etc.
  - **Ethernet and Wi-Fi modules**: Network connectivity (LAN or Internet). They support protocols for data transmission and network communication (like TCP/IP).
  - **Wireless Communication Modules**: Short-range or long-range wireless connectivity (Bluetooth, Zigbee, LoRa, RFID…). Use case examples: remote control, wireless sensing, asset tracking, etc.

- **Memory devices**: They store program code, data, configuration settings, and other information. Examples:

  - **Flash memory**: Non-volatile memory for storing program code (firmware), application data, and system configurations. Retains data even when power is removed.
  - **EEPROM** (Electrically Erasable Programmable Read-Only Memory): Non-volatile memory that can be electrically erased and reprogrammed. Commonly used for small amounts of data (calibration values, user settings, device parameters…).

**Functionalities** of peripheral devices:

- **Data acquisition**: Sensors and input devices capture data from the environment (temperature, pressure, motion, user input…) and provide it to the ES for processing and analysis.
- **Control and Actuation**: Output devices and actuators receive control signals from the ES and perform physical actions or generate outputs based on the processed data (like controlling motors, valves, displays, or audio devices).
- **Communication and Networking**: Exchange data with external devices, networks, or other systems. They support various communication protocols for wired and wireless connectivity, facilitating data transmission, remote monitoring, and control.
- **User interaction and Feedback**: Input devices allow users to interact with the ES, provide input commands, and configure settings (switches, buttons, keypads, touchscreen…). Output devices provide feedback, status indications, alerts, and notifications to users (displays, LEDs, audio devices…).
- **Data storage and Retrieval**: Non-volatile storage used for retaining data across power cycles and system resets (program code, application data, configuration settings…).


## C programming

### Introduction

**Embedded systems** are specialized systems created to carry out extremely particular tasks or operations. It consists of both hardware and software (firmware). Three categories: small-sized, medium-sized, advanced.

**C language**: General-purpose language. It's appropriate for desktop applications and system programming (OSs, compilers…). It provides low-level memory access, a limited number of keywords, and a clean syntax. Its development methodology is native platform-based (i.e., it creates platform-specific applications, limited to a single platform).

**Embedded C**: It's a C extension for creating applications for microcontrollers/microprocessors. It provides some expansions (I/O hardware addressing, fixed-point arithmetic operations, accessing address spaces…). It allows working with hardware (I/O devices, sensors…). It's used for programming everyday electronics (air conditioners, printers, cell phones…). It uses fewer resources during execution than high-level languages (like assembly). It provides extra data types and keywords. Special function registers in memory are addressed using specific datatypes (like `sbit` and `sfr`). There're different embedded C compilers (Keil, SPJ, Embedded GNU C, …).

[**STM32cubeIDE**](https://www.st.com/en/development-tools/stm32cubeide.html#section-get-software-table): C/C++ IDE for STM32 code development. Download it and install it (including the J-Link and ST-LINK drivers).

**Embedded C basics**:

- **Comments**:
  - Single line comment: `// comment`
  - Multiline comment: `/* comment */`
- **Processor directives**: `#include <stdio.h>` (include code from a header)
- **Port configurations**: We need to configure the port number before writing code.
- **Global variables**: Defined outside any function (`unsigned int a = 10;`).
  - File scope: Default. However, the variable can be "grabbed" if another file uses `extern`.
  - Program scope: Use `extern`.
  - Restricted global scope: Use `static`. It's like File scope, but cannot be "grabbed" with `extern`.
- **Core function/Main function**: `int main() { }`
- **Variable types**: `int`, `double`, `stp`, `srp`, etc.
- **Program logic**: flow control, etc.

**Basic syntax**:

- C language:

```
#include<stdio.h>
void main() { }
```

- Embedded C:

```
#include<reg51.h>
Main() { }
```

### Operators

**Variables**: Container used to store data values (numbers, characters…). There're different types:

- Declaration structure: `<dataType> <varName> = <value>;`
- `int num1 = -25;`
- `float num2 = -20.01;`
- `char letter = 'a';`
- `char string[] = "abc";`

**Operators**: Special characters or symbols used to carry out different operations on operands (expressions, constants, variables…). They allow manipulating data and making computations. Different types:

- Assignment: `=`, `+=`, `-=`, `/=`, `%=`
- Arithmetic: `+`, `-`, `*`, `/`, `%`, `++`, `--`
- Relational: `==`, `!=`, `>`, `<`, `>=`, `<=`
- Logical: `&&`, `||`, `!`
- Bitwise: `&`, `|`, `^`, `~`, `<<`, `>>`
- Size of: `sizeof(dataType/variable)` (number of bytes)
- Conditional: `condition ? trueExp : falseExp`
- Comma: Separates consecutive operations.

**Binary numbers**: To convert a decimal number to binary, activate the bits whose power-of-two values add up to that decimal number. Example:

|     | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 0   | 0   | 0   | 0   | 0   | 0   | 0   | 0   | 0   |
| 5   | 0   | 0   | 0   | 0   | 0   | 1   | 0   | 1   |
| 25  | 0   | 0   | 0   | 1   | 1   | 0   | 0   | 1   |
| 100 | 0   | 1   | 1   | 0   | 0   | 1   | 0   | 0   |
| 128 | 1   | 0   | 0   | 0   | 0   | 0   | 0   | 0   |

**Bitwise operations**: `&` (AND), `|` (OR), `^` (XOR), `~` (NOT), `<<` (left shift), `>>` (right shift)

| a | b |`&`|`|`|`^`|
|:-:|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 0 |

**Comma operator**:

```
int a;
int b = (a = 2, a + 6);   // b == 8
```

```
int a = 10, b = 20, c = 30;
printf("%d, %d, %d", a, b, c);   // 10 20 30
```

```
int a = 10;
printf("%d %d", a, a++);   // undefined behavior
```

### Storage classes

| Storage class | Default storage | Lifetime | Initial value | Scope |
|:-------------:|:---------------:|:--------:|:-------------:|:-----:|
| Auto          | Memory (RAM)    | Within block/function where it's declared | Garbage value | Local |
| Register      | CPU registers   | Within block/function where it's declared | Garbage value | Local |
| Static        | Memory (RAM)    | Throughout program execution | 0 (for functions) & functions remain in memory | Local (variables) & global (functions) |
| Extern        | Memory (RAM)    | Throughout program execution | Depends on where the variable or function is defined | Global |







## ARM Cortex (STM32) fundamentals: Building embedded systems
## ARM Cortex (STM32) deep dive: Mastering embedded systems
