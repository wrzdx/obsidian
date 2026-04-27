**Types Of Data:**
 - Analog data – continuous information
	 - Ie: analog clock – movement of hands are continous
	 - Human voice
- Digital data – discrete state information
	- Ie: digital clock – suddenly move from 8.05 – 8.06
	- Computer memory

## Signals and Transmission
In data communications, we commonly use periodic analog signals and nonperiodic digital signals.
Periodic analog signals can be classified as simple or composite. A simple periodic analog signal, a sine wave, cannot be decomposed into simpler signals.

**Bandwidth** – the difference between the highest and the lowest frequencies contained in that signal.

**Number of bits per level** $=\lceil \log_{2}L \rceil$
**attenuation or gain in decibels (dB)** $= 10 \log_{10} (\frac{P_{2}}{P_{1}})$ 
- $P_1$​ = original power (input signal)
- $P_{2}$​ = resulting power (after transmission)
**milliwatts**$=10^{\frac{dB}{10}}$
# Switching and Multiplexing
## CIRCUIT-SWITCHED NETWORKS
- Switches at the L1 allow signals to travel in one path or another
- A circuit-switched network consists of a set of switches connected by physical links.
- A connection between two stations is a dedicated path made of one or more links.
- However, each connection uses only one dedicated channel on each link.
- Each link is normally divided into n channels by using FDM or TDM.

## Multiplexing
- Multiplexing is a set of techniques that allows the simultaneous transmission of multiple signals across a single data link.

### Frequency-Division Multiplexing (FDM)
- FDM is analog technique can be applied when the bandwidth of a link (in hertz) is greater than the combined bandwidth of the signals to be transmitted.
- Channels can be separated by strips of unused bandwidth – guard bands.
- Guard bands – to prevent signals from overlapping

### Wavelength-Division Multiplexing
- Conceptually same as FDM, except that the multiplexing and demultiplexing involve light signals transmitted through fiber optics channels.

### Time-Division Multiplexing(TDM)
- a digital process that can be applied when the data rate capacity of transmission medium is greater than the data rate required by the sending and receiving devices.

#### Synchronous TDM
- Synchronous means that the multiplexer allocates exactly the same time slot to each device at all times, whether or not device has anything to transmit
