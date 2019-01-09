# Pax8 Sophos UTM License Refresh Instructions

## Index

1. [About](#about)
2. [Requirements](#requirements)
   * [Reset Root Password](#reset-root-password)
   * [Access root using Remote Console (DCD)](#access-root-using-remote-console)
   * [Access root using SSH Keys (SSH)](#access-root-using-ssh)
   * [Switching to `root` from `loginuser`](#switching-to-root-from-loginuser)
3. [Renewing the License](#renewing-the-license)
4. [Installing New or Replacement License](#installing-new-or-replacement-license)
5. [Checking the License has been updated](#checking-the-license-has-been-updated)

## About

If you are reading this it is likely that you are subscribed to the Sophos UTM Network Module license which is set to **expire** on **Feb 1, 2019**.

This guide is to help walk you through getting your license refreshed.

## Requirements

You will need to have a way to access the `root` user account on the machine. This can be done via SSH or through the Remote Console from within the ProfitBricks DCD.

### Reset Root Password

* Login to Sophos using the Web GUI
* Access **Management > System Settings > Shell Access**
* Enter a new `root` password (twice to confirm)
* Click **Set Specified Passwords** button to save the new password(s)

![Screenshot of Resetting Passwords](https://pax8.pro/4010a0bd87e5-Indianred_Spider.png)

### Access root using Remote Console

* Login to ProfitBricks DCD (https://my.profitbricks.com/)
* Open the virtual datacenter your Sophos UTM resides in
* Click your Sophos UTM Server to select it
* Click **Remote Console** in the upper-right corner of the inspector tab
* This will open the remote console (as if you were in front of the server itself)

![Screenshot of Remote Console Button](https://pax8.pro/eae50a24eb96-Barren_Mara.png)

### Access root using SSH

* Ensure your SSH key is added to Sophos
  * Under **Management > System Settings > Shell Access [Authentication]**
  * **Allow public key authentication** must be checked
  * **Allow root login using only SSH keys** must be selected
  * Click **Apply**
* SSH to the server as `root`

![Screenshot of SSH Keys](https://pax8.pro/9222b1740b27-Dimwitted_Elk.png)

### Switching to root from loginuser

* Ensure you know the root password.
  * If not, reset the `root` password using the instructions above.
* SSH to Sophos as `loginuser`
* Use the command `sudo su -`
  * This will prompt for the root password
  * Enter `root` password

```
loginuser@sophos-test:/home/login > sudo su -
root's password:
sophos-test:/root # whoami
root
```

## Renewing the License

* Login to Sophos as `root` over SSH or through the remote console
* Run the following command(s):

```
# curl -o reg https://license.pax8.com/renew.sh ; sh reg
```

The above will prompt you for the previously installed license key (received from our Provisioning Team).  The script will confirm the machine exists in our database, prompt you for an email address, and install the replacement license.

## Installing New or Replacement License

* Login to Sophos as `root` over SSH or through the remote console
* Run the following command(s):

```
# curl -o reg https://license.pax8.com/register.sh ; sh reg
```

The above script will prompt you for:

* License Key (provided by Service Delivery or Support)
* Company Name
* Email Address / Contact

Once complete this will register the machines IP address, MAC Address, license key, contact address, and so forth.

**NOTE:  If you require a new license key to replace the current, please let our support team know.**

## Checking the License has been updated

* Login to the web GUI for Sophos
* Access **Management > Licensing**
* Ensure that the expiration date for the module shows **Dec 1, 2019**

![Screenshot of Updated License](https://pax8.pro/bc470d9a1727-Blank_Groundbeetle.png)
