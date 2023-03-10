# incident-response-scanner
An easy to configure malware scanner for incident responses. 
<br>
![preview](preview.PNG)

## Status
Pre-Release

## Features
* File scan with optional sha1 hash verfication
* IPV4 Addresses found in active TCP connections
* Running Processes
* Registry Scan

## To/Do
* IPV6 TCP in active TCP connections 

# How to Configure
 Find and edit the section below in scanner.cs
 ```C#
 /* Edit the variables below to match your malware symptoms */

 /* process names to search for */
 string[] processes = { "svchost" };

 /* Searches ALL users AppData folders for a specific file and verfies the hash if wanted
 * e.g: If the malicous file was located in C:\Users\DrewQ\AppData\Roaming\backdoor.ps1 
 * and its file has was c7a5fa3e56640ce48dcc3e8d972e444d9cdd2306
 * 
 * you would configure the dictionary below as   
 */
 Dictionary<string, object?> appDataFiles = new Dictionary<string, object?>() {
     {"\\Roaming\\backdoor.ps1", "c7a5fa3e56640ce48dcc3e8d972e444d9cdd2306"}
 };
 /* Note: If you are not concerned about the files hash you can pass null.
  * Dictionary<string, object?> appDataFiles = new Dictionary<string, object?>() {
     {"\\Roaming\\backdoor.ps1", null}
   };
  */

 /* List of IP's to flag if they show up in the active TCP connections */
 string[] IPAddresses = { "" };

 /* Non user specific files to look for */
 Dictionary<string, object?> files = new Dictionary<string, object?>() {
     {"C:\\Windows\\Boot\\Mal.exe", "b32dab7b26cdf6b9548baea6f3cfe5b8f326ceda"}
 };


 /* Windows Registries to check
  * Note: Use the full path. PATH/VALUE
  * the format is {REGISTRY, VALUE}. If you are not concerned about the value and only 
  * want to check for existence pass null.
  */
 Dictionary<string, object?> registries = new Dictionary<string, object?>() {
     {"HKEY_LOCAL_MACHINE\\SYSTEM\\Software\\Microsoft\\shell", "ls -las"},
     {"HKEY_CURRENT_USER\\Software\\Microsoft\\Windows\\CurrentVersion\\Internet Settings\\Test", null }
 };
 ```
