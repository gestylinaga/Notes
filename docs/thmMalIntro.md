# MAL: Malware Introductory

* **Malware Analysis** -- form of incidence response

* when analysing malware, consider:

    - Point of Entry -- PoE; through spam email?

    - any files/processes/*unordinary* communication

    - RAT -- Remote Access Tool; backdoor

    - can we prevent further infection?


## Malware Campaigns

* **Targeted** 

    - created for a specific purpose, against a specific person

    - see [DarkHotel](https://www.kaspersky.co.uk/resource-center/threats/darkhotel-malware-virus-threat-definition) malware

* **Mass Campaign**

    - most common type of attack

    - entire purpose is to infect as many devices as possible

    - **APTs** -- Advanced Persistent Threats; another name for these campaigns

        - companies like Kaspersky track APTs and write reports like the World Health Organisation


## Identifying a Malware Attack

* Process of a malware attack in broad steps:

    1. **Delivery**

        + USB -- Stuxnet!

        + PDF attachments through *Phishing*

        + vulnerability enumeration

    2. **Execution**

        + main factor in classifying malware

        + it encrypts files -- *Ransomware*

        + records keystorkes -- *Spyware*

        + only understood through analysing the sample

    3. **Maintaining Persistence**

        + not always the case; see [Cerber](https://blog.malwarebytes.com/detections/ransom-cerber/)

    4. **Persistence**

        + makes sure the *execution* is worth its while

        + this stage is what makes malware so *noisy*

    5. **Propagation**

        + host discovery causes a lot of network traffic; makes it noticeable

        + 2 categories of fingerprints left on host

            1. **Host-Based Signatures**

                - result of any execution or persistence performed by the malware

                - have any files be encrypted?

                - has any additional software been installed?

            2. **Network-Based Signatures**

                - observations of any network communtication during delivery/execution/propagation

                - in ransomware: where has the Malware contacted for Bitcoin payments?

* see [EternalBlue](https://research.checkpoint.com/2017/eternalblue-everything-know/)


## Static vs Dynamic Analysis

* Static Analysis

    - used to gain a high-level abstraction of the sample

    - analysis at the state the malware presents itself, without executing the code

    - ie: signature analysis via checksums

    - quick, efficient, and safe 

* Dynamic Analysis

    - a lot more involved, where the abstraction of the sample is built upon

    - executing the sample and observing what happens

    - **NOT SAFE** obviously

---
[back to TryHackMe main page](thm.md)

[back to Index/Table of Contents](index.md)
