# Global Positioning System (GPS)
- Originally Navstar GPS.
- It is a satellite based radionavigation system.
- Owned by: US Government
- Operated by: US Space Force
- GNSS (Global Navigation Satellite System) provides **geolocation** and **time** information to a GPS receiver, anywhere there is an unobstracted line of sight.
- To estimate location of GPS receiver you need to get signal from four or more GPS satellite.
- The GPS does not require the user to transmit any data.
- It operates independently of any telephonic or Internet reception.
- US made it freely accessible to anyone with a GPS receiver.

## Basic Concepts
- GPS receiver calculates its own 4D position in spacetime based on data received from multiple GPS satellites.
- Each satellite carries an accurate record of its position and time, and transmits that data to the receiver.
- At a minimum, four satellites must be in view of the receiver for it to compute four unknown quantities:
    1. Three position coordinates
    2. Deviation of its own clock from satellite time.
- Each GPS satellite continually broadcasts a signal (carrier wave with modulation) that includes:
    1. A pseudorandom code that is known to the receiver. By time-aligning a receiver-generated version and the receiver-measured version of the code, the time of arrival (TOA) of a defined point in the code sequence, called an epoch, can be found in the receiver clock time scale.
    2. A message that includes the time of transmission (TOT) of the code epoch (in GPS time scale) and the satellite position at that time.

- From the TOAs and the TOTs, the receiver forms time of flight (TOF) values.
- TOF --> (receiver satelite distance) + (dt * speed of light)
- Where, dt is time difference between the receiver and GPS satelite.
- 3D position and dt is calculated simultaneously, using the **navigations equations** to process the TOFs.
- The receiver's Earth-centered solution location is usually converted to:
    1. latitude
    2. longitude
    3. and height relative to an ellipsoidal Earth model.
        - Can be further converted to height relative to the geoid (mean sea level).

## Structure
- The current GPS consists of three major segments:
    1. Space Segment
        - 6 Orbital planes with 4 satellites each. (6 x 4 = 24)
        - The orbits are arranged so that at least six satellites are always within line of sight from everywhere on the Earth's surface.
    2. Control Segment
    3. User Segment 

- GPS receivers are composed of:
1. An antenna, tuned to the frequencies transmitted by the satellites.
2. Receiver processors
3. Highly stable clock

- A receiver is often described by its number of channels: This signifies how many satellites it can monitor simultaneously.

## Communication
- Two different encodings are used:
1. A public encoding that enables lower resolution navigation.
2. Encrypted encoding used by the U.S. military.

- 50 bits/sec
- Each msg takes 750 sec to compleate.
- MSG Frame: 1500 bit = 5 * 300 bit
- 25 * 1500 = 37500 bits -> 37500 / 50 = 750 sec

- The system uses two distinct CDMA encoding types:
1. Coarse/Acquisition (C/A) code, which is accessible by the general public.
2. Precise (P(Y)) code, which is encrypted so that only the U.S. military and other NATO nations who have been given access to the encryption code can access it.

>GOOD NEXT STARTING POINT: LAIKA

## Resources
- [GPS: An Introduction to Satellite Navigation (Stanford)](https://www.youtube.com/playlist?list=PLGvhNIiu1ubyEOJga50LJMzVXtbUq6CPo)
- [laika by comma ai](https://github.com/commaai/laika)
