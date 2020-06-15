# Purpose 

This document describes Firebase, python and Firebase, ELFI gui threads and code flow chart

## Table of Contents
* [What is Firebase](#What-is-Firebase)
* [Firebase Realtime Database](#Firebase-Realtime-Database)
* [Python and Firebase](#Python-and-Firebase)
* [Qt Designer and GUI](#Qt-Designer-and-GUI)
* [Errors Causes and Solutions](#the-errors-causes-and-solutions)


## What is Firebase

<p align="center">
  <img src="media/Firebase_Logo.png">
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
  <img src="media/1_kiliGRYQIVzsCTx_JsUYdg.png">
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
  <img src="media/1.JPG">
</p>

3. Click on add project 

<p align="center">
  <img src="media/2.JPG">
</p>

4. Write down your project name
5. Press Continue

<p align="center">
  <img src="media/3.JPG">
</p>

6. Press Continue

<p align="center">
  <img src="media/4.JPG">
</p>

7. Name your Firebase Acoount

<p align="center">
  <img src="media/6.JPG">
</p>

8. Choose your Analytics location
9. Accept the terms and policy

<p align="center">
  <img src="media/7.JPG">
</p>

10. Press Create project

<p align="center">
  <img src="media/8.JPG">
</p>

11. Press Continue

<p align="center">
  <img src="media/9.JPG">
</p>

12. Time to register your app

<p align="center">
  <img src="media/10.JPG">
</p>

13. Add a nickname to your app
14. Press Register app

<p align="center">
  <img src="media/12.JPG">
</p>


15. Add Firebase SDK, press Next

<p align="center">
  <img src="media/13.JPG">
</p>

16. Install Firebase CLI, press Next

<p align="center">
  <img src="media/14.JPG">
</p>

17. Deploy to Firebase Hosting , press Continue to the console

<p align="center">
  <img src="media/15.JPG">
</p>

### Access your project's info. 

* Press on the icone shown below

<p align="center">
  <img src="media/16.JPG">
</p>

* Get your Web API Key which is used to connect the gateway to firebase

<p align="center">
  <img src="media/17.JPG">
</p>

* Get Firebase SDK snippet used in the pythone script used to upload and download frames

<p align="center">
  <img src="media/18.JPG">
</p> 

## Python and Firebase

FirebaseTrial.py is the script used to:
1. Upload Marker, Erase, Verify and Data frames to our firebase database. 
2. Download and check the responses uploaded to the firebase via the Gateway. 

### Connect python script to Firebase Database

```py
   config = {
  "apiKey": "AIzaSyCLVYhUGxHVeIfLW8DkWPZy7kBu4f1-79o",
  "authDomain": "fota-905e1.firebaseapp.com",
  "databaseURL": "https://fota-905e1.firebaseio.com",
  "projectId": "fota-905e1",
  "storageBucket": "fota-905e1.appspot.com",
  "messagingSenderId": "746270454506",
  "appId": "1:746270454506:web:32183900e0176d27b31d93",
  "measurementId": "G-ZE9JE4FGRP"
    }
#FireBase Initialization     
firebase = pyrebase.initialize_app(config)
db = firebase.database()
```

### Operations done on firebase



* Set value for a certain chiled, or to create the child  

```py
db.child("NodeMCUSemaphore").set(False)
```

* Get value of a particuler child
```py
result = db.child("NodeMCUs").get()
if (result.val() ==  "No_Target_Connected"):
```

## Qt Designer and GUI

### Description:

**First we will start by how we can install Pyside2 to make our GUI:**

Pyside2 is newer than PyQt and supports Python **v3.8.1** so:

1.  First make sure that the version of python you have is 3.8.1 by open CMD and
    write :

**\>\>python –version**

1.  After checking the python version start download Pyside2 using CMD window
    and run this command:

-   **\>\>pip install PySide2**

-   This command will install PySide2 site-packages in the following path

-   **C:\\Program Files\\Python38\\Lib\\site-packages\\PySide2\\**

-   Also will install the PySide2 GUI converter in the following Path

-   **C:\\Program Files\\Python38\\Scripts\\PySide2-uic.exe**

-   Then in the PySide site-package folder you will find designer tool called

-   **designer.exe**

-   Then create shortcut from **designer.exe** of designer app by making **right
    click** the choose **send to -\>desktop**

**Now we have PySide2 designer ……………………………………………………………………………………........**

**Second we will show how we can make our GUI step by step :**

1.  First open Pyside2 just click on **designer.exe,** this page will open

![](media/af7236bb6ee803b4ffe23b4d21e201a7.png)

2.  Then choose Widget and press create button and this form will open

![](media/e94639d2c9e8b09b4c34ad3aa9962963.png)

3.  Now we can make your design of GUI by choosing the components from This list

![](media/57e240cd30a529508889e54695f84cb6.png)

**Now we will see an example to make for example Hardware Family box in our
GUI**

-   First we will choose Combo Box from Component list

![](media/0b6335744af827b4ba9863c96723704f.png)

-   Then we will add it in our form as below

![](media/14ea3fbb80dd94123605bf57145657ae.png)

-   Then we need to add different types of ECU

![](media/bd2bd9df81f6d5dac92e4efb1753a393.png)

-   Then if you need for example to change many options related to Combo Box

1.  **For example name of Qwidget from object Inspector part**

2.  **Changing Qwidget options from property part**

3.  **By adding signal to connect ComboBox with any another component using
    signal/slot editor**

![](media/e140c933d9be01eeeefb3660aee56767.png)

-   Then to show result in GUI mode use **ctrl+R**

![](media/bf9edabba57c00b0f736c28b30286be3.png)

**So in our GUI we used many components as:**

-   **Combo Box**

-   **Label**

-   **Line Edit**

-   **Push Button**

-   **Text Browser**

1.  Then after finishing your GUI design save it in any location you need Then
    go to this location and open CMD and write

**\>\>pyside2-uic File.ui –o File.py**

>   This command used to generate output Python file from File.ui generated from
>   PySide2 designer

1.  Then open File.py and Write Your Logic that you needed to serve your
    application

-   ………………………………………………………………………………………………………………………………….

**Third we will discuss our Extra logic added to our GUI to serve our
Application (Firmware over the air) :**

-   It is the user interface to our project just open **Elfi.exe** and it will
    direct you to the GUI,

-   But first must read the **readme.txt** file in this location and make the
    necessary downloads

-   After finishing the installation open Elfi.exe and Browse the **Elf file as
    (Main_APP.elf)** needed to flash it on the target

-   Then press upload, and our GUI will call first the **CommReceive.c** to add
    all commands needed to flash in Text file (**tst.txt**)

-   Then GUI Python Script will call the **FirebaseTrial.py** to start
    Connection with FireBase and this done in parallel Thread with another
    Thread to update progressbar by the new values added by **FirebaseTrial.py**
    in **Progress.txt** file and this indicate how many number of frames have
    been sent and flashed on our target and also updating the Title from setup
    to n progress to the End according to the number of frames have been flashed

-   Then after finishing the process GUI will noticed you that the flashing done
    .
<p align="center">
  <img src="/media/ELFI_v2.JPG">
</p>

![](media/ELFI_v2.JPG)

>   C:\\Users\\DELL\\Pictures\\Screenshots\\Screenshot (476).png

\\…………………………………………………………………………………………………………………………………………………/


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
