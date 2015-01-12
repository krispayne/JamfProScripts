CasperSuiteScripts
==================

A collection of scripts I have worked on to be used with the Casper Suite, and in some cases, which can be used with other Mac management tools.

###Current scripts
####**Update_Core_Apps.sh**<br>
The Update_Core_Apps script can be used to update many common free applications and Plug-ins. Despite the word "Update" in its name, it can also be used to install most of these applications and Plug-ins new on a target Mac.

Details on the script are as follows:
- Requires the current beta release of cocoaDialog to be installed on the target Mac if using Self Service mode (see below)
- Can update any of the following applications and plug-ins:
  * **Adobe Reader**
  * **Adobe Flash Player**
  * **Firefox**
  * **Firefox ESR**
  * **Flip Player** (free version)
  * **Oracle Java**
  * **Microsoft Office 2011** (updates only)
  * **Silverlight**
  * **VLC**
- Can be used in a "silent" mode to update apps/Plug-ins silently on a target Mac, or "Self Service" mode to prompt an end user to install an update and show them both download and install progress, new version information, and success or failure notifications.
- Has built in version checking against installed applications (if its installed), by comparing it to the latest release from the vendor. The version checking can handle odd version naming conventions, so that it ensures it is only "upgrading" a client, not downgrading it.
- Office 2011 updates utilize a noquit.xml file to suppress the built in quit apps function of these updates. This allows these updates to install either silently, or via Self Service, without forcing the client to shut down the open applications. In both silent and Self Service modes, a dialog will alert the client of any applications that were open that should be quit and relaunched after installation.
- The script accepts two Parameters passed to it from a Casper Suite policy:
  * Parameter 4 ($4) is mandatory, and accepts a number of different strings for the app or Plug-in to check for updates. (For a full listing of acceptable strings, see how to display the help page for the script below).
  * Parameter 5 ($5) is optional, and can accept any string to enable Self Service mode.
  * Strings are case insensitive.
- The script replaces both the **installLatestFlashPlayer-v1.sh** and **install_Latest_AdobeReader.sh** scripts.

#####Basic usage  
1. To test the script from Terminal on a Casper Suite managed Mac:  
`sudo jamf runScript -script Update_Core_Apps.sh -path /path/to/script/ -p1 "app or plugin name"` _(mandatory)_ `-p2 "any string to enable Self Service"` _(optional)_  

2. When adding the script to a Casper Suite policy, add a string to Parameter 4 and optionally Paramater 5.

#####To show a help page for the script, in Terminal:  
`/path/to/script/Update_Core_Apps.sh`  
<br>
<br>
####**create_SelfService_Plug-in.sh**<br>
This script can be used to create Casper Suite Self Service Plug-ins on the fly, without needing to create them first within the JSS, then pulling them down with the management framework. Useful for quick testing when creating new Plug-ins, before actually setting them up within the JSS. Also useful for environments that wish to 'scope' URL Plug-ins and not auto deploy all new Plug-ins to all managed Macs.

Details on the script:  

1. The script must be run as root (sudo)
2. The script is interactive. It will 'guide' you on what you need to enter each step of the way.
3. The script clearly indicates what items are **Required** versus those that are **Optional**.
4. The script can accept images to use for the icon and convert them into the correct binary format
5. The script will create SS URL plug-ins with unique IDs that start in the 1000+ range. This is done so (hopefully) none of the ones you create with the script will conflict with any you created in your JSS.  
  *Note: the JSS will start with ID 1 and increment up, even if you delete any plug-ins later (IDs don't get reused).*
6. The script will create the necessary folder hierarchy on a Casper managed Mac, and save it to the appropriate location, making it immediately available in Self Service.app.
 * If used on a non managed Mac, it will save the resulting plug-in plist to your Desktop
7. The script notes the resulting Plug-in's ID (same as file name) and save path, so it should be easy to locate and wrap into a package later for deployment.  

#####Basic usage
`sudo /path/to/create_SelfService_Plug-in.sh`  
Enter your administrator password, and follow the on screen instructions
<br>
<br>
####**selectable-SoftwareUpdate.sh**<br>
- Requires the current beta release of cocoaDialog to be installed on the target Mac.
- Displays a checkbox dialog with available Software Updates to be installed.
- Provides feedback on installations as they run with a moving progress bar.

####**installLatestFlashPlayer-v1.sh**<br>
(This script has been replaced by Update_Core_Apps.sh)

####**install_Latest_AdobeReader.sh**   (_New_)<br>
(This script has been replaced by Update_Core_Apps.sh)
