## ShiftRegisterPISO
### Description
Arduino library for controlling PISO shift register.
PISO stands for Parallel In Serial Out. This type of shift register is used to read multiple digital inputs using only a few microcontroller pins.

The libraly relies on timestamps to manage timing of reading and clock signals. This way, it does not block the main program loop, allowing other parts of the code to run concurrently.

Library further provides methods for setting delays between reading or
adjusting frequency of clock signal. The real time intervals may depend on computational complexity of the main thread.

### Usage
The library provides a class *PISORegister* with methods for initializing and reading data from the shift register.

#### Initialization
To initialize the reading process, *Init()* method must be called. This method initializes the pins connected to shift register and sets the polarity of
signals, as well as number of register inputs.
Required inputs:
 - *pinNum* Number of register inputs (max 64)
 - *clkPin* Pin used for clock signal
 - *ldPin* Pin used for asynchronous load signal
 - *qhPin* Input from shift register
 - *clkPol* Polarity of clock edge - true for rising edge, false for falling edge
 - *ldPol* Logic level of asynchronous loading - false for 0, true for 1
 - *inputLogic* Type of input logic (true for normal, false for inverse)

#### Additional settings
- *SetFrequency()* - Set frequency of clock signal
- *SetReadDelay()* - Set delay between reading inputs
- *SetGlitchPrevention()* - Set number of consistent   readings before updating input data
- *SetLdClkPulseDelay()* - If delay is not 0, generates additional clock pulse during loading phase. Some registers require this to load inputs. This is the delay between loading signal edge and clock pulse signal edge during loading phase. 

#### Reading data
For continuous reading, call *ReadData()* method in main program loop.

To improve input reliability, *SetGlitchPrevention()* method can be used.
Using this option, input data are updated only if the input has been constant for certain number of reading.

To obtain data from specific input, use *GetInput()* method. This input corresponds to the input number on the shift register (0 to pinNum-1).

To obtain data from all inputs as a single integer, use *GetAllInputData()* method.


