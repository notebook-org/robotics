## Basic Principle

- Satellite with a known position transmit a regular time signal.

- Based on the measured travel time of the radio wave, the position of the reciever is calculated.

- Time of the clock on-board, may not be exactly synchronized with the clock at the transmitter. So there can be discrepancy between the calculated and actual distance travelled.

- **pseudorange:** In navigation, observed distance referenced to the local clock is referred to as pseudorange.

### Solution to time synchronized issue

  - ![](Notes/1.png)

  - The solution involves using a second synchronized time signal transmitter, for which the seperation to the first transmitter is known.

  - When an unsynchronized onboard clock is employed in calculating position, it is necessary that the number of time signal transmitters exceed the number of unknown dimensions by a value of one.

### Navigation message
1. GNNS date and time 
2. Satellite status and health
3. Satellite ephemeries data, which allows the receiver to calculate the satellite's position
4. Almanac, which contains information and status of all GNSS satellites.
