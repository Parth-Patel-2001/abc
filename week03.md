# Week 3 | Computer Networks and the Internet

## Task 2. View Your Addresses

The following is a screenshot of Get Address:
![GitHub Screenshot Demo](./images/week3-task2-getaddress-part1.png)
![GitHub Screenshot Demo](./images/week3-task2-getaddress-part2.png)
![GitHub Screenshot Demo](./images/week3-task2-getaddress-part3.png)
![GitHub Screenshot Demo](./images/week3-task2-getaddress-part4.png)
![GitHub Screenshot Demo](./images/week3-task2-getaddress-part5.png)

## Network Addresses on My Computer

## IPv6 Addresses

### 1. `fe80::9a0d:2a05:ebb6:919f%39`
- **Interface Alias**: Ethernet
- **Description**: This is a **link-local IPv6 address** used for communication within the local network (like a home or office network). This address is automatically assigned to your Ethernet network adapter (the physical part that connects your computer to the network). It can only be used within your local network and can’t be accessed over the internet.

### 2. `fe80::87b:ca6:151f:d72e%10`
- **Interface Alias**: Local Area Connection* 3
- **Description**: This is another **link-local IPv6 address**. It’s assigned to a different network adapter on your computer. This address is no longer actively used (it’s marked as "deprecated"), meaning the adapter might not be in use or connected right now.

### 3. `fe80::bd73:17bb:e13:85a6%8`
- **Interface Alias**: Bluetooth Network Connection
- **Description**: This is a **link-local IPv6 address** assigned to the Bluetooth network connection on your computer. It helps your computer communicate with other Bluetooth devices, like wireless speakers or keyboards, but only over short distances.

### 4. `fe80::72fe:285b:d096:74b9%16`
- **Interface Alias**: Wi-Fi
- **Description**: This is a **link-local IPv6 address** assigned to your computer's Wi-Fi adapter. It allows your computer to communicate with other devices on the same Wi-Fi network. Like other link-local addresses, it can only be used in your local network.

### 5. `::1`
- **Interface Alias**: Loopback Pseudo-Interface 1
- **Description**: This is the **loopback address** (`::1`) for IPv6. It’s used for communication **inside** your computer. Think of it as a special address that always points back to your own machine. It’s useful for testing and debugging.

---

## IPv4 Addresses

### 1. `192.168.56.1`
- **Interface Alias**: Ethernet
- **Description**: This is a **private IPv4 address** assigned to your Ethernet adapter. It belongs to the `192.168.x.x` range, which is commonly used for home and office networks. This address can only be used within your local network (for example, it’s not reachable from the internet).

### 2. `169.254.127.29`
- **Interface Alias**: Local Area Connection* 3
- **Description**: This is an **APIPA (Automatic Private IP Addressing)** address. APIPA addresses are automatically assigned when your computer can’t get an IP address from a DHCP server (the server that assigns IP addresses). This address means your computer couldn’t connect to a network with a working DHCP server, so it assigned itself an address in the `169.254.x.x` range.

### 3. `169.254.7.199`
- **Interface Alias**: Bluetooth Network Connection
- **Description**: This is another **APIPA address** for the Bluetooth connection. Just like the previous one, it’s used when your computer can’t get an IP address from a network’s DHCP server.

### 4. `169.254.148.10`
- **Interface Alias**: Wi-Fi
- **Description**: This is another **APIPA address**, but assigned to the Wi-Fi adapter. It means the Wi-Fi adapter couldn’t get an IP address from a DHCP server, so it picked an address in the `169.254.x.x` range.

### 5. `127.0.0.1`
- **Interface Alias**: Loopback Pseudo-Interface 1
- **Description**: This is the **loopback address** (`127.0.0.1`) for IPv4. It is a special address that always points back to your own computer. Any network communication sent to this address will be processed by your computer without leaving it. It’s commonly used for testing or troubleshooting network services on your own machine.



## Task 3. Ping Your Local Router

## Objective

In this task, I used PowerShell to find the IP address of my local (default) router and ping it to measure the delay between my computer and the router. I recorded the command outputs, explained the delay values, and discussed the factors that impact delay.

