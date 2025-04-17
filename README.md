![MIT License](https://img.shields.io/badge/License-MIT-yellow.svg)
# Automotive Software-Defined Firewall (SDF) Framework
A comprehensive framework for implementing Software-Defined Firewalls (SDF) in automotive Electronic Control Units (ECUs) to enhance security, control, and management of inter-ECU communications.

## Description
This project extends the original [VirtualECU](https://github.com/pschichtel/VirtualECU) repository to focus on the implementation and validation of a Software-Defined Firewall (SDF) specifically designed for securing communication between automotive ECUs. The SD-Firewall protects against unauthorized access, malicious communication, and cybersecurity threats in a virtual automotive network using customized firewall rules. The project runs on a Linux-based virtual environment using Scala, SBT, SocketCAN, and CAN-utils, simulating a robust automotive communication system.

## Key Features:
- Virtual ECU Simulation: Provides a virtual environment for testing firewall rules and ECU interactions without requiring physical hardware.
- Python-Based Firewall: Controls and manages the flow of data between virtual ECUs, enforcing allow/block rules based on security requirements.
- Virtual CAN Networks (vCAN): Simulates the in-vehicle communication system for ECUs, allowing for realistic testing.
- Logging and Monitoring: Captures detailed logs for analysis, ensuring the firewall operates as expected.
- Attack Simulations: Test the firewall under various cybersecurity threat scenarios to ensure robustness and resilience.

<table>
  <tr>
    <td>
      <h3>Scenario 1</h3>
      <p>Central Gateway ECU with four vCAN Interface and Firewall Protection</p>
      <img src="https://github.com/shubodaya/SD-Firewall-for-Automotive-Network/blob/9c22ed6455bd7f93e630385eab1821409371cebb/SDFW/Scenario1-Shared-vCAN/Scenario1.png" alt="Central Gateway ECU with four vCAN Interface" width="350" />
    </td>
    <td>
      <h3>Scenario 2</h3>
      <p>Central Gateway ECU with eight vCAN Interface and Firewall Protection</p>
      <img src="https://github.com/shubodaya/SD-Firewall-for-Automotive-Network/blob/e9c04540c2470499b97b86a1172976e11856c028/SDFW/Scenario2-Dedicated-vCAN/Scenario2.png" alt="Central Gateway ECU with eight vCAN Interface" width="380" />
    </td>
  </tr>
</table>

## Project Objectives
The goal is to develop a firewall framework that:
* Controls communication between critical ECUs in a vehicle, such as the ABS, ECM, ADAS, and more.
* Protects against potential cybersecurity threats by implementing custom firewall rules for specific ECUs.
* Allows for scalable and flexible testing of automotive firewalls in a virtual environment.



## Methodology
1. System Design
The project begins by identifying key automotive ECUs (ABS, ACM, BCM, ECM, ICU, TCM, and ADAS) that require specific firewall rules to secure communication. The firewall is designed to manage the data flow between these virtual ECUs and mitigate cybersecurity threats.

2. Virtual Environment Setup
Using Scala, SBT, and Linux, a virtual network of ECUs is created where vCAN interfaces simulate real-world communication channels. SocketCAN and CAN-utils are used for monitoring and controlling the CAN traffic.

3. Firewall Implementation
The firewall is developed using Python, where custom rules are written to allow/block communication between ECUs based on security needs. These rules ensure that only necessary and secure communications are allowed, while all suspicious or irrelevant traffic is blocked.

4. Testing and Validation
To validate the effectiveness of the firewall, traffic between the ECUs is simulated under different attack scenarios. The performance of the firewall is observed to ensure that it correctly enforces the rules and blocks unauthorized access.

5. Log Analysis
Event logs from vCAN networks are collected and analyzed to assess the firewall's performance. Any anomalies detected are used to refine the firewall rules.

## Components
Virtual ECUs
This project simulates the following ECUs:
* Anti-lock Brake System (ABS)
* Airbag Control Module (ACM)
* Body Control Module (BCM)
* Engine Control Module (ECM)
* Infotainment Control Unit (ICU)
* Transmission Control Module (TCM)
* Advanced Driver Assistance Systems (ADAS)
Each ECU represents key vehicle functions and security requirements, ensuring that the firewall is tailored for realistic and complex automotive scenarios.

## Virtual CAN (vCAN) Network
Virtual CAN networks (vCAN) are used to simulate data communication between the ECUs. These virtual networks allow real-time monitoring and testing of ECU traffic, enabling effective testing of the firewall rules.

## Installation
Prerequisites
* Linux-based environment with at least 8 GB RAM for optimal performance.
> 💡 **Tip:** If you have limited RAM, you can check with 2-3 ECUs instead of all seven.
* Python 3.12.3
* Scala and SBT for virtual ECU simulation
* SocketCAN and CAN-utils for CAN communication


## Setup Instructions
1. Install Git if not already installed and clone repository.
```
sudo apt install git -y
```
2. Clone the repository:
```
git clone https://github.com/shubodaya/SD-Firewall-for-Automotive-Network.git
cd SD-Firewall-for-Automotive-Network
cd Scenario1-Shared-vCAN
```
For the second scenario
```
cd Scenario2-Dedicated-vCAN
```
> **_Note:_** You can test one scenario at a time. Make sure to run either Scenario 1 or Scenario 2 to avoid conflicts between shared and dedicated vCAN interfaces.

2. Install the required packages:
```
sudo apt update && sudo apt upgrade -y
sudo apt install openjdk-17-jdk
sudo apt install scala -y
sudo apt-get install sbt
sudo apt install can-utils
sudo apt-get install linux-modules-extra-$(uname -r)
sudo apt-get update
```
4. Set up Scala and SBT for virtual ECU simulation.
```
# Install sbt (Scala build tool) from https://www.scala-sbt.org/download/
echo "deb https://repo.scala-sbt.org/scalasbt/debian all main" | sudo tee /etc/apt/sources.list.d/sbt.list
echo "deb https://repo.scala-sbt.org/scalasbt/debian /" | sudo tee /etc/apt/sources.list.d/sbt_old.list
curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | sudo apt-key add
or
curl -fsSL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | gpg --dearmor -o /etc/apt/trusted.gpg.d/sbt.gpg
```

6. Configure and launch SocketCAN and vCAN interfaces for network communication.
```
sudo modprobe vcan
sudo ip link add dev vcan0 type vcan | sudo ip link set up vcan0
sudo ip link add dev vcan1 type vcan | sudo ip link set up vcan1
sudo ip link add dev vcan2 type vcan | sudo ip link set up vcan2
sudo ip link add dev vcan3 type vcan | sudo ip link set up vcan3
sudo ip link add dev vcan4 type vcan | sudo ip link set up vcan4
sudo ip link add dev vcan5 type vcan | sudo ip link set up vcan5
sudo ip link add dev vcan6 type vcan | sudo ip link set up vcan6
sudo ip link add dev vcan7 type vcan | sudo ip link set up vcan7
```
8. Run SBT
```
sbt clean
sbt update
sbt compile
```
* Scenario 1:
Open separate terminal tabs for each ECU and run the following commands:
```
sudo sbt "runMain tel.schich.virtualecu.Main vcan0 abs.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan1 acm.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan2 adas.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan1 bcm.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan0 ecm.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan1 icu.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan0 tcm.yaml"
```
* Scenario 2: 
Again, open separate terminal tabs for each ECU and run the following commands:
```
sudo sbt "runMain tel.schich.virtualecu.Main vcan0 abs.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan1 ecm.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan2 tcm.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan3 acm.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan4 bcm.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan5 icu.yaml"
sudo sbt "runMain tel.schich.virtualecu.Main vcan6 adas.yaml"
```
> **_Note:_** You can test one scenario at a time. Make sure to run either Scenario 1 or Scenario 2 to avoid conflicts between shared and dedicated vCAN interfaces.

9. Run the firewall script:
Again, open a separate terminal tab to run the firewall:
```
python3 -m venv myenv
source myenv/bin/activate
python3 main.py
```
10. Send CAN messages to interfaces
```
cansend vcan0 7E2#02010A00 
cansend vcan1 7E0#02010500
cansend vcan2 7E1#02010A00
cansend vcan3 7D4#02040100
cansend vcan4 7C2#02060100
cansend vcan5 7B8#02010500 
cansend vcan6 7E4#02011000
```

## Log Analysis
After running the scenarios, analyze the logs generated by the firewall and virtual ECUs to understand communication details and evaluate firewall effectiveness:
* Log Monitoring: Review log files for timestamps, source/destination messages, and whether communications were allowed or blocked.
* Identify Anomalies: Look for any unexpected behavior, such as messages being incorrectly blocked or allowed, and refine the firewall rules as needed.
* Performance Evaluation: Assess the firewall's response time to incoming CAN messages to ensure efficient processing.
* Iterate and Refine: Adjust firewall rules based on your findings to enhance performance and security.
* Documentation: Document any changes made to the rules for future reference.

This analysis ensures that the firewall functions as intended and strengthens the security of the automotive network.



## Usage
* To test with different scenarios, connect multiple ECUs to their respective vCANs and ensure that they are configured correctly in the environment. This allows for comprehensive testing of the firewall's effectiveness across various use cases.
* Customize the firewall rules and interface configurations in the "main.py" and "firewall_dict.py" files to meet your specific requirements.
* Simulate traffic between the virtual ECUs and monitor the log files for communication details and firewall performance.
* Use CAN-utils for additional monitoring and CAN frame operations.

## Changes from the Original VirtualECU
* Custom configurations and YAML files for specific ECU interactions and firewall rules.
* Enhanced monitoring and logging features for CAN traffic and firewall performance analysis.
* Updated components for better integration and improved functionality in testing firewalls within the virtual environment.

## Attribution
This work is based on the [VirtualECU](https://github.com/pschichtel/VirtualECU) project by pschichtel. Modifications have been made to adapt the framework to the development and testing of firewalls for automotive ECU security.

## License
This project is licensed under the GNU General Public License v3.0. See the LICENSE file for more details.

## Future Work
The project will be expanded with additional features:
* Integration of physical ECUs for real-world testing.
* Enhanced attack simulations for better testing of firewall robustness.
* Machine learning-based firewall rule adaptation.




