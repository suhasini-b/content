# Microsoft Windows Logs

This pack includes Cortex XSIAM content.

Notes: 
 - The logs will be stored in the dataset named *microsoft_windows_raw*.
 - The pack currently supports the following data source: "Security" and "System".

To view logs only from the Windows Event log, apply the following filter to the datamodel query: *| filter xdm.observer.type="Microsoft-Windows-Security-\*" or xdm.event.type="System"*


## Collect Events from Vendor

In order to use the collector, you can use one of the following options:       
    - [Broker VM (Windows Event Collector)](#broker-vm-windows-event-collector)   
    - [XDRC (XDR Collector)](#xdrc-xdr-collector)
   


### Broker VM (Windows Event Collector)
To create or configure the Broker VM, use the information described [here](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Pro-Administrator-Guide/Configure-the-Broker-VM).


To connect and use Windows Event Collector, use the information described [here](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Pro-Administrator-Guide/Activate-the-Windows-Event-Collector).

### XDRC (XDR Collector)

To create or configure the Filebeat collector, use the information described [here](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/Cortex-XDR-Pro-Administrator-Guide/XDR-Collectors).


As Cortex XSIAM provides a YAML template for Windows Security Event Logs, you can use the following steps to create a collection profile:

 1. In Cortex XSIAM, select **Settings** → **Configurations** → **XDR Collectors** → **Profiles** → **+Add Profile** → **Windows**.
 2. Select **Winlogbeat**, then click **Next**.
 3. Configure the General Information parameters:
   - Profile Name — Specify a unique Profile Name to identify the profile. The name can contain only letters, numbers, or spaces, and must be no more than 30 characters. The name you choose will be visible from the list of profiles when you configure a policy.

   - Add description here — (Optional) Provide additional context for the purpose or business reason that explains why you are creating the profile.

4. You can use one of the following options to collect event logs using the XDR Collectors:
#### Option A
If you wish to collect only **Security** logs please select the "Windows Security" template located in the **Select Template** drop-down. After selecting the template press **Add**.

#### Option B
In the **Winlogbeat Configuration File** section, add the following YAML template to collect **Security** and **System**:
 ```bash
  winlogbeat.event_logs:
  - name: Security
    ignore_older: 1h
  - name: System
    ignore_older: 1h  
```

**Note:** You can customize what will be collected by removing the "name" and "ignore_older" lines of the specific event type.

5. Press **Create** to save the new template.
