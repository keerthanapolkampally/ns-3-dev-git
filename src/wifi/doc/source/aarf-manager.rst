Adaptive Auto Rate Fallback (AARF) Algorithm
****************************************************

Adaptive ARF (AARF) is alleviate the inefficiency of ARF due to the automatic attempt of new rates every ten successfully transmissions. This algorithm behaves like ARF with one difference: instead of trying the next higher rate every ten successfully
transmissions, it doubles this number whenever the first transmission attempt with the higher rate fails. The number of successfully transmission attempts required to increase the rate is reset to ten every time the rate is decreased and it does not exceed a given threshold (which is equal to 60).


Auto Rate Fallback (ARF)
========================
ARF algorithm uses a fixed transmission power - typically set fairly high to maximize the chance that a node can communicate with the intended destination. However, these high power levels create significant interference which may reduce performance for other channels.

In ARF, each sender attempts to use a higher transmission rate after a fixed number of successful transmissions at a given rate and switches back to a lower rate after 1or 2 consecutive failures. When the rate is increased, the first transmission after the rate increase (commonly referred to as the probing transmission or probing packet) must succeed or the rate is immediately decreased.

If the channel conditions change very quickly, it cannot adapt effectively. If the channel conditions do not change at all or change very slowly, it will try to use a higher rate every 10 successfully transmitted packets; this results in increased retransmission attempts and thus decreases the application throughput. At the highest data rate, even if there are no packet failures, it uses the same transmission power.


Motivation
==========

While ARF is reasonably good at handling short term variations of wireless medium characteristics in an infrastructure network, it fails to handle stable conditions that are the norm efficienetly. 

To avoid the scenario described above an obvious solution is to increase the threshold used to decide when to increase the current rate from 10 to 40 or 80. 

While this approach can indeed improve performance in certain scenarios it does not work in practice since it completely disables the abiltiy of ARF to react to short term channel condition changes. This led to form the basis of AARF. 

Class List
==========

The ``AarfWifiManager`` contains the following classes:

*``AarfWifiManager:`` This class implements the AARF rate control algorithm which was initially described in IEEE 802.11

Attributes
==========

The key attributes that the ``AarfWifiManager`` class holds include the following: 

* ``SuccessK:`` The multiplication factor for the success threshold in the AARF algorithm.
* ``TimerK:`` The multiplication factor for the timer threshold in the AARF algorithm.
* ``MaxSuccessThreshold:`` The maximum value of the success threshold in the AARF algorithm.
* ``MinTimerThreshold:`` The minimum value for the 'timer' threshold in the AARF algorithm.
* ``MinSuccessThreshold:`` The minimum value for the success threshold in the AARF algorithm.

TraceSources
============

*``Rate:`` Traced value for rate changes.

Explanation
===========

In AARF the threshold is continuously changed at runtime to better reflect the changes conditions. In this, the threshold is adapted using binary exponential backoff. When the transmission of the packet fails we switch back immediately to the previous lower rate but we also multiply by two the number of consecutive successful transmissions required to switch to a higher rate.

This threshold is reset to its initial value of 10 when the rate is decreased becuase of two consecutive fail transmissions. The effect of this adaptation mechanism is to increase the period between successive failed attempts to use a higher rate. Fewer failed transmissions and retransmissions improves the overall throughput.

References
==========
M. Lacage, M.H. Manshaei, and T. Turletti. IEEE 802.11 rate adaptation: a practical approach. Proceedings of the 7th ACM international symposium on Modeling, analysis and simulation of wireless and mobile systems, pages 126–134, 2004.