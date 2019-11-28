Block ACK Algorithm
****************************************************

Block Acknowledgment is an 802.11 MAC feature that increases throughput by decreasing protocol overhead. Instead of individually acknowledging each received packet, a single block acknowledgment frame can acknowledge multiple packets. This reduces the number of ack frames and corresponding interframe spaces, thereby increasing throughput.


Motivation
==========

The multicast frames are sent in a low data rate without the feedback in IEEE 802.11. The low data rate of multicast causes performance anomaly problem.

Instead of transmitting an individual ACK for every MPDU (i.e., frame), multiple MPDUs can be acknowledged together using a single BA frame.


Class List
==========

The ``BlockAckManager`` includes the following classes: 

* ``BlockAckManager:`` Manages all block ack agreements for an originator station

Attributes
==========

No attributes are defined for this type.

TraceSources
============

* ``AgreementState:`` The state of ADDBA handshake

Explanation
===========

In 802.11, block acknowledgment frames (block acks or BAs) are used within block ack sessions. To establish a block ack session, one of the participants, the originator, sends an ADDBA request frame. The other participant, the recipient, replies with an ADDBA response frame. This exchange establishes the block ack session. The frames contain information about the capabilities of each participant, such as buffer size, or whether aggregation is supported. Each ADDBA frame is acked. The block ack session is for one direction only, i.e. a separate block ack session must be established for the reverse direction. Block ack sessions are terminated by the originator sending a DELBA frame.

The originator sends multiple data frames, then sends a block ack request frame. The recipient replies with a block ack frame, acknowledging the correctly received frames from the previous block. The block ack request frame and block ack frame are acked if delayed block ack is used, and not acked if immediate block ack is used. The frames or fragments of frames from the previous block which are not acked are retransmitted in the next block by the originator. Manages all block ack agreements for an originator station.


References
==========
Seungho Ryu, W. Kim and Y. Suh, "A block ACK transmission scheme for reliable multicast in IEEE 802.11 WLANs," 2016 IEEE Conference on Computer Communications Workshops (INFOCOM WKSHPS), San Francisco, CA, 2016, pp. 978-979.