# How to detect Frida?

## Case 1: Check the availability of port 27042  \
The application attempts to connect to port=27042, if it connect successfully, which means Frida server is running on Android device. 

**ByPass** : 
Method 1: Hook connect() function of libc.so. If the port is equal to 27042, set it to other values, i.e., 27043. \
Method 2: Run Frida Server on a different port instead of 27042.


## Case 2: Detect Frida-agent.    \
When we attach/spawn Frida to any running app, Frida injects a few components to the running process memory, such as frida-agent. \
This agent is called frida-agent.so. This frida-agent.so is loaded to the app's process memory. One way to do this is to detect whether frida-agent-64.so is in
/proc/[app_pid]/maps/. \
$ cat /proc/[app_pid]/maps | grep "frida-agent"


**ByPass** : 
Step 1: Create a fake /proc/[app_pid]/maps file. Back up the orignial maps file, and replace frida-agent-64.so with xxxx.so. \
Push the modified maps file back to the /data/local/tmp/maps. Make sure the modified maps have 777 permisssion. \

Step 2: Hook open() functions. If running process is trying to access "self/map" file, we will replace it with /data/local/tmp/maps file.
e.g., the arg.readCString().indexOf("self/maps"), 


Note: If open function is not there, try svc functions. svc functions can be found by radware2 tools with the following commands:  \
$ e asm.os = linux  \
$ /as


## Case 3: Check the checksum of the library
  When Frida is attached to the app, it makes some changes of the process memory. The app can compare some libraries to detect Frida. \
  If the library in the disk is not equal to the one in the memory, indicating Frida is injected to the app. So, the app can check if some libraries are manipulated or not. \
  For example, compare libc.so.

  **ByPass**:???




Ref: https://www.youtube.com/watch?v=FNtzJDU5BAI
