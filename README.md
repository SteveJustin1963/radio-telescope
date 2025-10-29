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

- https://spectrum.ieee.org/track-the-movement-of-the-milky-way-with-this-diy-radio-telescope

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

# 3 Open Source Radio Telescopes (OSRT)
- https://www.opensourceradiotelescopes.org/

### Overview of Open Source Radio Telescopes (OSRT)

The website **https://www.opensourceradiotelescopes.org/** is the online hub for the **Open Source Radio Telescopes (OSRT)** initiative. OSRT is a collaborative, community-driven project aimed at democratizing radio astronomy—essentially, making it easier and more affordable for hobbyists, educators, students, and enthusiasts to build and use their own radio telescopes. The tagline "Observe the Invisible Universe" highlights how these tools allow users to detect radio waves from cosmic sources like pulsars, galaxies, and the cosmic microwave background, which are invisible to optical telescopes.

#### Purpose and Mission
OSRT's core goal is to lower the barriers to entry in radio astronomy by promoting **open-source designs, software, and educational resources**. It positions itself as a central database and collaboration space where people at any skill level—from elementary school kids to advanced researchers—can access tools and knowledge to construct personal radio telescopes. This aligns with broader open-source principles, emphasizing free sharing of ideas to foster innovation and learning.

The initiative addresses key challenges in the field:
- High costs of professional equipment.
- Complexity of signal processing.
- Lack of accessible curricula for teaching radio astronomy.

By focusing on low-cost, off-the-shelf components (like affordable electronics and antennas), OSRT makes the hobby feasible without needing expensive specialized gear.

#### Main Features and Goals
The site outlines three primary objectives:
1. **Collaborative Open-Source Collection**: A shared repository of ideas, blueprints, and methods for building educational radio telescopes. This includes hardware designs (e.g., antennas and receivers) and software for data analysis.
2. **Educational Resources**: Free curricula and materials tailored for all ages and levels, from basic introductions to advanced topics. These help integrate radio astronomy into classrooms or personal projects.
3. **Accessible Tools and Discussions**: Advocacy for using free software like **GNU Radio** (an open-source toolkit for signal processing) alongside cheap hardware. The community discusses ways to make digital signal processing more approachable, enabling real-time analysis of radio signals.

The website itself is straightforward, with a clean, minimalist design centered on the homepage. It doesn't appear to have extensive subpages (based on the content), but it serves as an entry point to the broader ecosystem.

#### Projects and Resources
While the site doesn't list specific ongoing projects in detail, it emphasizes user-generated content like:
- **Open-Source Designs**: Blueprints for DIY radio telescopes, such as simple dish antennas or interferometers built from household items.
- **Software and Code**: Integrations with GNU Radio for processing signals from sources like the Sun, Jupiter, or hydrogen emissions from space.
- **Example Builds**: Community-shared examples of telescopes that detect phenomena like meteor trails or satellite signals, often documented with step-by-step guides.

Resources are geared toward hands-on learning, with an implied focus on reproducibility—anyone can download, modify, and contribute back.

