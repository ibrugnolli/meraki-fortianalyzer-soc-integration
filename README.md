# meraki-fortianalyzer-soc-integration



## Introduction

Welcome to the Cisco Meraki MX to FortiAnalyzer integration guide. This project provides procedures to properly configure the FortiGuard SOC Automation third-party log parser, set up a Cisco Meraki MX device to export syslog messages to FortiAnalyzer, and deploy a custom parser designed to accurately translate and map Meraki MX event types and parameters. Comprehensive documentation is included to walk you through the entire deployment process.

![image alt text](images/intro.jpg)


## Overview

The FortiAnalyzer SOC Automation service is a licensed feature that provides monthly content packs released by FortiGuard. These content packs include premium reports, alert handlers, advanced correlation rules, third-party log parsers, and other tools designed to help you detect, investigate, and respond to security incidents. For more information, see the FortiAnalyzer Security Automation Service on the FortiGuard website.


## Environment Requirements

1. Cisco Meraki MX device (tested with MX67 running version MX 26.2.3)
2. FortiAnalyzer 7.6.4 or later with valid license and register to FortiGuard (teste with version v8.0.2 build0198)
3. FortiAnalyzer SOC Automation Service valid license


## Environment Diagram Overview

The Cisco Meraki MX device nust be able to send UDP syslog messages (port 514) to Fortinet FortiAnalyzer ip address.
In this demo scenario, the MX device is using the ip address of the WAN interface to communicate with FortiAnalyzer.

![image alt text](images/image001.jpg)


## Installation Requirements

1. Verify your FortiAnalyzer current Firmware Version. Also,verify that your FortiAnalyzer system time is update and in sync.

![image alt text](images/image002.jpg)

2. Verify that your FortiAnalyzer in fully connected and registered with Forticare Support, and that you have a valid SOC Automation Service license.

![image alt text](images/image003.jpg)

3. Verify that your Fortianalyzer connection with Fortiguard is healthy

![image alt text](images/image004.jpg)

The FortiAnalyzer Security Automation Service includes support for the RHSP FortiGuard package which is used to share updated reports, alert handlers, SIEM parsers, and connectors as content packages. RHSP FortiGuard package objects are only applied with a valid Security Automation Service license.

* Reports: Go to Reports > Report Definitions > All Reports.
Reports included in the RHSP package are stored on the global level. They are displayed in the global Security Automation Reports folder. The global folder and global reports are identified with the system theme's color applied to the icon. Reports delivered by the RHSP package are displayed with Origin = FortiGuard.

* Alert handlers: Go to Incidents & Alerts > Alert Handlers > Alert Handlers.
Alert handlers delivered by the RHSP package are displayed with Origin = FortiGuard.

* Connectors: Go to Incidents & Alerts > Automation > Active Connectors.
You will need to create and configure the connector for your environment. 

* SIEM parsers: Go to Incidents & Alerts > Log Parsers > Log Parsers.
A carefully curated selection of log parsers, delivered by the RHSP package are displayed with Origin = FortiGuard. There parsers make the integration with non-Fortinet devices effortless and efficient.

4. To review the list of Third-Party log parsers from the Content Packs, go to Incidents & Alerts > FortiGuard Services > SOC Automation:

![image alt text](images/image005.jpg)

5. Search for the Cisco Meraki parser:

![image alt text](images/image006.jpg)

6. Install Third-Party Log Parser: After verifying that you SOC automation addon is in sync with Fortiguard Content Packs, go to Incidents & Alerts > Log Parsers > Log Parsers in order to install the Cisco Meraki MX Firewall parser.

7. Click on "Uninstalled Log Parsers" to verify the list of Third-Party log parsers available:

![image alt text](images/image007.jpg)

8. Search for "Cisco Meraki Firewall Log Parser" and click *Install* 

![image alt text](images/image008.jpg)

9. Move the Cisco parser to the top of the screen. Verify the parser origin as *FortiGuard*

![image alt text](images/image009.jpg)

10. Now, your Fortianalyzer is ready to start receiving and properly parser Cisco Meraki MX syslog messages.
In case your FortiAnalyzer supports ADOM´s, it´s recommended that you create a new ADOM to integrate the Cisco Meraki MX device via syslog. We will proceed with the creation of the new ADOM.
Go to the main dashboard screen, and click on the *ADOM:root* button.

![image alt text](images/image010.jpg)

11. Click on *Create New ADOM*

![image alt text](images/image011.jpg)

12. Create a name (ex *MERAKI_INTEGRATION*), and select the type *FABRIC*. Make sure also to select the proper timezone, and click *OK*

![image alt text](images/image012.jpg)

