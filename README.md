# Overview

The information detailed in this document are to be used for Control-M v 9. 

# 1. Installation and Configuration

This document provides information about installing the xMatters (IT) for BMC Control-M Workload Automation integration. This document also contains complete instructions on how to configure xMatters, BMC Control-M, and the integration components.

Installing the integration service and updating the integration agent

To configure the integration agent for the BMC Control-M integration, you must copy the integration components into the integration agent; this process is similar to patching the application, where instead of copying files and folders one by one, you copy the contents of a single folder directly into the integration agent folder (<IAHOME>). The folder structure is identical to the existing integration agent installation, so copying the folder's contents automatically installs the required files to their appropriate locations. Copying these files will not overwrite any existing integrations. This integration includes the following components:


| Tables        | Are           |
| ------------- |---------------|
| bin/Controlm-APCclient.bat     | right-aligned |
| col 2 is      | centered      |
| zebra stripes | are neat      | 



Once you have installed the files and folders, you will need to modify the controlm-config.js and IAConfig.xml files to suit your deployment configuration.

Note: If you have more than one integration agent providing the BMC Control-M service, repeat the following steps for each one.

To install the integration service:

1. Copy all of the contents of the \components\integration-agent\ folder from the extracted integration archive to the <IAHOME> folder.

2. Open the IAConfig.xml file found in <IAHOME>\conf and add the following line to the “service-configs” section: <path>controlm20/controlm.xml</path>

3. Open the controlm-config.js file (now located in <IAHOME>\integrationservices\controlm20\ folder, and set the values for the following variables:
