
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



## Flame Keyring Popup
**Potential fix for “Unable to access information in your keyring”**
![alt text](https://global.discourse-cdn.com/flex020/uploads/thedepartmentofexternalservices/original/2X/6/689ff113d0e77b3f1b1c16dc53868d717b4abb38.png)

## Test Environment

- Operating System: Rocky Linux 9.3
- Flame Family: 2025
- Auto-Login: Activated
 

## Installation:
- Install seahorse using `dnf`.
  - This process included upgrading openldap, openldap-clients, openldap-devel and installing dependencies for openldap-compat.
- The code block below should be appended to end of the user's local `~/.bash_profile`, if intending to be automated at login.
  - Can also be placed into an external script.  

**Note**: Change PASSWORD to your user password.

    sleep 5
    killall gnome-keyring-daemon
    sleep 2
    unlock_keychain="PASSWORD"
    eval $(echo -n "${unlock_keychain}" | gnome-keyring-daemon --unlock)

## Caveats:
- Installing seahorse may not be neccessary.
- This workaround does not remove the need to open a browswer session and Return to product.
- While testing workaround, wait at least 10 seconds after login to launch Flame.
- The `sleep` commands can be experimented with or removed.


-------------