## 1. Find the IP Address of My Local Router

### Command Used

To find the IP address of my default router (also known as the default gateway), I used the following PowerShell command:

Get-NetRoute -DestinationPrefix "0.0.0.0/0"

## 2. Ping the Router

### Command Used
After identifying the router's IP address, I used the Test-Connection cmdlet to ping the router:

Test-Connection $gatewayIP<br>
(Here, ***$gatewayIP*** is the IP address of the router, obtained from the previous step.)

## 3. Command Output
### IP Address of the Router
The output of the Get-NetRoute -DestinationPrefix "0.0.0.0/0" command showed that the default gateway (router IP address) is 172.20.10.1.

### Ping Results
After pinging the router, the following results were returned:

PS C:\Users\Archana> Test-Connection $gatewayIP

Ping to 172.20.10.1 with 32 bytes of data:<br>
Reply from 172.20.10.1: bytes=32 time=6ms<br> 
Reply from 172.20.10.1: bytes=32 time=11ms <br>
Reply from 172.20.10.1: bytes=32 time=5ms<br>
Reply from 172.20.10.1: bytes=32 time=4ms 

Ping statistics for 172.20.10.11:
    Approximate round trip times in milli-seconds:
        Minimum = 4ms, Maximum = 11ms, Average = 6ms

## 4. Analysis of Delay Values
### Delays:
Minimum Delay: 4ms <br>
Maximum Delay: 11ms<br>
Average Delay: 6ms<br>

These values were directly provided by the Test-Connection cmdlet in the Time(ms) column of the ping results. The minimum delay is the fastest time recorded, the maximum delay is the longest time, and the average delay is the mean value of all ping responses.

### How the Delays Were Found
The delay values were provided by the Test-Connection cmdlet after pinging the router. The command output includes the round-trip time for each ping request in milliseconds. The minimum, maximum, and average delay values were found by looking at these times.


## 5. Factors That Impact Delay and Why Delays May Vary Over Time
Several factors can contribute to delays in network communication, and they may vary over time. These include:

### 5.1 Network Traffic
Impact: High network traffic from other devices or processes can cause congestion, increasing delay. When more devices are accessing the network simultaneously, the available bandwidth is shared, which may slow down packet delivery.
### 5.2 Wi-Fi vs. Wired Connection
Impact: If you are using Wi-Fi to connect to the router, signal strength and interference can affect the delay. A wired Ethernet connection tends to have more stable and lower latency.
### 5.3 Router Load
Impact: If the router is handling a large number of devices or heavy traffic (such as video streaming or gaming), the router's processing capacity can cause delays in responding to ping requests.
### 5.4 Distance from Router
Impact: The physical distance between your device and the router, especially in a Wi-Fi setup, can affect the signal quality and the time it takes for data to be transmitted and received.
### 5.5 Firewall or Security Settings
Impact: Routers or computers may have firewalls or security settings that either slow down or block ping responses. Some routers may block ICMP traffic to protect against potential network attacks.
### 5.6 ISP and External Network Conditions
Impact: While not directly related to local ping tests, any network issues with your Internet Service Provider (ISP) can indirectly affect the delay by impacting the overall routing and connectivity.<br>

### The delays observed in ping tests may vary over time due to several reasons:

### Network Load:
As more devices join the network or as network usage increases, delays can increase due to congestion and bandwidth sharing.
### Router Status:
If the router is under heavy load, rebooting, or experiencing a high number of requests, it may take longer to respond to ping requests, increasing the delay.
### Environmental Factors:
In Wi-Fi networks, physical obstructions (walls, furniture, etc.) or interference from other wireless networks and devices can impact signal strength, leading to fluctuations in delay.

The following is a screenshot of Ping Local Router:
![GitHub Screenshot Demo](./images/week3-task3-pingLocalRouter.png)

## Task 4. Browse to OpenWRT Websites
Include your journal entry here.
## Task 5. Academic Intetrity Policy
[Academic integiry policy](./images/integrity.pdf)
