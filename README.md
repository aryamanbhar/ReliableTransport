I designed a simple transport protocol that provides reliable datagram service for ensuring data gets delivered in order without duplicates, missing data or
errors over networks.

High-level Approach:

Sender (3700send.py):
Initialized a UDP socket and bound it to a specific port.
Implemented methods for sending packets, managing acknowledgments, and adjusting the congestion window.
Implemented a timeout mechanism for packet retransmission meaning when the packet got dropped
Also designed the sending packet mechanism ensuring no duplicates were sent in the process
Parse respone from the receiver to help calculate the RTT and RTO that determine the size of the window throughout the procedure

Receiver (3700recv.py):
Implemented methods for receiving packets, sending acknowledgments, and handling out-of-order packets.
Utilized a temporary buffer to store out-of-order packets until they can be processed once it becomes their turn
Saw the failed output on the terminal to realize it was out of order when a message with a sequence number greater than the current sequence occured first

Challenges Faced
Congestion Control: Designing an efficient congestion control mechanism posed a significant challenge. I had to carefully balance between slow start and congestion avoidance to maximize network throughput without causing congestion collapse. Also it really required me to understand the lecture slides such as the pseudocode provided in the Transport layer slides

Packet Handling: Ensuring reliable packet transmission when they were getting drooped and reception while managing out-of-order packets by the receiver 

I had challenges with the corruption handling as I wasnt able to get the checksum appended in the message, it made the message too long. I believe I could have spent more time on this area as when I encountered this issue I focused on other test cases which took up time. I believe this issue is manageable by possibly changing my mechanism for the congestion control. 
Also the current congestion control mechanism causes the simulation to fail when working with high bandwidth and low latency but works for the other test cases which means my mechanism is too slow and it can be improved definetely.

Good Design Features
Modular Design by seperating code into functions
Documentation: Extensive comments and documentation were provided throughout the codebase to facilitate understanding and future modifications.
Kept code as clean as possible by having purposeful functions and to avoid redundancy

Testing Methodology
Unit Testing: Performed unit tests on individual components of our sender and receiver classes to ensure they functioned as expected.

Integration Testing: Tested with the various bandwidths and latencies provided to best try and design the sending of packets 
