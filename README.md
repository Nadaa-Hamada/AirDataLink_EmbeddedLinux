# AirDataLink_EmbeddedLinux
The goal of this project is to send data wirelessly (over air) between two embedded systems while ensuring data integrity using CRC validation.

## 📖 Project Overview
**QNX-Linux-DataBridge** is an embedded systems project designed to demonstrate wireless data transmission between two systems — one running **QNX** and the other running **Yocto Embedded Linux**.  
The communication uses the **SOME/IP** protocol, with **CRC (Cyclic Redundancy Check)** ensuring the integrity of transmitted data.

---

## 🧩 System Architecture

+----------------+
| PC Host |
| (Ubuntu/Linux) |
+--------+-------+
|
| FTP
v
+----------------+
| QNX VM | (acts as Raspberry Pi 1)
| - Receives data from PC
| - Calculates CRC
| - Sends data + CRC via SOME/IP
+--------+-------+
|
| SOME/IP
v
+----------------+
| Raspberry Pi 2 |
| (Yocto Linux) |
| - Receives data + CRC
| - Recalculates CRC
| - Compares CRCs for integrity
+----------------+


---

## ⚙️ System Requirements

### Hardware
- PC (Ubuntu/Linux) for development and virtualization  
- 1 × Raspberry Pi 4 (with Yocto Linux)  
- Stable network connection (Ethernet/Wi-Fi)

### Software
- **QNX Neutrino RTOS** (running in VirtualBox/VMware)  
- **Yocto Embedded Linux** on Raspberry Pi  
- **vsomeip** library for SOME/IP communication  
- **FTP client/server** (e.g., FileZilla, vsftpd)  
- **GCC / QNX Momentics IDE** for compiling C/C++ code  
- **Python or C/C++** for CRC calculation  
- **Git & GitHub** for version control

---

## 📡 Communication Workflow

1. **File Transfer (FTP):**  
   The PC sends a data file to the QNX VM through FTP.

2. **CRC Calculation (QNX):**  
   The QNX system computes a **CRC checksum** for the received data to ensure its integrity.

3. **Data Transmission (SOME/IP):**  
   The QNX system sends the **data + CRC** over the air using the **SOME/IP protocol** to the Yocto-based Raspberry Pi.

4. **CRC Verification (Yocto):**  
   The Yocto system receives the data, recalculates the CRC, and compares it with the received checksum.  
   - If they match → ✅ *Data Verified*  
   - If not → ❌ *Data Corrupted*

---

## 🧮 CRC Function

The **Cyclic Redundancy Check (CRC)** is used to detect accidental changes in data during transmission.  
The sender computes a CRC value before sending the data.  
The receiver computes it again upon receiving the data — if both values match, the data is verified as correct.

## Tools & Technologies
Category	Tools / Technologies
OS	QNX Neutrino RTOS, Yocto Linux
Protocols	SOME/IP, FTP
Programming	C/C++, Python
Libraries	vsomeip, zlib
Development Tools	QNX Momentics IDE, GCC, Git
Virtualization	VirtualBox / VMware

## How to Run the Project

Setup QNX VM

Install QNX in a virtual machine.

Configure the network interface (NAT or Bridged).

Setup Yocto Linux

Flash Yocto onto your Raspberry Pi.

Ensure it can communicate with your PC via the network.

Setup FTP

Install and configure an FTP server on your PC.

Send a test file from the PC to the QNX VM.

Implement CRC

Write a small program to calculate CRC on the sender (QNX) side.

Implement CRC verification on the receiver (Yocto) side.

Setup SOME/IP

Install and configure the vsomeip library on both systems.

Create a service-client communication setup.

Send the file + CRC from QNX → Yocto.

Verify Data Integrity

Compare the CRC values on both systems.

Print “Data Verified” or “Data Corrupted” in terminal logs.

## 🔒 Future Enhancements

Implement encryption for secure data transmission.

Add acknowledgment and retransmission mechanism.

Build a Qt-based GUI for file monitoring.

Visualize transmission stats (speed, reliability, retries).

## 👩‍💻 Contributors
Nada Hamada
Embedded Systems Trainee @ Brightskies

## Project Status

✅ Repository initialized
🔜 CRC calculation implementation
🔜 SOME/IP setup between QNX VM and Raspberry Pi
🔜 Testing and verification phase

## References

vsomeip Documentation
QNX Neutrino RTOS
Yocto Project
