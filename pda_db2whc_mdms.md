---

copyright:
  years: 2014, 2019
lastupdated: "2018-06-15"

keywords:

subcollection: Db2whc

---

<!-- Attribute definitions -->
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}

# Migrating from IBM PureData System for Analytics (Netezza)
{: #pda}

The {{site.data.keyword.Bluemix_notm}} Mass Data Migration Service (MDMS) can be used to migrate data from large IBM PureData Systems for Analytics (Netezza) databases of about 25 TB and greater to a fully managed {{site.data.keyword.dashdblong}} database on {{site.data.keyword.Bluemix_notm}}.

MDMS offers a fast, simple, secure way to physically transfer terabytes to petabytes of data to the {{site.data.keyword.Bluemix_notm}}. The MDMS is a mobile storage device with 120 TB of usable storage capacity. This device gives you the ability to overcome common transfer challenges like high costs, long transfer times, and security concerns – all in a single service.
{: shortdesc}

![View of the Mass Data Migration Service device](images/mdms.svg)

## What you need when requesting a device
{: #prereq}

1. Network settings for the storage device
   - Static IP address
   - Netmask for enabling the data transfer
2. Network settings for remote computer
   - Static IP address
   - Netmask 
   - Default Gateway to access the user interface (UI)
3. Cloud Object Storage download destination <br/>
   You must have at least one {{site.data.keyword.cos_full}} account and one bucket in a US Cross Region or US South location to complete the request form. If you don't have an {{site.data.keyword.cos_full_notm}}} account yet, create one before requesting the MDMS device. For more information, see: [About {{site.data.keyword.cos_full}}](/docs/services/cloud-object-storage?topic=cloud-object-storage-about#about){:external}.
   {: important}

## Step 1: Creating a request
{: #create-req}

1. Log in to the [{{site.data.keyword.slportal}}](https://control.softlayer.com/){:external} by using your unique credentials.
2. Select **Storage > Data Migration > Mass Data Migration** from the Navigation Bar to access the MDMS landing page.
3. Click **Request Device** to open the order form.
4. Complete each field in the **Mass Data Migration** order form.
   - **Shipping Address**: This form is not prefilled and each field is editable. Provide the name of the person who will accept the device delivery in the Attention field. When picking the delivery location, consider the weight of the device (30 kg (66 lb) with its case) and accessibility. <br/> (**Note**: The device is equipped with wheels and pop-up handle for maneuvering.)
   - **Key Migration Contacts**: This form isn't prefilled. Each field is editable. More than one person can be added.
   - **Data Center Network Configuration**: Provide network configuration details for the pre-provisioning of the Eth3 port on the MDMS device before shipment.
   - **Data Offload Destination**: Select your existing target account from the list.
   - **Request Name**: Enter a name to help you track your order.
5. Select the **I have read and agree to the full terms of the Mass Data Migration Agreement** check box after reading each service agreement that is provided.
6. Click **Place Request** to submit the request. Click **Cancel** to completely abandon the form and return to the MDMS landing page.

## Step 2: Preparing and shipping
{: #prep-ship}

After submitting the request, the status for the request ticket appears as *Processing Request*. When your request has been processed, {{site.data.keyword.IBM}} begins pre-configuring the next available device and the status on the [Requests](https://control.softlayer.com/storage/mdms){:external} grid will show *Prepping Device* followed by *Awaiting Shipment*. After your request enters *Awaiting Shipment* status, it can no longer be canceled. 

The device is picked up by the carrier to be sent to your location. At this time, the request status is updated to *Device Shipped*. The tracking number is shared with you in the **Order Details** section of the [Requests](https://control.softlayer.com/storage/mdms){:external} grid.

## Step 3: Receiving and connecting
{: #rec-con}

<!-- **[Editor's note: What to keep from this section immediately below?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
1. The device arrives pre-configured for you. Basic [powering/connectivity instructions](docs/infrastructure/mass-data-migration/user-instructions.html) are included.  **[Editor's note: Are the instructions included in the MDMS package? If so, are they different from the instructions found with the "powering/connectivity" link?]**<br/>
  **Note**: User name and storage pool password is provided separately. Check the **Request Details** in your [Requests](https://control.softlayer.com/storage/mdms){:external} grid for the credentials.
2. Point your browser to the static IP address that you provided in the order form. **[Editor's note: Is this done on PDA? What system is the static IP address for?]**
3. Log in. Enter password to unlock the empty storage pool. **[Editor's note: How is this done?]**<br/>
   **Note**: See the **Request Details** of your [Requests](https://control.softlayer.com/storage/mdms){:external} grid for the password.
4. Mount the NFS share on your server. **[Editor's note: How is this done?]**
5. Rerun your DataShuttle inventory to ensure any new files are captured. **[Editor's note: Is "DataShuttle inventory" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

### Overview

The {{site.data.keyword.cloud}} Mass Data Migration device is a portable storage device able to present mountable Network File System (NFS) or FileNet Content Federations Services (CF)S shares and is managed through a web browser interface. The device is shipped to your data center, loaded with data onsite, returned to an {{site.data.keyword.BluSoftlayer_full}} data center, and your data is loaded into your {{site.data.keyword.cos_full}} account.

### Power

The device includes with a C13-US power cord ([IEC 60320](https://en.wikipedia.org/wiki/IEC_60320){:external}). If the device is being used outside of the United States, a power adapter might be required.

The MDMS device accepts all standard power ranges.
![Power range](/images/PowerRating.png)

### Ethernet connectivity

There are two Ethernet connections to be made. One for device management through a browser, and one for data movement on the same subnet where the source data resides.

Both ports originate from the device as RJ45, and CAT6A cables are supplied. Copper SFP+ adapters are provided to convert from RJ45. The adapters work with all switch manufacturers. These adapters are located in a pocket on the underside of the shipping lid.

- Eth1 (1GbE-B) is used for device management, and as such, must have a gateway that is specified in the IP address configuration. This can be viewed on the LCD screen after the device is powered on (see the [IP address configuration](#ip_cfg) section).

- Eth3 (10GbE-B) is used for the data transfer. This connection must be either on the same subnet as the source data, or can be directly connected to the server if needed.

If a different form factor of Ethernet connection is required, you must provide the converter.

### Step-by-step user instructions

1. The MDMS device arrives pre-configured with your IP address, user name, locked storage pool and NFS share. The user password and storage pool password are communicated through a separate email.

2. Determine the most appropriate place for the device to be placed; where it will reach both power and your Ethernet (1GbE and 10GbE) connections and have minimal foot traffic nearby.

3. Position the device to be connected. It can remain in the transport case during use. Ensure that the device is at room temperature and there's no condensation on it. Connect to power by using the provided power cable underneath the case lid. Power on the device.<br/>
    There are two power switches.
    {: note}

    ![Power switches](/images/MDMSPowerSwitch.png "Power switches are circled"){: caption="Figure 1. Power switches" caption-side="bottom"}
    The device does not need to be removed from the portable case.
    {: note}

4. Remove the CAT6A cable from the case lid and connect it to the Eth3 (10GbE-B) port that is shown in the picture.
    ![Eth1 and Eth3 port location](/images/MDMSNewEth1and3.png "Eth1 and Eth3 port locations are highlighted"){: caption="Figure 2. Eth1 and Eth3 port location" caption-side="bottom"}

5. Connect the provided CAT6A to SFP+ adapter and connect to your 10Gb switch.

6. If the IP address configured for Eth3 can be reached through a browser `https://<your_Eth3_IP_Address>`, continue to the next step. 

   Otherwise, connect to the Eth1 (1GbE-B) port. Open your browser and enter `https://<your_Eth1_IP_Address>`. Enter the Eth1 IP address appropriate for your network configuration. Accept the certificate exception.<br/>
   If you need to alter any IP settings for Eth3 or Eth1, see the [IP address configuration](#ip_cfg) section.
   {: note}

7. Use the provided user name and password to log in.<br/>
    ![Login dialog](/images/Login.png "Login dialog"){: caption="Figure 3. Login dialog" caption-side="bottom"}

8. The workflow wizard presents access to the specific items generally used in order from left to right.<br/>
    ![Workflow icons](/images/workflow.png "Workflow wizard displaying workflow icons"){: caption="Figure 4. Workflow wizard" caption-side="bottom"} <br/>
    The workflow can be reopened by using **Workflow Manager** in the upper left of the GUI.
    {: note}

9. Activate the pre-configured storage pool:
    - Click **Unlock and Start Storage Pool**.
    - Enter your Storage Pool Passphrase and click **OK**.
    ![Activate storage pool](/images/UnlockPool.png "Enter passphrase in circled field"){: caption="Figure 5. Activate storage pool" caption-side="bottom"}

10. By default, the share has both NFS and SMB protocols that are enabled with no access restrictions that are placed on the share. To restrict access to this share (for NFS or SMB), right-click the share name and select the appropriate menu item.<br/>
    ![Restrict share access](/images/ShareControls.png "Restrict share access"){: caption="Figure 6. Restrict share access" caption-side="bottom"}

11. When the storage pool is enabled, the NFS share is available to mount. In the workflow, click **View Network Shares** to see the network shares view. Close the workflow, right-click the share, and select **View Mount Command** to see the share name and mount information. Mount the share on your source server. Be sure to specify the IP address of the 10 GB link when mounting the share.
    ![Mounting the share](/images/MountCommand.png "Mounting the share"){: caption="Figure 7. Mounting the share" caption-side="bottom"}

## Step 4: Copying data and shipping
{: #copy-ship}

<!-- &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&

1. Run the DataShuttle copy to move the data. **[Editor's note: What is "DataShuttle"? Is "DataShuttle copy" a command that is run on PDA?]**

&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& -->

1. Copy your data to the NFS share. Choose one of the following methods to extract your data from your Netezza database:
    1. Run the following example of the **nz_backup** utility:

       `/nz/support/contrib/bin/nz_backup –db <db_name> –d <target_directory>  ascii threads 4`

       **Note**: The `<target_directory>` is the NFS share on the MDMS device that is mounted onto your Netezza server.
   
    2. Run the following example of a CREATE EXTERNAL TABLE statement:

       `CREATE EXTERNAL TABLE '<path_to_mdms_device>/<file_name>' SELECT * FROM <table name>`

       **Note:** If you used the `USING` clause options for data export, remember or save the clause options. The clause is reused later during the external table load process from {{site.data.keyword.Bluemix_notm}} Object Storage.

       For more information about the SQL statement, see: [CREATE EXTERNAL TABLE statement](https://www.ibm.com/support/knowledgecenter/SS6NHC/com.ibm.swg.im.dashdb.sql.ref.doc/doc/r_create_ext_table.html){:external}. 

<!--       - Provide the {{site.data.keyword.Bluemix_notm}} team with the "USING" clause that was used for data export. The clause is reused during the load process on {{site.data.keyword.Bluemix_notm}}.
       - Select FORMAT = "Text"
-->

2. In the workflow, click **View Network Activity** to show the inbound Ethernet load in the GUI as data is transferred to the device on the 10Gb/sec link.
    ![View activity](/images/UserGuide13.png "GUI shows inbound Ethernet load"){: caption="Figure 8. View of network activity" caption-side="bottom"}

3. In the workflow, click **View Storage Pools** to monitor storage usage and IOPS on the device.
    ![View storage pool](/images/UserGuide14.png "GUI shows storage usage"){: caption="Figure 9. View of storage pool" caption-side="bottom"}

4. When the copying is done, gracefully power down the system. Powering down the device also locks the storage pool. In the workflow, click **Shutdown Appliance...**.  
    ![Appliance shutdown button](/images/Shutdown.png "Shutdown Appliance UI button"){: caption="Figure 10. Appliance shutdown" caption-side="bottom"}

5. Disconnect the device. Return the power cable, Ethernet cable, and SFP+ adapter into their respective storage locations under the lid.

6. Attach the provided shipping label to the device. Notify the shipper and return the device to the {{site.data.keyword.BluSoftlayer_full}} Data Center. After arrival at the data center, your data is then loaded into your {{site.data.keyword.cos_full_notm}} bucket.

After the device is returned to the {{site.data.keyword.BluSoftlayer}} team, the request status changes to *Device Received*.

## Step 5: Offloading and accessing
{: #offload}

During the data transfer process, the request status is displayed as *Offloading Data*. The status changes again when the migration to the {{site.data.keyword.objectstorageshort}} bucket is completed (*Offload Complete*). Your data is immediately accessible when the high-speed offload into your Cloud Object Storage bucket is completed. 

When the migration of your data into the Cloud Object Storage bucket has completed, you can proceed to [import your data into your {{site.data.keyword.dashdbshort_notm}} database](#import).

## Step 6: Importing data from {{site.data.keyword.Bluemix_notm}} Object Storage
{: #import}

To load data from {{site.data.keyword.Bluemix_notm}} Object Storage by using External Tables directly, the following is an example SQL statement:

```
INSERT INTO <table-name> SELECT * FROM EXTERNAL '<mys3file.txt>' USING
  (CCSID 1208 s3('s3-api.us-geo.objectstorage.softlayer.net', 
  '<S3-access-key-ID>',
  '<S3-secret-access-key>', 
  '<my_bucket>'
     )
  )      
```

**Notes:** 
* Be certain to use the same `USING` clause options that you used to extract the data from your PureData System for Analytics (Netezza) database by using the CREATE EXTERNAL TABLE statement.
* For {{site.data.keyword.Bluemix_notm}} Object Storage, to create HMAC credentials when creating new service credentials, specify {"HMAC:true"} in the *Add Inline Configuration Parameters* field.

For a guided tutorial about importing data from {{site.data.keyword.Bluemix_notm}} Object Storage, see: [IBM Db2 Warehouse on Cloud guided demo: Explore data loading](https://www.ibm.com/cloud/garage/demo/try-db2-warehouse-cloud/){:external}.

## Step 7: Erasing MDMS device
{: #erase}

{{site.data.keyword.IBM}} implements data wipe at the level of the US Department of Defense requirements to permanently erase your data from the MDMS device. When finished, your request status is displayed as *Erase Complete*.

## Additional notes
{: #notes}

### Uniqueness in the bucket

To ensure that object names are unique when they are copied into the bucket, the file path is included as a prefix in the object name. For example, the config.ini file in the `/root/user/` folder becomes renamed to "root/user/config.ini" when copied into the bucket.

### Buckets

If the target bucket doesn't exist, it's created. If it does exist, it must be empty, otherwise the copy can't proceed.

### File systems

Symlinks and hard links are skipped during the scan process.

### IP address configuration
{: #ip_cfg}

The LCD display on the device can be used to configure the IP addresses for the Ethernet ports. You navigate in the LCD display by using the **up arrow**, **down arrow**, **esc**, and **enter** buttons. The **enter** button takes you into a menu and **esc** takes you out of the menu.

![LCD display](/images/MDMSLCD.png "System Control Display"){: caption="Figure 11. System Control Display" caption-side="bottom"}

When editing an IP address or subnet mask, **enter** steps you forward one character at a time; **esc** steps you back one character at a time. The **up arrow** and **down arrow** toggles through the numbers for the selected location.

Use **esc** to go back to the former menu.  

Go to the **Update...** menu item and press **enter** to save the settings.
