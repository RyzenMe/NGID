---
title: The Network Geographic identification in Computing-Aware Traffic Steering
abbrev: NGID
category: info

docname: draft-ma-cats-ngid-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
area: Routing area
workgroup: cats
keyword:
 - Collaborative Networking


author:
 -
    fullname: "Yuyin Ma"
    organization: Beijing Jiaotong University
    email: "mayuyin@bjtu.edu.cn"
 -
    fullname: "Tianhao Peng"
    organization: Beijing Jiaotong University
    email: "th.peng@bjtu.edu.cn"
 -
    fullname: "Guoqing Dong"
    organization: Beijing Jiaotong University
    email: "22120037@bjtu.edu.cn"
 -
    fullname: "Qixuan Zhang"
    organization: Beijing Jiaotong University
    email: "23120155@bjtu.edu.cn"
 -
    fullname: "Xiaoshuang Lv"
    organization: Beijing Jiaotong University
    email: "20251239@bjtu.edu.cn"
 -
    fullname: "Yuanming Sun"
    organization: China University of Petroleum-Beijing at Karamay(CUPK)
    email: "2021015417@st.cupk.edu.cn"
 -
    fullname: "Yiyun Zhang"
    organization: China University of Petroleum-Beijing at Karamay(CUPK)
    email: "2021015367@st.cupk.edu.cn"
 -
    fullname: "Yuanming Sun"
    organization: China University of Petroleum-Beijing at Karamay(CUPK)
    email: "2021015433@st.cupk.edu.cn"
 -
    fullname: "Qihao Si"
    organization: Beijing Jiaotong University
    email: "21211129@bjtu.edu.cn"
 -
    fullname: "Haocheng Lang"
    organization: Beijing Jiaotong University
    email: "22211145@bjtu.edu.cn"


normative:

informative:


--- abstract

This document proposes a novel network address encoding scheme, called Network Geoidentifier (NGID), which aims to improve the efficiency and accuracy of network device management by directly embedding geolocation information (latitude and longitude) into IPv6 and IPv4 addresses.

This approach provides a native support for the geolocation of network devices and is expected to have a significant impact on the future of network management and service positioning.


--- middle

# Introduction

With the rapid growth of Internet devices, the traditional IP address system has shown its limitations in efficiently managing and identifying the physical location of devices.

The NGID scheme proposed in this draft aims to solve this problem by directly encoding geolocation information in IPv6 and IPv4 addresses, so as to improve the management efficiency of network resources and optimize the geolocation of services.


# The Definition of Terms

NGID: Network geographic identification code, a new type of network address coding scheme.

Latitude: North or south latitude, measured from the equator to the north or south.

Longitude: East or west longitude, the angle measured from the prime meridian to east or west.


# Design of NGID


This section describes in detail the encoding scheme for NGID, including its implementation in the IPv6 and IPv4 address schemes.

## 8-bit NGID

1st place: North and south latitude identifiers (0 for north latitude, 1 for south latitude).

Digits 2-4: Latitude position (binary encoding, can represent the range from 0 to 15, roughly representing latitude information)

5th place: East and West longitude identification (0 for east longitude, 1 for west longitude).

Bits 6-8: Longitude position (binary encoded, can represent the interval from 0 to 15, roughly represent longitude information)

## 12-bit NGID

1st place: North and south latitude identifiers (0 for north latitude, 1 for south latitude).

Bits 2-6: Latitude position (binary encoded, which can represent a range from 0 to 31, providing better latitude accuracy than an 8-bit scheme)

7th place: East and West longitude identification (0 for east longitude, 1 for west longitude).

Bits 8-12: Longitude position (binary encoded, which can represent a range from 0 to 31, providing better longitude accuracy than the 8-bit scheme)

## 16-bit NGID

1st place: North and south latitude identifiers (0 for north latitude, 1 for south latitude).

Digits 2-8: Latitude position (binary encoded to represent the range from 0 to 127, which significantly improves the accuracy of latitude representation)

9th place: East and West longitude identification (0 represents east longitude, 1 represents west longitude).

Digits 10-16: Longitude position (binary encoded to represent the range from 0 to 127, significantly improving the accuracy of longitude representation)

## 24-bit NGID

1st place: North and south latitude identifiers (0 for north latitude, 1 for south latitude).

Digits 2-12: Latitude position (can represent latitude information from 0 to 4095 with an accuracy of 90/4095 degrees)

13th place: East and West longitude identification (0 for east longitude, 1 for west longitude).

Digits 14-24: Longitude position (can represent longitude information from 0 to 4095 with an accuracy of 180/4095 degrees)

## 32-bit NGID

1st place: North and south latitude identifiers (0 for north latitude, 1 for south latitude).

Digits 2-16: Latitude position (can represent latitude information from 0 to 32767 with an accuracy of 90/32767 degrees)

17th place: East and West longitude identification (0 for east longitude, 1 for west longitude).

Digits 18-32: Longitude position (can represent longitude information from 0 to 32767 with an accuracy of 180/32767 degrees)

