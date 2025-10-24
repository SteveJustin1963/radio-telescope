# radio-telescope


# 1 The Mini Radio Telescope 
- https://github.com/UPennEoR/MiniRadioTelescope
(MRT) project from UPennEoR, hosted on GitHub, is a DIY system that uses a satellite TV dish and hobbyist electronics to create a small-scale radio telescope. Here's a breakdown of how it works based on the provided information and general knowledge of similar systems:

### System Overview
The MRT is designed to detect and map radio signals from celestial sources, such as the 21 cm hydrogen line emitted by neutral hydrogen in the Milky Way. It combines hardware (a satellite dish and electronics) with software (Arduino and Python code) to control the telescope, collect data, and process it into meaningful observations, such as sky maps.

### Hardware Components
1. **Satellite TV Dish**:
   - Acts as the primary antenna to collect radio signals from the sky.
   - The dish focuses incoming radio waves onto a receiver (feed horn or low-noise block downconverter, LNB) to amplify weak signals.

2. **Electronics**:
   - **Arduino**: Controls the movement of the dish (if motorized) and interfaces with sensors or other components. The Arduino sketch `MRTArduino` (previously `MRTv2`) is the working code for this.
   - **Raspberry Pi (or similar)**: Runs the Python code (`MRT_PY4.py`) to process data, control the system, and potentially generate visualizations like sky maps.
   - **RF Components**: Includes a feed horn, LNB, and possibly a software-defined radio (SDR) or similar receiver to capture and digitize radio signals.

3. **Detailed Parts List**: The GitHub mentions a detailed parts list, which likely includes specific models for the LNB, coaxial cables, motors for dish positioning (if applicable), and power supplies. This list is not provided in the document but is referenced as part of the repository.

### Software Components
1. **Arduino Code (`MRTArduino`)**:
   - Controls the hardware, such as motors for pointing the dish or reading data from sensors.
   - Interfaces with the RF receiver to collect raw signal data.
   - Likely sends data to the Raspberry Pi or another computer for further processing.

2. **Python Code (`MRT_PY4.py`)**:
   - Runs on a Raspberry Pi or similar device.
   - Processes raw radio signal data, possibly using libraries like NumPy or SciPy for signal analysis.
   - Generates maps of the sky based on received signal strength at different coordinates.
   - May include functionality for calibrating the telescope or filtering noise.

### How It Works
1. **Signal Collection**:
   - The satellite dish captures radio waves from a specific region of the sky, determined by its pointing direction.
   - The LNB amplifies and downconverts the radio signals (e.g., from the 1.42 GHz hydrogen line to a lower frequency) for processing.

2. **Data Acquisition**:
   - The Arduino interfaces with the RF receiver or SDR to sample the signal strength or spectrum.
   - The Arduino may also control motors to scan the dish across the sky in a grid pattern to map a larger area.

3. **Data Processing**:
   - The Python script (`MRT_PY4.py`) takes the raw data from the Arduino or receiver.
   - It processes the data to filter noise, calibrate the signal (e.g., against a known source), and convert signal intensities into a sky map.
   - The resulting maps visualize radio sources, such as the galactic plane, where hydrogen emissions are strong.

4. **Output**:
   - The system produces maps or plots of radio signal intensity as a function of sky coordinates (e.g., right ascension and declination).
   - These maps can reveal structures like the Milky Way or other radio-emitting objects.

### Example Application
- The MRT can be used to detect the 21 cm hydrogen line, a key signal in radio astronomy, to map the distribution of neutral hydrogen in the galaxy.
- It’s a low-cost, educational tool for students and hobbyists to learn about radio astronomy and signal processing.

### Additional Notes
- The Hackaday article (linked in the GitHub README) provides context about the project’s goals and accessibility, describing it as a "miniature radio telescope in every backyard." This suggests the system is designed to be affordable and replicable.
- The repository does not mention specific setup instructions or calibration procedures, but these are likely included in the detailed parts list or associated documentation.
- If you want to explore further, you can:
  - Check the GitHub repository for the `MRTArduino` and `MRT_PY4.py` files to see the exact code.
  - Review the detailed parts list for specific hardware requirements.
  - Refer to the Hackaday article for a narrative overview of the project.

# 2 DIY project to build a radio telescope capable of detecting neutral hydrogen emissions

