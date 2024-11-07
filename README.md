
# Install and Licensing Workarounds
Collection of unsupported Flame and Flow Production Tracking licensing issue workarounds

## Disclaimer

These are not official Autodesk certified scripts or solutions. Neither the author nor Autodesk are
responsible for any use, misuse, unintended results, or data loss that may occur from using
the information provided. These workarounds have not been thoroughly tested and are a work in progress. It was
created on personal time to address specific customer requests and may not be applicable to your workflow.

**Use at your own risk.**
- These workarounds are intended for providing guidance only.<br>
- There is no support provided.<br>
- Caution is **strongly** advised as these has not been thoroughly tested.

<br><br>

## Licensing/Accounts URL validation:
[Flow Production Combined URL Checker](https://github.com/flamescripts/FlowProductionTracking/tree/main/Flow_Combined_URL_Checker)<br /><br />
This Python 3 script checks if a list of Fully Qualified Domain Names (FQDNs), Autodesk Subscription URLs and Autodesk Identity URLs can connect to a port of your selection. It uses the data from the FPT Ecosystem help page, "Which URLs/Protocols need to be allowed for Autodesk Subscription Licensing" page and the "Which URLs/Protocols need to be allowed for Autodesk Identity Manager" help page. The script attempts to establish a socket connection for each one. The script then shows which URLs successfully connected to the selected port and which did not. Curl is used for the sitename check.


<br><br>
## Flame Keyring Popup
**Potential fix for “Unable to access information in your keyring”**
![alt text](https://global.discourse-cdn.com/flex020/uploads/thedepartmentofexternalservices/original/2X/6/689ff113d0e77b3f1b1c16dc53868d717b4abb38.png)

### Test Environment

- Operating System: Rocky Linux 9.3
- Flame Family: 2025
- Auto-Login: Activated
 

### Installation:
- Install seahorse using `dnf`.
  - This process included upgrading openldap, openldap-clients, openldap-devel and installing dependencies for openldap-compat.
- The code block below should be appended to end of the user's local start script, such as `~/.bash_profile`, if intending to be automated at login.  Can also be placed into the external script `unlock_keyring.sh` for manual execution, which is provided in the Alternate Testing section.  

**Note**: Change PASSWORD to your user password.

    sleep 5
    killall gnome-keyring-daemon
    sleep 2
    unlock_keychain="PASSWORD"
    eval $(echo -n "${unlock_keychain}" | gnome-keyring-daemon --unlock)

### Caveats:
- Installing seahorse may not be neccessary.
- This workaround does not remove the need to open a browswer session and Return to product.
- While testing workaround, wait at least 10 seconds after login to launch Flame.
- The `sleep` commands can be experimented with or removed.
<br><br><br>
### Alternate Testing:
If there are issues, please validate that you are able to unlock your Login keychain by performing the following:
- Pull up the Passwords and Keys app.
- Select the `Login` key under **Password**
- Right Click the `Login` key and and select **Lock** from the contextual menu.
- Run the script `unlock_keyring.sh` to validate `Login` gets unlocked.

unlock_keyring.sh contents:

    #!/bin/bash
    
    killall gnome-keyring-daemon
    unlock_keychain="PASSWORD"
    sleep 2
    eval $(echo -n "${unlock_keychain}" | gnome-keyring-daemon --unlock)

**Note**: It may be necessary to close the Passwords and Keys app and relaunch to see the updated lock status.  Change PASSWORD to your user password.

- If successful, your Passwords and Keys should unlock to see the AdskIdentityManager Safe Storage<br><br>
![Passwords and Keys](https://help.autodesk.com/sfdcarticles/img/0EMKf000006pY07)