#  Encoding and decoding process

## NGID encoding steps

Determine latitude and longitude: Get the actual latitude and longitude information of the device.

Convert to Binary: Converts latitude and longitude values to binary format.

The latitude is from 0 to 90 degrees from north to south, and the longitude from 0 to 180 degrees from east to west.

Set the north-south latitude marker: set the first digit to 0 if it is north latitude, and set it to 1 if it is south latitude.

Set Latitude Position: Padding the binary value of latitude to bits 2-16.

Set the east-west longitude marker: set the 17th bit to 0 if it is east longitude, and set it to 1 if it is west longitude.

Set longitude position: Padding the binary value of longitude to bits 18-32.

Combined NGID: Combines the above binary bits into a 32-bit NGID.

The geographical location is N 37.7749° and the longitude is W 122.4194°
North and South Latitude Identification: Since the latitude is north latitude (N), the first digit is set to 0.

Latitude position: The latitude range is 0° to 90°.This range needs to be mapped into 15 bits.

To simplify the process, the latitude value can be multiplied by a factor that allows it to be represented between 0 and 32767 (2^15 - 1).

Specifically, multiply by (2^15 - 1)/90.

For 37.7749°, the corresponding coded value is (37.7749 * (32767 / 90)).

East-West Longitude Mark: Because the longitude is West Longitude (W), the 17th position is set to 1.

Longitude position: Longitude ranges from 0° to 180°.

Similar to latitude, this range needs to be mapped into 15 bits.

Multiply by the factor (2^15 - 1)/180.

For 122.4194°, the corresponding coded value is (122.4194 * (32767/180)).

## NGID decoding steps

Extract the north-south latitude marker: Check the first position to determine whether it is north or south.

Extract latitude position: Read the binary values of bits 2-16 and convert them to decimal latitude values.

Extract the East and West meridian markers: Check the 17th position to determine whether it is east or west longitude.

Extract longitude position: Read the binary value of bits 18-32 and convert it to a decimal longitude value.

Convert to latitude and longitude: Converts the extracted latitude and longitude values to the actual latitude and longitude information.

North and South Latitude Markers: Look at the 1st position, if it is 0, it is the north latitude, if it is 1, it is the south latitude.

Latitude Position: Extracts the values of bits 2-16 and converts them back to the original latitude.

Assuming the extracted value is X, the original latitude is X / (32767 / 90).

East-West Longitude Mark: Look at the 17th position, if it is 0, it is east longitude, if it is 1, it is west longitude.

Longitude Position: Extract the values of the 18th-32nd digits and convert them back to the original longitude.

Assuming the extracted value is Y, the original longitude is Y / (32767 / 180).

# Implementation considerations

- The address space remains the same: The NGID design uses only a subset of bits in the IP address to encode geolocation information without changing the total length of the address.

This means that existing network equipment and software can continue to use these addresses without any modifications.

- No need to modify existing protocols: Geolocation information is encoded within the existing address structure and does not require the introduction of new protocols or modifications to existing network protocol stacks.

- Backwards compatible: Newly designed addresses can be recognized and processed by legacy network devices that do not support NGI because these devices ignore specific bits used to encode geolocation.

- Transparency: For applications and services that do not require geolocation information, the newly designed address is no different from a normal IP address and can be used transparently.

- Optional: NGIDs are optional features that network administrators can choose to enable in the appropriate network environment without affecting other parts of the network that do not use these features.

- Simple address resolution: Geo-coding is simple and intuitive, making it easy to implement address resolution in existing systems without the need for complex conversion or mapping processes.

- Maintain network hierarchy: The design of the NGID takes into account the hierarchy of the existing network, ensuring that the assignment and management of addresses still follows the existing network architecture and policies.

# Security Considerations

## Security Risks

- Location tracking: If an attacker is able to access an NGID, they may track the physical location of the device, causing a breach of the user's privacy.

- Address mapping: By analyzing NGIDs, an attacker could construct an accurate map of the device's location, which could be used for inappropriate purposes, such as targeted attacks.

- Traffic analysis: Attackers may use geolocation information to analyze network traffic patterns to infer sensitive information.

- Identity association: If an NGID is associated with a specific person or organization, an attacker may use this information to build a profile of a user's behavior.

## Response

- Encryption: Encrypt NGIDs to ensure that only authorized network entities can parse and use this information.

- Anonymization: Use a mechanism to change the NGID periodically to prevent long-term tracking.

- Access control: Restrict access to NGIDs to ensure that only trusted network nodes can access this information.

- Network isolation: Establish logical or physical isolation between network devices that process NGIDs and other network devices to reduce the risk of leakage.

- Monitoring & Auditing: Implement monitoring systems to detect and record access to NGIDs for tracking and responding to security incidents as they occur.

- Laws and Policies: Formulate relevant laws and policies to regulate the use of NGID and protect user privacy.

# IANA Considerations

There is no need for IANA to make new digital resource allocations and related management issues.

# Acknowledgments
To Do

# References
To Do

# Author Information
To Do
