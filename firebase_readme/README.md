# Purpose 

This document describes Firebase, FirebaseTrial.py, ELFI gui threads and code flow chart

## Table of Contents
* [What is Firebase](#What-is-Firebase)
* [Firebase Realtime Database](#Firebase-Realtime-Database)
* [FirebaseTrial.py](#FirebaseTrial.py)
* [Code FlowChart and Logic Explanation](#code-flowchart-and-logic-explanation)
* [Errors Causes and Solutions](#the-errors-causes-and-solutions)


## What is Firebase

<p align="center">
  <img src="./Firebase_Logo.png">
</p>

Firebase is a mobile and web app development platform that provides developers with a plethora of tools and services to help them develop high-quality apps, grow their user base, and earn more profit.

### Firebase vs Google Cloud Storage

* **Firebase**  : 
  The Realtime App Platform. 
  Firebase is a cloud service designed to power real-time, collaborative applications. 
  Simply add the Firebase library to your application to gain access to a shared data structure; any changes you make to that data are automatically synchronized with the Firebase cloud and with other clients within milliseconds.

* **Google Cloud Storage**  :   Durable and highly available object storage service. 
  Google Cloud Storage allows world-wide storing and retrieval of any amount of data and at any time. 
  It provides a simple programming interface which enables developers to take advantage of Google's own reliable and fast networking infrastructure to perform data operations in a secure and cost effective manner. 

In conclusion we used Firebase because in our application we needed to instantly upload and download between the PC with the elf file and the ELFI GUI, the PC2 that is connected to the target.


## Firebase Realtime Database

The Firebase Realtime Database is a cloud-hosted database. 
Data is stored as JSON and synchronized in realtime to every connected client. When you build cross-platform apps with iOS, Android, and JavaScript SDKs, all of your clients share one Realtime Database instance and automatically receive updates with the newest data.

The Realtime Database is really just one big JSON object that the developers can manage in realtime.

<p align="center">
  <img src="./1_kiliGRYQIVzsCTx_JsUYdg.png">
</p>


### Key capabilities

* **Realtime**  : 
  Instead of typical HTTP requests, the Firebase Realtime Database uses data synchronization—every time data changes, any connected device receives that update within milliseconds. 
  Provide collaborative and immersive experiences without thinking about networking code.

* **Offline**  : 
  Firebase apps remain responsive even when offline because the Firebase Realtime Database SDK persists your data to disk. 
  Once connectivity is reestablished, the client device receives any changes it missed, synchronizing it with the current server state.

* **Accessible from Client Devices**  : 
  The Firebase Realtime Database can be accessed directly from a mobile device or web browser; there’s no need for an application server. 
  Security and data validation are available through the Firebase Realtime Database Security Rules, expression-based rules that are executed when data is read or written.
 

### Create your Firebase Database

1. Firebase website -->> https://firebase.google.com/
2. Press Get started Button

<p align="center">
  <img src="./1.JPG">
</p>

3. Click on add project 

<p align="center">
  <img src="./2.JPG">
</p>

4. Write down your project name
5. Press Continue

<p align="center">
  <img src="./3.JPG">
</p>

6. Press Continue

<p align="center">
  <img src="./4.JPG">
</p>

7. Name your Firebase Acoount

<p align="center">
  <img src="./6.JPG">
</p>

8. Choose your Analytics location
9. Accept the terms and policy

<p align="center">
  <img src="./7.JPG">
</p>

10. Press Create project

<p align="center">
  <img src="./8.JPG">
</p>

11. Press Continue

<p align="center">
  <img src="./9.JPG">
</p>

12. Time to register your app

<p align="center">
  <img src="./10.JPG">
</p>

13. Add a nickname to your app
14. Press Register app

<p align="center">
  <img src="./12.JPG">
</p>


15. Add Firebase SDK, press Next

<p align="center">
  <img src="./13.JPG">
</p>

16. Install Firebase CLI, press Next

<p align="center">
  <img src="./14.JPG">
</p>

17. Deploy to Firebase Hosting , press Continue to the console

<p align="center">
  <img src="./15.JPG">
</p>








## FirebaseTrial.py

FirebaseTrial.py is the script used to:
1. Upload Marker, Erase, Verify and Data frames to our firebase database. 
2. Download and check the responses uploaded to the firebase via the Gateway. 

### Connect python script to Firebase Database




* **FlashNewApp**         : Indicates that a New Flashing Sequence is about to start.
* **Frame**               : Holds the Current Frame which is one of Four options **Data Command** or **Erase Command** or **Verification Command** or **Response Command**
* **Marker**              : Holds the Marker Frame and then the Marker Frame Response
* **MarkerRQT**           : Inicates is updated when New Flashing Sequence is about to start.
* **NodeMCUSemaphore**    : NodeMCUs checks that there is no other Node is writing in NodeMCUs channel right now.
* **NodeMCUs**            : Resgitered NodeMCUs that available for flashing. 
* **ResponseRQT**         : Flag to indicate that the uploaded command would wait for Response like **Erase Command** or **Verification Command**
* **SelectedGateway**     : Updates when **GUI** selectes specific target to Flash.
* **Send**                : **PC Application** sets it True when Uploading Command, **NodeMCU** sets it False after reading the Command, Major use is **Synchronization**.

## Code FlowChart and Logic Explanation.
<p align="center">
  <img src="/Gateway_Node/Images/NodeMCU_FlowChart.png">
</p>

* **NodeMCU** is used as a Gateway, so it's main job is to receive commands through WIFI from Firebase and trasnmit them serially using UART to STM or any microcontroller used.
* **NodeMCU** Synchrnoization between NodeMCU and PC Application responsible for Flashing Sequence is done through some Flags on Firebase ex) **Send** and **MarkerRQT**
* **NodeMCU** starts with setting up its Environment like Initializing WatchDog, Connecting to WIFI and Firebase, Setting up capacity of HTTP Transfer and Finally Registering itself on available **NodeMCUs** channel on Firebase
* **NodeMCU** Loop is Responsible for the Following:
   * Feeding the WatchDog Timer.
   * Fetching **FlashNewApp** and **SelectedGateway** Flags from Firebase, if the NodeMCU is the selected Node to be flashed and there is a new software to flash, **NodeMCU** enters Flashing Mode
   * In **Flashing Mode**, NodeMCU gets important flags from Firebase which are : **Send**, **ResponseRQT** and **MarkerRQT**
    * IF **MarkerRQT** is True it means that the **PC Application** started communication with the **NodeMCU**, and at that moment **NodeMCU** fires the DIO pin connecting it to STM to notify STM that there is a Flashing New Application Request
    
      When **STM** senses the event, it sends back Message to NodeMCU as a Notification that it's now available to receive the new **Marker**, at that moment **NodeMCU** fetches the **Marker** from **Firebase** and sends it STM, then wait for its response
    
      When **NodeMCU** receives Marker Response from STM, it checks against it, Positive Response means that the STM would proceed the flashing sequence, and Negative Response means that STM wouldn't proceed as the application already exists.
    
    * If **SendRQT** is True and **ResponseRQT** is True, this means that **NodeMCU** will receive Non-Data Command which it either **Erase Command** or **Verify Command**, these types of commands waits for response.
    
      So when it receives the command, **NodeMCU** sends it to **STM** and waits for the Response, when it receives Response it uploades the **Frame** to **Firebase** and set **Send** to false as an indicator that **PC Application** has something new to read.
    
    * If **SendRQT** is True and **ResponseRQT** is False, this means that **NodeMCU** will receive Data Command, this types of commands doesn't wait for response, and set **Send** to false as an indicator that **PC Application** has something new to read.
    
      So when it receives the command, **NodeMCU** sends it to **STM** and waits for **ResponseRQT** to be True -waits for **Verification Command**- , when it receives Response it Verification Command uploades the **Frame** to **Firebase** and set **Send** to false as an indicator that **PC Application** has something new to read.    

## The Errors Causes and Solutions 

### 1- ArduinoJson library not exist 

You should install ArduinoJson version 5.13.5 not the latest version.

### 2- Exception(9) and (28) 

![](/Gateway_Node/Images/6.jpg)

We Started with looking up exception code in the Exception Causes(EXCCAUSE) table to understand what kind of issue it is. We have no clues what it’s about and where it happens, so we used Arduino ESP8266/ESP32 Exception Stack Trace Decoder to find out in which line of application it is triggered.
After a lot of search and trying many solutions we discovered that the problem was because of some issues in the library we use at (2.1) step (1) so we used Firebase real-time database Arduino library for ESP8266 it’s Google's v 2.9.0, we used it with using the first library 

Steps for using it :
1. Instalation Using Library Manager At Arduino IDE, go to menu Sketch -> Include Library -> Manage Libraries..
   In Library Manager Window, search "firebase" in the search form then select "Firebase ESP8266 Client". Click "Install" button.
2. We added this line to our code and we started to use it in each Firebase API’s       
   
   ```ino
   // Declare the Firebase Data object in the global scope 
      FirebaseData firebaseData; 
   ```
Then we replaced our code with the new way using this object, for Example:

![](/Gateway_Node/Images/7.jpg)

### 3- Exception(29)

After reading it from the exception table and tring many unuseful solutions like using ArduinoJson library we found that when we used firebase database library as solution for problem (3.2), this library has buffer for each object and we should use those lines of code to change the size of the buffer corresponding to our data to avoid data corruption  
 

```ino
/* Optional, set the size of BearSSL WiFi to receive and transmit buffers */ 
       firebaseData.setBSSLBufferSize(4000, 4000); //minimum size is 4096 bytes, maximum size is 16384 bytes
```

```ino
/* Optional, set the size of HTTP response buffer */
       firebaseData.setResponseSize(4000); //minimum size is 400 bytes
```

And we also added those lines of code to avoid any watchdog timer issues 
 
```ino
   Add in setup()
   ESP.wdtDisable(); 
   ESP.wdtEnable(WDTO_8S);

   And in loop()
   ESP.wdtFeed();
```

### 4- Corrupted Data 

In our design, we have two kind of frames:
1. Non Data frame : it contains 8 bytes of data that includes the needed information about the Elf file.
2. Data frame : it contains 1600 bytes of data from the hex file.

As our project sequence is that the Pc send 8 bytes (Non Data frame) to the cloud in hex format as string and we should receive 8 bytes from it, we discovered after receiving it, that the data size is 16 bytes not 8 bytes, that’s because each byte of Data is represented as 2 string digits in hex format so we needed an algorithm to convert back the 16 bytes (digits) string to the original 8 bytes Data, then send those 8 Data bytes to the targeted MCU.
![](/Gateway_Node/Images/8.jpg)

To receive the data frame we received it as a string of 3200 hex string digit (the pc sends 200 frames each one of them is 8 bytes so the total number is 1600 byte and we receive those 1600 bytes multiplied by 2 because of each byte is represented as 2 digits in hex format as string so the numbe is 3200 ), we created (TX_string_buffer) and allocated it with 3200 char (3.2k bytes) becouse if it's not initialized with the size corresponding to our data, it will be initialized with the default size and it will corrapt our data

```ino
String TX_string_buffer = "00000…………”
```
Then we had a problem of sending the frames as an array from the PC as firebase Arduino library for esp didn't support receiving an array So we turned to receiving it as string as the size of string in the firebase Arduino library is big and the firebase can also receive and send a large sequence of string
Another problem is that when we receive the string frames on arduino we want to convert the frames first from string to hex values and to parse the hex values to be added into its place in the Txbuffer[8], so we used the functions strtoul to convert the string and the function substring to parse the string into sizes of 1 byte to be added to the buffer, but the problem was that the function strtoul was taking input parameter as a pointer to constant character
so we had to use an Arduino function c_str() to convert the string to pointer to constant character then the function substring to parse the string into characters in size of 1 byte then convert them using strtoul to be added to the Txbuffer[index] and finally we send this Data over UART to STM

```ino 
 Firebase.getString(firebaseData, "Frame");
 TX_Need_Resp_Buffer = firebaseData.stringData();
 
 TxBuffer[0] = strtoul(TX_Need_Resp_Buffer.substring(0,2).c_str()  ,NULL,16);
     .             
     .	 
 TxBuffer[7] = strtoul(TX_Need_Resp_Buffer.substring(14,16).c_str(),NULL,16);
 
 for(int index=0;index<8;index++)
    {
              Serial.write(TxBuffer[index]);
    }
```
 
## References

1. https://randomnerdtutorials.com/how-to-install-esp8266-board-arduino-ide/
2. https://www.javatpoint.com/iot-project-google-firebase-nodemcu
3. https://arduino-esp8266.readthedocs.io/en/latest/exception_causes.html
4. https://github.com/me-no-dev/EspExceptionDecoder
5. https://arduino-esp8266.readthedocs.io/en/latest/faq/a02-my-esp-crashes.html#watchdog
6. https://github.com/mobizt/Firebase-ESP8266/blob/master/README.md
7. https://lastminuteengineers.com/esp8266-nodemcu-arduino-tutorial/
