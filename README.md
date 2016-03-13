# wallaby-python
Connect your Wallaby to Eclipse to write Python
====

**This repository supports the automatic transfer of Python code from Eclipse to the Wallaby robot controller via USB.**

**Assumptions:**
* Your Wallaby is running v16
* You are running on a Windows PC
* You have Java installed
* You have Eclipse installed
* You have Python 2.7 installed 
* You have the Eclipse PyDev plug-in installed 
* You know how to open a terminal or cmd window
* You know how to open a text file and copy the contents into an Eclipse editor window

**Download the Wallaby_Eclipse Toolset**
* In a browser, open http://github.com/kipr/wallaby_eclipse
* On the right pane, click [Download ZIP]
* Save the file to a directory can find
* Open that directory and extract/unzip into `C:\tools\`
 - If this worked correctly there should be files in `C:\tools\wallaby_eclipse\`


Instructions 
====

**Setup Secure Shell**  (Only required the first time you connect to the Wallaby)
* Open a terminal window 
* Change directory to the Tools directory `cd  \tools\wallaby_eclipse\`
* Log into the Wallaby `putty -ssh root@192.168.124.1`
* Accept the security certificate `yes` 

**Setup Eclipse**
* Start Eclipse
* Click [Run -> External Tools -> External Tools Configurations...]
* Right click [Program -> New]
* Name: `Send Python to USB`
 - you can name it anything you want
* Location: `C:\tools\wallaby_eclipse\win_python.bat`
 - The [Browse File System...] button saves typing
* Working Directory: `C:\tools\wallaby_eclipse\`
 - Again the [Browse File System...] is your friend
* Arguments: `192.168.124.1  ${project_name}  ${project_loc}` 
 - don't change anything except the IP address!
* Click [Apply]
* Click [Close]

**Setup the Project**
* Click [File -> New -> Other...]
* Wizards: `PyDev Project`
* Click [Next]
* Project name: `DemoBot`
* Project type: [Python]
* Grammer Version: [2.7]
* Interpreter: [Default]
* Click radio button: [Create 'src' folder and add it to the PYTHONPATH]
* Click [Finish]

**Add Wallaby Library**
* Click [Window - Preferences]
* Click [PyDev - Interpreters - Python Interpreter]
* In Libraries tab, click [New Folder]
* Browse to `C:\tools\wallaby_eclipse\
* Click [Ok]
* Click [Ok]

**Create main.py**
* Expand [DemoBot] (in PyDev Package Explorer on left side of screen)
* Right click [src -> New -> PyDev Module]
* Package: (leave blank)
 - Packages are currently not supported.
* Name: `main`  
 - **(IMPORTANT: the python script you want to run first must be named main)**
* Click [Finish]
* Template: [Empty] 
* Click [Ok]
 
**Populate main.py**
* Copy the following code into the main.py window:
``` py
import wallaby as w


def main() :
    print "Starting...."
    testMotors()
    print "Finished"

def testMotors() :
    w.motor(1,100)
    w.motor(3,100)
    w.msleep(3500)
    w.ao()


if __name__ == "__main__":
    # set print to unbuffered
    import os
    import sys
    sys.stdout = os.fdopen(sys.stdout.fileno(),'w',0)
    main()
```
* Click [File - Save]

**Test Download**
* Click ub the [main.py] window 
* Click [Run - External Tools - External Configurations...]
* In the left pane, click [Send Python to USB]
* Click [Run]
* Look for the following transfer message in the console window
 - ` main.py                   | 0 kB |   0.3 kB/s | ETA: 00:00:00 | 100% `
 - `Update Complete `
* Launch your code on the Link [Programs - DemoBot - Run]