#### How to Get Involved
OSRT is all about participation. The site encourages visitors to:
- **Build Your Own**: Start with beginner-friendly kits or guides to assemble a basic radio telescope (e.g., using RTL-SDR dongles for under $50).
- **Share Contributions**: Upload your designs, code, or lesson plans to the database.
- **Join the Community**: Engage in discussions (likely via linked forums, Discord, or email lists—though specifics aren't detailed on the homepage) to collaborate on improvements or troubleshooting.

If you're new, the site implicitly suggests starting with the educational materials to understand fundamentals like radio frequency basics before diving into hardware.

#### Why It Matters
In a field dominated by billion-dollar observatories like the Square Kilometre Array, OSRT empowers "citizen scientists" to contribute to real discoveries. For instance, amateur radio telescopes have historically detected events like the Wow! signal or tracked spacecraft. By October 2025, with growing interest in space tech (e.g., via Starlink or Artemis missions), initiatives like this could spark more grassroots involvement in astronomy.



# 4 Society of Amateur Radio Astronomers (SARA)
- https://www.radio-astronomy.org/

### Overview of the Website
The URL https://www.radio-astronomy.org/ is the official website for the **Society of Amateur Radio Astronomers (SARA)**, a nonprofit organization founded to advance the hobby and science of radio astronomy among non-professionals. Radio astronomy involves detecting and studying radio waves from celestial objects like stars, galaxies, pulsars, and fast radio bursts (FRBs) using specialized antennas and receivers—often DIY or low-cost setups that amateurs can build or operate from home or remote observatories. SARA's mission emphasizes education, practical training, community building, and knowledge sharing, making complex astrophysics accessible to hobbyists, educators, students, and curious enthusiasts without requiring a PhD or professional-grade equipment.

The site serves as a hub for SARA members and the broader amateur radio astronomy community, promoting hands-on experiments (e.g., observing Jupiter's radio emissions or solar bursts) and fostering collaborations with institutions like the Green Bank Observatory (GBO) in West Virginia, a leading facility for radio telescope research.

### Target Audience
This website is geared toward:
- **Amateur astronomers and radio hobbyists**: People interested in building simple radio telescopes or joining observation projects.
- **Educators and students**: Resources support STEM learning, including workshops on topics like pulsars (rapidly rotating neutron stars) and mysterious FRBs (intense, millisecond-long radio signals from deep space).
- **Global community**: Events are open to international participants, with both in-person and virtual options to encourage worldwide involvement.

### Main Content and Sections
The homepage and key pages focus on events, resources, and announcements, structured around SARA's core activities. Here's a breakdown:

- **Conferences and Events**: A prominent feature, highlighting annual symposia for training, lectures, and networking. Examples include:
  - **2025 SARA and Radio Jove Eastern Conference & Global Radio Astronomy Symposium**: Scheduled for 2025 at the Green Bank Observatory, featuring guest speaker Dr. Emmanuel Fonseca, a researcher specializing in pulsars and FRBs. These events blend amateur sessions with professional insights, covering detection techniques and data analysis.
  - **2024 SARA Eastern Conference**: Held August 4–7, 2024, at GBO, with hybrid (in-person and online) formats for hands-on workshops and discussions.
  - **2024 SARA Western Conference**: Took place April 8–9, 2024, at the University of Texas in Dallas, timed to coincide with a total solar eclipse for integrated radio and optical observations.

- **Educational Resources and Projects**: While the homepage emphasizes events, deeper navigation (via linked nodes) reveals tools like project guides for building radio receivers, observation protocols (e.g., via the Radio Jove project for solar and Jovian radio signals), and forums for debating ideas or troubleshooting setups.

- **News and Blog-Style Updates**: Sections like "Node" pages announce speakers, research highlights, and symposia, often tying into current astronomy news (e.g., FRB origins potentially linked to neutron star mergers).

The site's design is straightforward and functional—think clean layouts with calendars, registration links, and photo galleries from past events—prioritizing utility over flashy visuals.

### Key Features and Benefits
- **Community and Fellowship**: SARA hosts debates, mentorships, and collaborative projects, helping newcomers progress from basic kits to advanced data processing.
- **Accessibility**: Many resources are free or low-cost, with virtual attendance options to lower barriers.
- **Integration with Pros**: Partnerships with GBO and experts like Dr. Fonseca bridge amateur and professional worlds, offering real-world applications (e.g., contributing to citizen science databases).

### Calls to Action
The site encourages visitors to join SARA (membership starts around $30/year for access to exclusive resources), register for upcoming conferences, or participate in ongoing projects. If you're new, start with their beginner guides or the Radio Jove kit for your first radio astronomy experiment—it's a low-entry way to "listen" to the universe's hidden radio symphony. For more, explore the full site or check event pages for 2025 details.

# 5 Radio JOVE Project

- https://radiojove.gsfc.nasa.gov/

The **Radio JOVE Project** is an educational initiative led by NASA, designed to engage students, amateur scientists, and enthusiasts in radio astronomy. It allows participants to observe and analyze natural radio emissions from celestial bodies such as Jupiter, the Sun, and our galaxy using affordable, easy-to-build radio telescope kits. The project's website (http://radiojove.gsfc.nasa.gov/) serves as a hub for resources, updates, and community engagement. Below is a detailed explanation based on the provided document and the project's context:

### Overview of Radio JOVE
- **Purpose**: The Radio JOVE Project enables participants to study decametric (radio waves in the 10–40 MHz range) emissions from Jupiter, solar bursts, and galactic background radiation. It fosters hands-on learning in radio astronomy through building and operating radio telescopes.
- **Participants**: Students, educators, amateur astronomers, and citizen scientists worldwide.
- **History**: Launched in 1999, the project celebrated its 25th anniversary in 2024. It has grown into a global community, with contributions from many participants, some of whom are no longer with us.

### Key Components and Resources
1. **Radio Telescope Kits**:
   - **Original Kits**: The initial Radio JOVE kits included a simple receiver tuned to 20.1 MHz for observing Jupiter and solar emissions.
   - **New SDR-Based Kits (Radio JOVE 2.1)**: The project now offers advanced kits using the **SDRPlay RSP1B receiver**, which allows simultaneous observation across a range of frequencies (e.g., 16–24 MHz). These kits are available through the Kit Orders page on the website.
   - **Antenna**: Typically, a wideband Terminated Folded Dipole (TFD) antenna is used, as mentioned in the Observer’s Corner.

2. **Software**:
   - **Radio-Sky Spectrograph (RSS)**: This is the preferred software for recording and displaying spectrograph data. It visualizes radio emissions with time on the x-axis, frequency (in MHz) on the y-axis, and intensity represented by color. The latest version can be downloaded from http://radiosky.com/spec/Spectrograph.exe.
   - **Purpose**: RSS helps users analyze solar and Jovian radio bursts, identifying patterns like Solar Type II and Type III bursts.

3. **Live Data Streaming**:
   - Team member **Larry Dodd** live-streams spectrograph data and audio on YouTube (https://youtube.com/channel/UCtawz3MnMBwjz9ShhSC0ygQ/live). The spectrograph data cover 16–24 MHz from an SDRPlay receiver, while audio is from a 20.1 MHz Radio JOVE receiver.

4. **Training and Education**:
   - In partnership with the **SunRISE Ground Radio Lab**, Radio JOVE offers training modules on radio astronomy and how to use the Radio JOVE system. These are accessible through the website.
   - The project emphasizes hands-on learning, with resources for building, testing, and operating telescopes (e.g., http://radiojove.gsfc.nasa.gov/radio_telescope/building_testing.php).

5. **Observer’s Corner**:
   - This section highlights recent observations, such as the **X1.2 solar flare** on May 13, 2025, recorded by Richard Gray and Jacob Hansman at the Dark Sky Observatory in Boone, NC. They used a wideband RX-888 MK II receiver and a TFD antenna to capture:
     - A strong **Solar Type III burst** at 1535 UTC, characterized by rapid frequency drifts.
     - A slower-drifting **Solar Type II burst** from 1551–1555 UTC.
     - Detailed spectrograms showing fine structures of the flare’s radio emissions.
   - These observations demonstrate the project’s ability to capture significant astronomical events.

6. **Historical Significance**:
   - The project commemorates the 1955 discovery of **Jupiter’s radio emissions**, marked by a Maryland Historic Marker. A video about this milestone is featured on the website.
   - The 25-year milestone (1999–2024) celebrates the contributions of the Radio JOVE community.

### What’s New (as of October 1, 2025)
- **Website Status**: Due to a lapse in federal funding, NASA is not updating the website, which may limit access to new content.
- **New Kit Availability**: The Radio JOVE 2.1 kit with the SDRPlay RSP1B receiver is now available, enhancing the ability to observe a broader frequency range.
- **Training Modules**: New educational resources have been developed with SunRISE to support users in radio astronomy.

### How It Works
- **Building a Telescope**: Participants construct their own radio telescopes using kits provided by Radio JOVE. The process is detailed on the website’s building and testing page.
- **Observing**: Users tune into specific frequencies (e.g., 20.1 MHz for Jupiter or 16–24 MHz for broader observations) to capture radio emissions.
- **Analyzing Data**: Software like RSS generates spectrograms, which visually represent radio signal intensity over time and frequency. For example, solar bursts appear as distinct patterns (Type II or III) on these charts.
- **Community Engagement**: Observers share findings through the JOVE Bulletin, Observer’s Corner, and platforms like YouTube.

### Significance
- **Educational Impact**: Radio JOVE makes radio astronomy accessible, fostering STEM education and citizen science.
- **Scientific Contribution**: Participants contribute to real scientific observations, such as solar flares and Jovian emissions, which are shared within the community.
- **Global Reach**: The project connects a worldwide network of enthusiasts, from students to professional astronomers.

### Accessing Radio JOVE
- **Website**: http://radiojove.gsfc.nasa.gov/ (note the funding-related update limitation).
- **YouTube Live Stream**: For real-time data, visit Larry Dodd’s channel.
- **Kit Orders**: Available through the website’s Kit Orders page.
- **Software**: Download RSS from the provided link for data analysis.