13. After the creation of the new ADOM, click on it to select and change to the new ADOM.

![image alt text](images/image013.jpg)

14. Repeat the steps described above to select the Cisco Meraki MX parser, install and move it to the top of the list as shown below:

![image alt text](images/image014.jpg)

15. Now your Fortianalyzer system and proper ADOM is ready to start receiving syslog messages from the Cisco Meraki device.


## Cisco Meraki MX device Setup steps:

1. Login into your Cisco Meraki dashboard. Select the proper *Organization* and *Network*. Go to *Security & SD-WAN -> Appliance Status -> Uplink* to verify your MX device status, firmware version, and WAN IP address. In *Tools* you can also use the ping to verify it the interface can reach the FortiAnalyzer ip address (192.168.88.82)

![image alt text](images/image015.jpg)

2. In order to enable sending syslog messages to FortiAnalyzer, go to *Network-Wide -> General*. Look for the section *Logging* and create a syslog entry, using the FortiAnalyzer ip address as *Server Address*. Keep the default port and protocol. Select the required Roles, and click *Update syslog servers*

![image alt text](images/image016.jpg)

3. Go to *Network-Wide ->Alerts* to select the alerts that will be enabled and generate logging messages.

![image alt text](images/image017.jpg)

4. Go to *Security & SD-WAN -> Threat Protection*. Enable AMP and IDS/IPS features, in order to trigger the security engines and generate security log messages.

![image alt text](images/image018.jpg)

5. Go to *Security & SD-WAN -> Content Filtering*. Enable a content category to block for testing purpose (ex. *Tobacco*).

![image alt text](images/image019.jpg)

6. Now, we need to trigger the security engines and content filtering by simulating traffic passing through the Meraki MX device. Some events will be displayed under *Network-Wide -> Monitor -> Event Log*, and security engine event will be displayed under *Security & SD-WAN -> Monitor -> Security Center -> MX Events*.

![image alt text](images/image020.jpg)

![image alt text](images/image021.jpg)

7. You can also verify that the Meraki MX device is sending syslog messages to the FortiAnalyzer, using the Packet Capture. Go to *Network-Wide -> Packet Capture*.

![image alt text](images/image022.jpg)

8. Now that your Cisco Meraki MX device is proper setup and sending syslog messages, lets return to the FortiAnalyzer dashboard and setup the device.

## Adding Cisco Meraki MX as an FortiAnalyzer authorized device:

Once your Cisco Meraki MX starting sending syslog messages to the FortiAnalyzer, this device is displayed in the root ADOM as unauthorized devices. You can quickly view unauthorized devices by clicking Unauthorized Devices in the quick status bar. You must authorize the devices before FortiAnalyzer can start receiving logs from the devices.

Because in this scenario, we are using ADOM's, you must assign the device the ADOM created before (ex.*MERAKI_INTEGRATION*).

1. Right click in the unauthorized device, and select *Authorize*.

![image alt text](images/image023.jpg)
 
2. The Authorize Device dialog box opens. Select the ADOM in the Add the following device(s) to ADOM list and click OK.

![image alt text](images/image024.jpg)

![image alt text](images/image025.jpg)

3. Once the device is authorized and the FortiAnalyzer receives syslog messages, it will update the status *UP*.

![image alt text](images/image026.jpg)

4. Wait a couple of minutes, then navigate to Incidents & Alerts > Log Parsers > Assigned Parsers. Verify that FortiAnalyzer automatically creates a new assignment using the Cisco Meraki Firewall Log Parser. This confirms that the system has successfully interpreted and parsed the incoming messages. 

![image alt text](images/image027.jpg)

5. Navigate to Log View > Logs > All. Using the filter, find all the logs containing *Cisco*.

![image alt text](images/image028.jpg)

![image alt text](images/image029.jpg)

![image alt text](images/image030.jpg)


## Using a Cisco Meraki MX custom parser:

Third-party parsers provided by FortiGuard establish a baseline for SOC analysts to begin integrating external devices into FortiAnalyzer. This custom parser extends that foundational work, offering deeper interpretation and mapping of the *event_type* messages available in the latest firmware releases of Cisco Meraki MX devices.

The json parser provided here will help you achieve further interpretation of the Cisco Meraki MX device.



Navigate to Incidents & Alerts > Log Parsers > Log Parsers, and click *Create New*.

![image alt text](images/image031.jpg)

Simplify Copy&Paste the json content in the following screen and click *Apply*.

![image alt text](images/image032.jpg)

![image alt text](images/image033.jpg)

![image alt text](images/image034.jpg)

![image alt text](images/image035.jpg)

![image alt text](images/image036.jpg)
