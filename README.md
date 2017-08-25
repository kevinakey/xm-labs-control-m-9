# Overview

The information detailed in this document are to be used for Control-M v 9. 

# 1. Installation and Configuration

This document provides information about installing the xMatters (IT) for BMC Control-M Workload Automation integration. This document also contains complete instructions on how to configure xMatters, BMC Control-M, and the integration components.

Installing the integration service and updating the integration agent

To configure the integration agent for the BMC Control-M integration, you must copy the integration components into the integration agent; this process is similar to patching the application, where instead of copying files and folders one by one, you copy the contents of a single folder directly into the integration agent folder (<IAHOME>). The folder structure is identical to the existing integration agent installation, so copying the folder's contents automatically installs the required files to their appropriate locations. Copying these files will not overwrite any existing integrations. This integration includes the following components:

* **bin/Controlm-APClient.bat** & **bin/Controlm-APClient-Del.bat**
Batch files targeted by the SHOUT destinations from within Control-M. They take the SHOUT message and call APClient.bin.exe with the correct map-data for either the controlm20 service or the del service, depending on which SHOUT destination was used

* **conf/deduplicator-filter.xml**
The filtering mechanism used to suppress duplicate messages. By default, the filter checks the job_name, status and run_num values; if they are all the same within a two minute window, only the first message will be sent through to xMatters.

* **controlm-config.js:** The main configuration file for the integration; includes API connection information and user information.

* **bmccontrolm.pwd:** Stores the password for the Control-M API user used by the integration service. If you change the name of this file, you must also update the controlm-config.js files to point to the correct password file.


Once you have installed the files and folders, you will need to modify the controlm-config.js and IAConfig.xml files to suit your deployment configuration.

_**Note:** If you have more than one integration agent providing the BMC Control-M service, repeat the following steps for each one._

**To install the integration service:**

1. Copy all of the contents of the \components\integration-agent\ folder from the extracted integration archive to the <IAHOME> folder.

2. Open the IAConfig.xml file found in <IAHOME>\conf and add the following line to the “service-configs” section: <path>controlm20/controlm.xml</path>

3. Open the controlm-config.js file (now located in <IAHOME>\integrationservices\controlm20\ folder, and set the values for the following variables:
   * **CONTROL_M_USER:** The user name to be used for the BMC Control-M API Server; default value is "username".
   * **CONTROL_M_HOST_NAME:** Hostname of the BMC Control-M API Server; default value is "localhost".
   * **CONTROLM_PASSWORD_FILE:** Location of the password file for the API user; default value is "conf/bmccontrolm.pwd".
   * **CTMEMAPI_PROPERTIES_FILE:** Location of the CTMEMAPI_PROPERTIES_FILE; default value is "integrationservices/controlm20/ctmemapi.properties". For more information about this setting, see the following section, "Installing Control M/EM API server properties files"
   * **JACORB_PROPERTIES_FILE:** Location of the JACORB_PROPERTIES_FILE; default value is "integrationservices/controlm20/jacorb.properties". For more information about this setting, see the following section, "Installing Control M/EM API server properties files".
   * **SLEEP_PERIOD_BETWEEN_CALLBACK:** The amount of time (in milliseconds) to sleep between receiving a SHOUT Message and making the callback to the BMC Control-M API for the job details. (Default is 3000, or three seconds.)
   * **DEDUPLICATOR_FILTER:** Name of the deduplicator filter; i.e., the attribute name for the element filter in the deduplicator-filter.xml file. The default value is controlm20.

4. Save and close the file.

5. Open the Controlm-APClient.bat and Controlm-APClient-Del.bat files (now located in <IAHOME>\bin ) in a text editor, and change the value for the "IAHOME" variable to the location of the <IAHOME>\bin folder on your machine. (The default is C:\PROGRA~1\xmatters\integrationagent\bin ).

6. Save and close the files.

7. Restart the integration agent. 

On Windows, the integration agent runs as a Windows Service; on Unix, it runs as a Unix daemon