The article from IEEE Spectrum describes a DIY project to build a radio telescope capable of detecting neutral hydrogen emissions at a wavelength of 21 centimeters (frequency of 1420 MHz), which allows tracking the motion of the Milky Way’s spiral arms. Here’s a breakdown of the key components, construction, and functionality of the setup:

### Objective
The goal is to create an affordable (under $150) radio telescope to observe neutral hydrogen emissions, a key signal used by radio astronomers to map interstellar gas clouds and study the dynamics of the Milky Way’s spiral arms.

### Components and Construction
1. **Antenna Design**:
   - **Horn Antenna**: The main antenna is a horn made from aluminum flashing (51 cm wide, $13), cut into four 75 cm-long pieces to form a pyramid shape. The dimensions provide a directional gain of 17 decibels, calculated using an online tool.
   - **Waveguide**: An empty 1-gallon paint-thinner can ($9) serves as the waveguide, feeding signals to the antenna. Its size is suitable for the 1420 MHz frequency.
   - **Signal Pickup**: A wire “pin” inside the waveguide, connected to an N-type coaxial bulkhead connector ($5) and an N-to-SMA adapter ($7), captures the signal. The pin is placed 68 mm from the base of the can, calculated using the guide wavelength for optimal signal propagation.

2. **Receiver System**:
   - **USB Dongle**: A software-defined radio (SDR) dongle with a TV tuner ($37 from Nooelec) serves as the receiver, paired with HDSDR software for signal processing.
   - **Amplifier and Filter**: A device with two low-noise amplifiers and a surface-acoustic-wave (SAW) filter centered at 1420 MHz ($38) boosts the signal. Power is supplied through a 30 cm coaxial cable ($9).
   - **Connection**: The dongle connects to a Windows laptop via a USB extension cable.

3. **Materials and Assembly**:
   - Aluminum flashing is used instead of aluminized foam-board insulation (which failed to shield radio signals in a test).
   - The horn is reinforced with ordinary foam board and assembled using aluminized HVAC tape ($8).

### Functionality
- **Detecting Hydrogen Emissions**: The telescope captures the 21 cm wavelength emitted by neutral hydrogen, a signal used to map the Milky Way’s structure. By pointing the antenna at specific stars (e.g., Deneb in Cygnus), it detects a strong hydrogen “line” (a spectral peak) at 1420.4 MHz.
- **Doppler Shift Observations**: When aimed at different galactic longitudes (e.g., toward Cassiopeia), the hydrogen line shifts slightly (e.g., to 1420.5 MHz), indicating the relative motion of gas clouds in the Milky Way’s spiral arms due to the Doppler effect.
- **Signal Processing**: The HDSDR software averages the signal over time, producing a spectral plot that shows the hydrogen line as a distinct peak, allowing users to analyze frequency shifts and map galactic structure.

### Outcome
The telescope successfully detects neutral hydrogen emissions, enabling the user to observe the Milky Way’s spiral arms and their motions. While not capable of detecting extraterrestrial signals, the project offers an accessible way to engage with radio astronomy.

### Response to Comment
Regarding Britt Braghini’s question on improving the setup or signal processing:
- **Setup Improvements**:
  - **Larger Antenna**: Increasing the horn’s aperture (e.g., using wider flashing) could improve gain and sensitivity, though it would raise costs and complexity.
  - **Better Shielding**: Ensure all connections are tightly sealed to minimize signal leakage, possibly using higher-quality coaxial cables or connectors.
  - **Mounting System**: Adding a motorized mount for precise pointing could enhance tracking of celestial objects.
- **Signal Processing**:
  - **Advanced Software**: Explore software like GNU Radio for more sophisticated signal analysis or custom filtering.
  - **Calibration**: Regularly calibrate the system against known sources (e.g., the Sun or a calibration signal) to improve accuracy.
  - **Noise Reduction**: Use additional low-noise amplifiers or better grounding to reduce interference.
  - **Data Analysis**: Implement scripts to automate Doppler shift calculations or integrate data over longer periods for clearer spectral plots.

# 3


- https://spectrum.ieee.org/track-the-movement-of-the-milky-way-with-this-diy-radio-telescope

# 4



- https://www.opensourceradiotelescopes.org/

# 5

- https://www.radio-astronomy.org/

# 6

- https://radiojove.gsfc.nasa.gov/
- 
