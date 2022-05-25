# Challenge Questions

## Crossword Puzzles

### Basic Knowledge Crossword
## Host Forensics
### Hashing Out a Plan
#### Question
Investigators recovered a device suspected of belonging to a malicious actor, and found several interesting artifacts in the user's browser history.

This challenge requires the use of a Windows 10 image. The image (approx. 7GB in size) can be downloaded [here from Google Drive](https://drive.google.com/file/d/1WS-xugADODCI5MPaQ0kFfA8phuNfTJVk/view?usp=sharing)

After downloading, unzip the .7z file to obtain the image.
Use the SuspectImage.E01 file to answer the following questions.

First, what is the MD5 hashvalue associated with this file?
#### Answer
    2E7316484652CC116327A174797BC991
#### Hint
    Make sure you are hashing the unzipped .E01, and not the zipped .7z file.
    If you are looking for a native hashing tool, 
    you can never go wrong with Powershell.
#### Solution Detail
Once the .7z image file is downloaded from the provided link above, 7Zip was used to extract it. After extraction, the file was placed on the Desktop. Powershell was used to retrieve an MD5 hash value from the file, using the following command from the Desktop:

    Get-Filehash SuspectImage.E01 -algorithm md5

The output of the command provided a hash that matches the flag for this challenge.

### Find That User
#### Question
Using the same image obtained from the previous exercise, identify the primary user account name associated with this system.
#### Answer
    tknight
#### Hint
    Look for the main file path used, you are looking for the one 
    Users name that is not just a generic Windows name.
#### Solution Detail
Once the image is unzipped, it can be browsed through and/or mounted using an application like FTK Imager.
Using FTK Imager, click the "Add Evidence Item" button near the top left. In the Select Source window, choos Image File and click Next. In Select File window, browse to navigate to the SuspectImage.E01 file, and then click Finish. Once loaded, in the Evidence Tree pane, click the plus sign on SuspectImage.E01, click the plus sign on Basic data partition (3), click the plus sign on NONAME [NTFS], click the plus sign on [root], and click on the Users folder. The contents of the Users folder should be displayed in the File List pane on the right. Within the contents, the user folder for tknight is visible. The tknight user folder is the only non-pregenerated user folder shown.

### Just Browsing
#### Question
How many different browsers are on this system?
#### Answer
    5
#### Hint
    Looking for a number here, not a word.
#### Solution Detail
The number browsers can be determined by browsing through the contents of the image with FTK Imager or a similar application. In FTK Imager, after mounting the file, navigate to `SuspectImage.E01/Basic data partition/NONAME[NTFS]/[root]/Users/tknight/AppData/Local`. Within the Local folder, there should be separate browser folders for all the browsers, listed by their respective publishers (for example, within the Google folder is Chrome, within the Microsoft folder is Edge *and* Internet Explorer, and so on). The Local folder should contain listings for Chrome, Edge, Internet Explorer, Opera, and Firefox, bringing the grand total number of internet browsers on the device to 5.

### Did You Google It?
#### Question
Search result have returned some interesting hits. What is the Date Accessed time that the phrase "hmi hacking videos" was searched?

(flag format: YYYY-MM-DD HH:MM:SS)
#### Answer
    2022-05-13 10:20:39
#### Hint
    Most browsers keep track of search terms, but each one stores them in slightly different locations.
    But for the mostpart, you will find them in one of the folders in root/Users/<username>/AppData/..
#### Solution Detail
The solution to this question, and the other internet browser history questions, can be solved in a number of ways. Browser history files are stored as SQL databases, and their locations vary slightly depending on the browser. For this question, the browser used was FireFox. Firefox browser databases can be found at `[root]\Users\tknight\AppData\Roaming\Mozilla\Firefox\Profiles\<unique number>.default-release\places.sqlite`. The database file can then be exported and viewed with any number of sql database viewer applications. A review of the search terms used reveals that "hmi hacking videos" was searched for on May 13, 2022, at 10:20:39.

Additionally, more sophisticated forensic tools like Autopsy can be used to automatically retrieve all browser history data from an image and put it all in one convienent location for browsing (in the case of Autopsy, that location is `Results/Extracted Content/Web Search` and `Results/Extracted Content/Web History`).
### Targeted Search
#### Question
Based on the users' browsing history, what famous person's critical infrastructure may have been researched?
#### Answer
    Elon Musk
#### Hint
    Most browsers keep track of search terms, but each one stores them in slightly different locations.
    But for the mostpart, you will find them in one of the folders in root/Users/<username>/AppData/..
#### Solution Detail
The solution to this question, and the other internet browser history questions, can be solved in a number of ways. Browser history files are stored as SQL databases, and their locations vary slightly depending on the browser. For this question, the browser used was Chrome. Chrome browser databases can be found at `[root]\Users\tknight\AppData\Local\Google\Chrome\User Data\Default\History`. The database file can then be exported and viewed with any number of sql database viewer applications. A review of the search terms used reveals that the subject in question was Elon Musk.

Additionally, more sophisticated forensic tools like Autopsy can be used to automatically retrieve all browser history data from an image and put it all in one convienent location for browsing (in the case of Autopsy, that location is `Results/Extracted Content/Web Search` and `Results/Extracted Content/Web History`).

### Some Light Digging
#### Question
The user appears to have looked at methods of using opensource techniques to gather intelligence. Which browser was used to look for a specific framework tool?
#### Answer
    Opera
#### Hint
    Most browsers keep track of search terms, but each one stores them in slightly different locations.
    But for the mostpart, you will find them in one of the folders in root/Users/<username>/AppData/..
#### Solution Detail
The solution to this question, and the other internet browser history questions, can be solved in a number of ways. Browser history files are stored as SQL databases, and their locations vary slightly depending on the browser. For this question, the browser used was Opera. Opera browser databases can be found at `[root]\Users\tknight\AppData\Roaming\Opera Software\Opera Stable\History`. The database file can then be exported and viewed with any number of sql database viewer applications. A review of the search terms used reveals that the tool in question was OSINT, and that Opera was indeed the browser used to search for the tool.

Additionally, more sophisticated forensic tools like Autopsy can be used to automatically retrieve all browser history data from an image and put it all in one convienent location for browsing (in the case of Autopsy, that location is `Results/Extracted Content/Web Search` and `Results/Extracted Content/Web History`).

### More Potential Targets
#### Question
The user may have been targeting a specific sector of critical infrastructure. Where were they looking for PLCs?
#### Answer
    Hospitals
#### Hint
    Most browsers keep track of search terms, but each one stores them in slightly different locations.
    But for the mostpart, you will find them in one of the folders in root/Users/<username>/AppData/..
#### Solution Detail
The solution to this question, and the other internet browser history questions, can be solved in a number of ways. Browser history files are stored as SQL databases, and their locations vary slightly depending on the browser. For this question, the browser used was Edge. Edge browser databases can be found at `[root]\Users\tknight\AppData\Local\Microsoft\Edge\User Data\Default\History`. The database file can then be exported and viewed with any number of sql database viewer applications. A review of the search terms used reveals that the phrase searched for was "plcs in hospitals," thus "hospitals" is the flag.

Additionally, more sophisticated forensic tools like Autopsy can be used to automatically retrieve all browser history data from an image and put it all in one convienent location for browsing (in the case of Autopsy, that location is `Results/Extracted Content/Web Search` and `Results/Extracted Content/Web History`).

### Of Course it Was
#### Question
Looks like the user used one browser to download all the rest of the browsers. Which browser was used to download the rest?
#### Answer
    Edge
#### Hint
    Most browsers keep track of search terms, but each one stores them in slightly different locations.
    But for the mostpart, you will find them in one of the folders in root/Users/<username>/AppData/..
#### Solution Detail
The solution to this question, and the other internet browser history questions, can be solved in a number of ways. Browser history files are stored as SQL databases, and their locations vary slightly depending on the browser. For this question, the browser used was Edge. Edge browser databases can be found at `[root]\Users\tknight\AppData\Local\Microsoft\Edge\User Data\Default\History`. The database file can then be exported and viewed with any number of sql database viewer applications. A review of the search terms used reveals that Chrome, FireFox, and Opera Browser were all searched with the Edge browser.

Additionally, more sophisticated forensic tools like Autopsy can be used to automatically retrieve all browser history data from an image and put it all in one convienent location for browsing (in the case of Autopsy, that location is `Results/Extracted Content/Web Search` and `Results/Extracted Content/Web History`).

## ICS Knowledge-Based Questions
### ICS Protocols
#### Question
What is the most popular ICS-specific networking protocol?
#### Answer
    modbus
#### Hint
    The internet is your friend.
#### Solution Detail
The answer to this question can be found by googling the phrase "most widely used ics protocol."

### ICS Power Source
#### Question
A fail-______ device or system is one that is designed so that the process being controlled will assume its most secure condition in the event of a power or component failure.
#### Answer
    secure
#### Hint
    Read the challenge text carefully.
#### Solution Detail
This is a tough question to goole without any context. But as the hint indicates, the answer is within the text of the question itself: secure.

### Basic ICS Architecture
#### Question
What is the device called that receives instructions and sends out control commands to the sensors, actuators, etc. of an ICS process?
#### Answer
    PLC
#### Hint
    Think about what types of devices are found within Level 0 of the ICS Purdue Model.
#### Solution Detail
The answer to this question can be obtained by googling keywords within the question. A top search his is the Wikipedia page for Programmable logic controler.

## ICS Security
### ICS Safety Systems
#### Question
What is the system called that constantly checks an ICS process to ensure it is within safe parameters?
#### Answer
    Safety Instrumented System
#### Hint
    None provided.
#### Solution Detail
*Will need solution detail*

### ICS Network Security
#### Question
What is the area called that separates the IT and OT networks?
#### Answer
    DMZ
#### Hint
    None provided.
#### Solution Detail
*Will need solution detail*

### ICS MITRE ATT&CK
#### Question
What is the MITRE ATT&CK technique ID for Man in the Middle attacks?
#### Answer
    T0830
#### Hint
    None provided.
#### Solution Detail
The solution to this question can be found by navigating to MITRE's ATT&CK website, and exploring the techniques within ICS.

### ICS APT
#### Question
What unit is thought to have created the Industroyer and Killdisk malware?
#### Answer
    74455
#### Hint
    None provided.
#### Solution Detail
The answer to this question can be obtained by googling keywords within the question. The top result to googling this question is a document from DoJ which mentions the APT's unit number within the first paragraph.

### ICS Targeted Malware
#### Question
Which malware was the first of its kind to target safety instrumented systems within ICS networks?
#### Answer
    TRITON
#### Hint
    None provided.
#### Solution Detail
The answer to this question can be obtained by googling keywords within the question.

## Ladder Logic
### Basic Ladder Logic (Uses Ladder_Logic_Easy.PNG)
#### Question
With this ladder logic diagram will the Motor stay ON if the “Test Button” is depressed and released?
#### Answer
    No
#### Hint
    Think of the flow of electricity.
#### Solution Detail
Since the test button bypasses both the start and stop logic the flow of electricity to the motor will only be completed while the test button is depressed.

### Intermediate Ladder Logic (Uses Ladder_Logic_Medium.PNG)
#### Question
With this ladder logic diagram what actions will occur if the “On/Off Switch” is depressed?

Answer Format = Warning Light: ON or OFF Motor 1: ON or OFF Motor 2: ON or OFF (Must enter semi-colons in your answer.)
#### Answer
    Warning Light: ON Motor 1: ON Motor 2: ON
#### Hint
    Think about what the relay is doing.
#### Solution Detail
Once the On/Off switch is depressed electricity will flow through the top rung and will activate the relay which is linked to the relay in the second rung. Once this relay is activated then the electricty will have access to the warning light, and both motors resulting in all of them to be "ON".

### Advanced Ladder Logic (Uses Ladder_Logic_Hard.PNG)
#### Question
With this ladder logic diagram what will the “Light” do after the “Start Button” is depressed?
#### Answer
    Blink
#### Hint
    Think about what happens to the electricity as it flows through the different rungs and how this affects the relays.
#### Solution Detail
This ladder logic diagram takes advantage of only a single rung but has multiple nested rungs that can be confusing if you don't understand how the electricity will flow through them. For this diagram the reason why the light blinks instead of just turning and staying on is because of how the relays work. When the start button is depressed the flow of electricity will only be able to flow through the second nested rung based on the logic and this will activate the relay which is linked to the relay in the second set of nested logic. Once the electricity reaches the second nested rung it has a path to flow to the light but as it passes through the rung it will also activate the relay again. This causes the flow of electricity to pulse the light on and off. 

### Identify Ladder Logic Symbols #1 (Uses Ladder_Logic_Symbol_1.PNG)
#### Question
Identify what ladder logic symbol is in the attached file.
#### Answer
    Normally Open
#### Hint
    Not provided.
#### Solution Detail
A Google search of ladder logic symbols will provide the answer to this.

### Identify Ladder Logic Symbols #2 (Uses Ladder_Logic_Symbol_2.PNG)
#### Question
Identify what ladder logic symbol is in the attached file.
#### Answer
    Normally Closed
#### Hint
    Not provided.
#### Solution Detail
A Google search of ladder logic symbols will provide the answer to this.

### Identify Ladder Logic Symbols #3 (Uses Ladder_Logic_Symbol_3.PNG)
#### Question
Identify what ladder logic symbol is in the attached file.
#### Answer
    Coil
#### Hint
    Not provided.
#### Solution Detail
A Google search of ladder logic symbols will provide the answer to this.

## Modbus Network Analysis
### Malicious Modbus Command #1 (Uses fortiphyd_attack.pcapng)
#### Question
What is the MAC address of the IP address 192.168.90.100?
#### Answer
    08:00:27:5d:7b:c3
#### Hint
    Not provided.
#### Solution Detail
You simply need to find a packet within the PCAP that is associated with the IP 192.168.90.100 and dig into the packet data within the "data-link" breakdown to find this answer.

### Malicious Modbus Command #2 (Uses fortiphyd_attack.pcapng)
#### Question
What is the name of the ScadaBR file being requested in the web traffic?
#### Answer
    MiscDwr.doLongPoll.dwr
#### Hint
    Not provided.
#### Solution Detail
You will have to dig through the PCAP file until you find HTTP traffic that is associated ScadaBR and packet information will contain the file name for this answer. Packet #18405 is an example.

### Malicious Modbus Command #3 (Uses fortiphyd_bitflip.pcapng)
#### Question
What is the packet number in the PCAP file that sent the malicious write command?
#### Answer
    15050
#### Hint
    Pay attention to the ICS protocol.
#### Solution Detail
If you sort by the Modbus protocol you will see specific packets that show write commands that indicate when the attack occured.

### Pressure Tank goes BOOM! #1 (Uses fortiphyd_bitflip.pcapng)
#### Question
How many different Modbus function codes are there in this PCAP?

Answer = #
#### Answer
    3
#### Hint
    Not provided.
#### Solution Detail
Sorting the packets by Modbus you will be able to find there are 3 distinct function codes in the PCAP.

### Pressure Tank goes BOOM! #2 (Uses fortiphyd_attack.pcapng)
#### Question
What type of webserver is being used during this attack?
#### Answer
    Apache-Coyote
#### Hint
    Not provided.
#### Solution Detail
By sorting the packets by protocol and looking at the HTTP traffic you can pull this answer from the packet data breakdown.

### Pressure Tank goes BOOM! #3 (Uses fortiphyd_attack.pcapng)
#### Question
What is the checksum of the last POST command to ScadaBR?
#### Answer
    0x6289
#### Hint
    Not provided.
#### Solution Detail
By sorting the packets and looking at the HTTP traffic you can scroll down to the last POST request and dig into the packet data to find the checksum value.

### Modbus Attack Identification Challenge #1 (Uses Modbus_PCAP_Challenge_1.pcap)
#### Question
Analyze the provided Modbus traffic PCAP to identify what type of attack is occurring.
#### Answer
    Man In The Middle
#### Hint
    Wireshark might not be the best PCAP analyzer for this
#### Solution Detail
This challenge will prove to be difficult to complete by using Wireshark. I used NetworkMiner to analyze the PCAP file which lays out the series of events that occured and makes it clear there was a Man-in-the-Middle attack.

### Modbus Attack Identification Challenge #2 (Uses Modbus_PCAP_Challenge_1.pcap)
#### Question
Analyze the provided Modbus traffic PCAP to identify what type of attack is occurring.
#### Answer
    Query Flooding
#### Hint
    Wireshark might not be the best PCAP analyzer for this.
#### Solution Detail
Again, this challenge will be difficult to complete by using Wireshark. I used NetworkMiner to analyze the PCAP and it if you look under the "Sessions" tab and sort by event you will see there is a large amount of query requests over a short amount of time. Indicating a query flood attack.

## Networking
### Basic Networking Knowledge
#### Question
What is Considered the gateway in a network?
#### Answer
    router
#### Hint
What device directs network traffic within a LAN or WAN?
#### Solution Detail
An entry-level question designed to get users thinking.

### Intermediate Networking Knowledge
#### Question
What would you implement to segregate a LAN to increas a network's security posture?
#### Answer
    VLAN
#### Hint
    Think Layer 2.
#### Solution Detail
The solution here can be reached pretty quickly with a well-placed search or two. For instance, googling the phrase "What is Network Segmentation?" results in an easy-access document by Palo Alto on the first hit, giving high-level discriptions as to what VLANs are and how they're established.

### Advanced Networking Knowledge
#### Question
What is the Cisco command to enable sticky learning for port security for a switch? (Syntax sensitive.)
#### Answer
    switchport port-security mac-address sticky
#### Hint
    None provided.
#### Solution Detail
Cisco Packet Tracer was used to complete this challenge. Using Packet Tracer, a switch and an end-device PC were added to the GUI, and an ethernet connection was made to connect the switch at FastEthernet port 0/2 to the PC at the FastEthernet port 0. Once connected, a CLI window was pulled up from the switch. Below is a list of commands used to configure the switch to use the port security sticky feature:

    enable
    config t
    int f0/2
    switchport mode access
    switchport port-security
    switchport port-security mac-address sticky

Additionally, the correct answer can be found by googling the phrase "cisco port security sticky"

### Expert Networking Knowledge
#### Question
What part of an Ethernet frame allows detection of corrupted data within the entire frame as received on the receiver side?
#### Answer
    frame check sequence
#### Hint
    None provided.
#### Solution Detail
FCS information can be gleaned by googling key terms within the question. This leads users to the Ethernet frame Wikipedia page, which contains the answer.
