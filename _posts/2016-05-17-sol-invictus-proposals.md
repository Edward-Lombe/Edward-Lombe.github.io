# Sol Invictus Tech Proposals

---

## 1 - Onboard systems

### 1.1 - Overview

### 1.2 - Main goals

- Design an interface for the pilot that effectivley controls and monitors the
  status of the solar car
  - Control of the vehicle.
    - It is possible that an electronicaly controlled accelerator and steering
      system would allow for more precise, efficient control of car.
  - Communications with team car
    - Solar car status
    - Pilot communications
    - Pilot vital readings
      - Heart rate
      - Temperature
  - Monitoring of sensor information
  - Telemetry back to team car with status of vehicle
  - Recording of sensor and telemtry data
    - Will not be able to communicate all data back to team car
    - Or will simply want to preserve the bandwidth to and from the car
      to the most critical and time sensitive information possible
    - Having as rich a datasource as possible means a higher fidelity source of
      data for post performance analysis
- Use open source, off the shelf (OTS) software.
- Pick components that are cheap and readily available.
- As some of the team may be engineers before they are programers, pick
  technology that has a large body of supporting teaching documetation to
  accompany it, so as to make the transistion between the two disciplines as
  smooth and easy as possible.
- Pick relaible, proven software and hardware.
- Pick components for the subsytems that allow rich and easy integration with
  each other. This wil facilitate inter-team communication and will allow for
  more general delegation (one person will be familiar with a technology that
  could span multiple teams

Describe the purpose of the racing and telemetry system.

People who are not extremely experienced will be working on the project.

Therefore we want to opt more towards technologies that have a strong body of
both documentation in terms of using the system and documentation that is
designed to help you learn how the system works.

The main purpose of the systems will be to provide control to the vechicle and
to provide an interface input received by the various sensors. The top level of
this system or the one that will be closest to the driver will be the input and
display. The first part will a screen hooked up to the onboard computer. This
screen could possibly be touch screen as there are 7" touch screens that will
plug into the Raspberry PI. This will alow us to provide a very rich control
interface with the driver. Also, as the computer has USB inputs, standard
keyboards and mice can be used to plug in this system

### 1.3 - Limitations

All software and hardware has limitations imposed on it by both formal
specifications and the greater environment and context in which it is run. This
section aims to elucidate the relationship between these two contexts and the
rationale for deciding on technology that is best suited to its application.

The first and most obvious limitation when it comes to running software on a
solar vehicle is that of power. Power is the main resource of the solar vehicle
and any sane implementation must ensue that its drain must not be significant
enough to affect the performance in any significant manner. One way to
circumvent this would be to have seperate power supplies for the comand and
control systems, though this must be investigated to make sure that the
additional weight and complexity of such a systems would also not adversely
affect the performance of the car. Regardless of which system ends up powering
the the solar vehicles subsystems, it is as important as possible that any
non-critcal, power intensive computation takes place on systems that are not
actually mounted on the car itself.

The second limitation is mass. This limitation is more easily met as for the
past half centurary we have seen computer systems shrink from being behemoths
that take an entire floor to run and operate, to being something that anyone
with adequete means can carry in their pockets. However mass is brought back
into context when considering the total mass of the solar cars that these
systems will be placed into. For example the 'Aurora 101 4th Generation' the
current flagship of 'Aurora Vehicle Association' has a mass of ~130kg without
batteries and a driver, and a mass of ~240kg in racing livery for competitions
such as the world solar challenge. The small mass of these solar vehicles means
that it could be quite easy to create a design which has a mass that makes up a
significant fraction of the cars mass. As the mass of the car will need to be
managed across all subsystems, it is important that this limitation is kept in
mind while considering any potential design for systems to be used onboard.

The third limitation imposed comes from experience, or to be more precise, the
limited amount of it. It is likely that most people who will be designing,
building, and piloting this vehicle will have not previoulsy had any experience
directly related to the processes involved. This is simply due to the fact that
this is the ANU's first entry into the World Solar Challenge. Another experience
related limitation is that there will be limited technical expertise when it
comes to implementing embedded systems and the software development process. As
a result the startup time, defined as the amount of time it takes for one to go
from completely unfamiliar to productive competence with a particular subsytem
or development tool must be kept to a minimum. This will ensue that resources
from teams can be shared in an efficient manner as there is not a large
complexity hurdle that must be passed for one to be able to contribute.

### 1.4 - Components

#### 1.4.1 Rasberry PI 3

For the main control unit a Raspberry PI, as mentioned in the email from
Benjamin Roberts to Alan Babei, would perform well under the limitations
mentioned above. The RPI would meet these criteria well for several reasons. The
first is that the RPI runs an ARM processor. This type of processor is the same
type of chip architecture that is used in both the ubiquitous iOS and Android
powered smart phones. These types of chips are specifically designed for low
power consumption and and energy efficient computation. Most importantly, in the
case of the RPI 3, it now runs on a 64-bit architecture, which means higher
precision calculations and a broader spectrum of support for programs.

The RPI 3 now also contains many common networked capabilities, including
ethernet, both Bluetooth and Bluetooth Low Power standards, and most importantly
built in WiFi. This allows for rich communication to be set up using hardware
that can be bought from any common electronics store, such as WiFi routers, and
protocols that form the basis of the most common forms of electronic
communication on the planet (HTTP, FTP, WebSockets, etc.).

Storage can be provided by a microSD for installation of operating system, as
well as where the source code or compliled binaries for the operation of the
solar vehicle subsystems. For larger more static storage, a PiDrive would be
suitable to store telemetry information for more comprehnsive post performance
analysis. The PiDrive is a 314GB hard disk drive that is specifically optimised
for the RPI, in that it is easily connected and has a lower power profile
compared to conventional HDDs.

The RPI also has a very large aftermarket of accessories and peripherals for
building complex systems. For example, some of the accessories that could be
related to the system could be:

- HDMI 7" 800x480 Display With Touchscreen
  <https://www.adafruit.com/products/2407>

- Raspberry Pi Camera Module V2
  <https://thepihut.com/collections/raspberry-pi-accessories/products/raspberry-pi-camera-module>

- Raspberry Pi Sense HAT (Astro-Pi)
  <https://thepihut.com/collections/raspberry-pi-accessories/products/raspberry-pi-sense-hat-astro-pi?variant=4552311044>

- Ultrasonic Distance Sensor (HC-SR04)
  <https://thepihut.com/collections/raspberry-pi-accessories/products/ultrasonic-distance-sensor-hcsr04>

- RTK Motor Controller Board Kit
  <https://thepihut.com/collections/raspberry-pi-accessories/products/rtk-motor-controller-board-kit?variant=758603397>

- Temperature Sensor for Raspberry Pi
  <https://thepihut.com/collections/raspberry-pi-accessories/products/temperature-sensor-for-raspberry-pi?variant=1258572784>

- Wireless Keyboard & Trackpad Combo Remote
  <http://www.buyraspberrypi.com.au/shop/wireless-keyboardtrackpad-combo-remote/>

One of the most beneficial aspects of the Raspberry PI comes from the intent of
its design (quote from Wikipedia).

> The Raspberry Pi is a series of credit card–sized single-board computers
> developed in the United Kingdom by the Raspberry Pi Foundation with the intent
> to promote the teaching of basic computer science in schools and developing
> countries.

Due to this aspect of its nature, the is a very large body of freely available
introductory and educational materials available. It also means that the
interfaces and programs that are installed and designed for use with the RPI are
very user and beginner friendly. The RPI language of choice is Python, which
provides serveral advantages. The first is that Python is also a beginner
friendly language, yet is powerful enough that it has seen widespread adoption
throughout the scientific community. There is a large and vibrant 'ecosystem' of
libraries and packages to provide useful out of the box functionality.

**Pricing **

A standalone Rasberry PI 3 (not including any supporting peripherals) can be
purchased for $69.00 AUD. Shipping is then a further $9.40 AUD for express
shipping and $7.20 AUD for regular post.

- <http://raspberry.piaustralia.com.au/products/raspberry-pi-3-model-b>
- <http://www.buyraspberrypi.com.au/shop/raspberry-pi-3-model-b/>
- <http://au.element14.com/raspberry-pi/raspberrypi-modb-1gb/raspberry-pi-3-model-b/dp/2525226>

**Specifications **

```text
SoC: Broadcom BCM2837
CPU: 4× ARM Cortex-A53, 1.2GHz
GPU: Broadcom VideoCore IV
RAM: 1GB LPDDR2 (900 MHz)
Networking: 10/100
Ethernet, 2.4GHz 802.11n wireless
Bluetooth: Bluetooth 4.1 Classic, Bluetooth Low Energy
Storage: microSD
GPIO: 40-pin header, populated
Ports: HDMI, 3.5mm analogue audio-video jack, 4× USB 2.0, Ethernet, Camera
Serial Interface (CSI), Display Serial Interface (DSI)
```

##### 1.4.2 - Arduino

From Wikipedia,

> Arduino is a software company, project, and user community that designs and
> manufactures computer open-source hardware, open-source software, and
> microcontroller-based kits for building digital devices and interactive
> objects that can sense and control physical devices.

The Arduino's purpose would be to act as a high level intermediatery where any
low level serial communication is required. This would include any systems that
do not have high level networking capabilities and require some form of 'raw'
input / output. This is an example of some sample code that blinks an LED on an
off with a delay.

```text
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin 13 as an output.
  pinMode(13, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(13, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);              // wait for a second
  digitalWrite(13, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);              // wait for a second
}
```

Similar to the RPI the Arduino was also designed with the primary intent of
being an educational tool, and thus benefits from the same advantages as
mentioned above for the Raspberry PI.

The development environment is also very easy to set up (one line install from
the package manager), is compatable with the RPI, and includes its own IDE
(integrated development environment) in order to make the startup time as small
as possible. [Here](<http://www.seeedstudio.com/recipe/166-basic-pi-lt-gt-arduin
o-communication-over-usb.html>) is a link to instructions detailing exactly how
to set up a basic form of communication between a RPI and an Arduino


**Pricing **

Pricing for the Arduino varies as there are several different models each with
varying degrees of capability.

The top of the line Arduino Mega 2560 R3 retails for $81.93 AUD. From there the
price decreses by around half for the standard model Arduino.

- <http://littlebirdelectronics.com.au/collections/arduino/products/arduino-mega-2560-r3>

##### 1.4.3 - Qt

- Application interface library
- Comes with IDE and GUI designer
- Includes abstractions of network sockets, threads, Unicode, regular
  expressions, SQL databases, SVG, OpenGL, XML, a fully functional web browser,
  a help system, a multimedia framework, as well as a rich collection of GUI
  widgets
- Open Source with GPL and LGPL licences for non commercial and educational
  purposes
- Initial release was on 20 May 1995; 20 years ago, proven, reliable
- Supports both GUIs (general user interfaces) and CLIs (command line interfaces)

##### 1.4.4 - PyQt

- Python bindings for the Qt application library which is written in C++
- Runs on all platforms supported by Qt including Windows, MacOS/X and Linux.
  PyQt5 supports Qt v5
- It allows us to reduce the scope of the technology used to Python
- Open source
- For more info see <https://riverbankcomputing.com/software/pyqt/intro>

##### 1.4.5 - PyQwt

- PyQwt is a set of Python bindings for the Qwt C++ class library which extends
  the Qt framework with widgets for scientific and engineering applications.
- It provides a widget to plot 2-dimensional data and various widgets to display
  and control bounded or unbounded floating point values.
- For an example of some 2d data plotes see
  <http://pyqwt.sourceforge.net/gui-examples.html>
- For 3d examples see
  <http://pyqwt.sourceforge.net/pyqwt3d-examples.html>
- Built in for graphing and displaying data from the NumPy and SciPi Python
  packages. These are two of the most popular libraries for scientific and
  numerical use, as well as providing considerable performance improvements

## 2 - Race modeling and simulation

### 2.1 - Overview

This document contains many references to combinations of systems that have the
potential to produce large amounts of data. Some examples of the data that may be
produced is

- Position
- Speed
- Battery capacity
- Battery discharge
- Battery temperature
- Cockpit temperature
- Accelerometer (G force)

The plan is to store this data onboard the the solar vehicle whilst it is
operating. Then once the car has finished a training run, this data can then be
taken and analyzed. The race modeling and simulation system is designed to
process this data and and utilize it in such a way to compare to previous
performance as well try and predict ways in which to imporve future performance
of the car.

### 2.2 - Main Goals

- Import and collect data produced by the solar vehicle
- Store, organise and present the data in such a way that it can be easily
  accessed by all members that require access to the data
- Perform analysis of data both to compare to previous runs and try and predict
  future performance runs of the car
- Model or aproximate potential design variations and compare their performance
  to the current car
- Simulate race conditions and simulate predicted performance of other teams
  using data from the previous event (a virtual race)

### 2.3 - Limitations

This project will not be as physically limited in scope as the other proposals,
being mainly an input / output based. However it is still limited by the
technical expertise of the team that is implementing it.

### 2.4 - Components

#### 2.4.1 - Python

From the Wikipedia page on the Python Programming language,

> Python is a widely used high-level, general-purpose, interpreted, dynamic
> programming language. Its design philosophy emphasizes code readability, and
> its syntax allows programmers to express concepts in fewer lines of code than
> would be possible in languages such as C++ or Java. The language provides
> constructs intended to enable clear programs on both a small and large scale.

> Python supports multiple programming paradigms, including object-oriented,
> imperative and functional programming or procedural styles. It features a
> dynamic type system and automatic memory management and has a large and
> comprehensive standard library.

Python, as mentioned above, has seen widespread adoption throughout the academic
community. The Python language is also used in many places as the defacto
language to learn programming in, slowly edging out larger, more established
rivals such as Java. The ANU course COMP1730 - Introduction to Programming for
Scientists, which is a course that is frequently taken by both engineers and
scientist alike, is taught using Python.

Another implication of the widspread use of Python is that many packages and
libraries have already been written, and are seeing large adoption throughout
industry and academia alike. The Python package index currently has 80665
pacakges published to it at the time writing. This means that any implementation
attempted has a high likelyhood of being related to some sort of work that
someone has already done, and allows one to leverge new work based of the
previous attempts.

#### 2.4.2 - Cython

Cython stands as the fill in answer to any of the perfromance issues that may be
encountered due to Python's dynamic nature. As Python is quite a high level
interpreted language, it means that there is a performance overhead in the
runtime environment of all Python programs. For most small programs this
overhead will not be humanly perceptible, however for more performance intensive
calculations, it may start to become noticeable.

Cython aims to address this problem by adding C-style type anotations to the
source code. The source code is then compiled (as opposed to interpreted in the
case of a normal python program), and then can be run as a stanalone binary or
imported and run in the same way as a standard Python module. This allows easy
and portable performance.

From the Cython website

> Cython is a compiler which compiles Python-like code files to C code. Still,
> 'Cython is not a Python to C translator'. That is, it doesn’t take your full
> program and 'turns it into C' – rather, the result makes full use of the
> Python runtime environment. A way of looking at it may be that your code is
> still Python in that it runs within the Python runtime environment, but rather
> than compiling to interpreted Python bytecode one compiles to native machine
> code (but with the addition of extra syntax for easy embedding of faster
> C-like code).
>
> This has two important consequences:
>
> **Speed**. How much depends very much on the program involved though. Typical
> Python numerical programs would tend to gain very little as most time is spent
> in lower-level C that is used in a high-level fashion. However for-loop-style
> programs can gain many orders of magnitude, when typing information is added
> (and is so made possible as a realistic alternative).
>
> **Easy calling into C code**. One of Cython’s purposes is to allow easy wrapping
> of C libraries. When writing code in Cython you can call into C code as easily
> as into Python code.


#### 2.4.3 - NumPy

#### 2.4.4 - SciPy

#### 2.4.5 - Theano

## 3 Race, communication, and development processes

### 3.1 - Overview

### 3.2 - Main Goals

### 3.3 - Limitations

### 3.4 - Components

#### 3.4.1 - WebSockets

#### 3.4.2 - Markdown

#### 3.4.3 - Git

#### 3.4.4 - Pandoc

#### 3.4.5 - Latex

#### 3.4.6 - IRC

#### 3.4.7 - The Python Ecosystem

