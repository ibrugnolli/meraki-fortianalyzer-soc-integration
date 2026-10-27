# meraki-fortianalyzer-soc-integration

## Introduction

Welcome to the Cisco Meraki MX to FortiAnalyzer integration guide. This project includes a custom parser designed to accurately translate and map Meraki MX event types and parameters into FortiAnalyzer, alongside comprehensive documentation to walk you through the entire deployment process.

## Overview

The FortiAnalyzer Security Automation Service is a license that provides content packs released from FortiGuard on a monthly basis. The content packs include premium reports, alert handlers, advanced correlation rules, third-party log parsers, and more. These tools are designed to help you detect, investigate, and respond to security incidents. For more information about this service, see FortiAnalyzer Security Automation Service on the FortiGuard website.

Cisco Identity Services Engine logs
FortiAnalyzer supports normalizing Cisco Identity Services Engine logs as Fabric logs.

This log parser enables FortiAnalyzer to parse Cisco Identity Services Engine (ISE) authentication-authorization-accounting syslogs, and normalize user, device, and policy fields into SIEM data. It also provides full AAA visibility through comprehensive field extraction.

## Enviroment Requirements

FortiAnalyzer 7.6.4 or later
FortiAnalyzer SOC Automation Service valid license

## Instalation Requirements

1. Verify your FortiAnalyzer current Firmware Version.
2. Verify that your FortiAnalyzer system time is udpate and in sync.

![image alt text](images/image001.jpg)

3. Verify that your FortiAnalyzer in fylly connected and registered with Forticare Support, and that you have a valid SOC Automation Service license.

![image alt text](images/image002.jpg)

4. Verify that your Fortianalyzer conection with Fortiguard is healthy

![image alt text](images/image003.jpg)

The FortiAnalyzer Security Automation Service includes support for the RHSP FortiGuard package which is used to share updated reports, alert handlers, SIEM parsers, and connectors as content packages. RHSP FortiGuard package objects are only applied with a valid Security Automation Service license.

* Reports: Go to Reports > Report Definitions > All Reports.
Reports included in the RHSP package are stored on the global level. They are displayed in the global Security Automation Reports folder. The global folder and global reports are identified with the system theme's color applied to the icon. Reports delivered by the RHSP package are displayed with Origin = FortiGuard.

* Alert handlers: Go to Incidents & Alerts > Alert Handlers > Alert Handlers.
Alert handlers delivered by the RHSP package are displayed with Origin = FortiGuard.

* Connectors: Go to Incidents & Alerts > Automation > Active Connectors.
You will need to create and configure the connector for your environment. 

* SIEM parsers: Go to Incidents & Alerts > Log Parsers > Log Parsers.
A carefully curated selection of log parsers, delivered by the RHSP package are displayed with Origin = FortiGuard. There parsers make the integration with non-Fortinet devices efforless and eficient.

5. To review the list of Third-Party log parsers from the Content Packs, go to Incidents & Alerts > FortiGuard Services > SOC Automation:

![image alt text](images/image004.jpg)

6. Search for the Cisco Meraki parser:

![image alt text](images/image005.jpg)

