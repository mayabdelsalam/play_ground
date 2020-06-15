# Purpose 

This document describes Firebase, python and Firebase, ELFI gui threads and code flow chart

## Table of Contents
* [What is Firebase](#What-is-Firebase)
* [Firebase Realtime Database](#Firebase-Realtime-Database)
* [Python and Firebase](#Python-and-Firebase)
* [Qt Designer and GUI](#Qt-Designer-and-GUI)
* [Threading in Python](#Threading-in-Python)
* [Steps to operate our GUI and how it workes](#Steps-to-operate-our-GUI-and-how-it-workes)


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

## Threading in Python

### What Is a Thread?
A thread is a separate flow of execution. This means that your program will have two things happening at once. But for most Python 3 implementations the different threads do not actually execute at the same time: they merely appear to.

### Starting a Thread

To start a separate thread, you create a Thread instance and then tell it to .start():

```py
##FetchNodeMCUs Thread Class  
class Import_NodeMCUs(QtCore.QThread):
  ##The initialization function 
  def __init__(self):
      QtCore.QThread.__init__(self)
	    
  ##The runnable of FetchNodeMCUs py file 
  def run(self):
 
	call(["python", "FetchNodeMCUs.py"])
    
    ##pending the Thread for 2Sec  
    time.sleep(2)
    
```

```py
##starting the FetchNodeMCUs Thread
self.fileNodeMCU=Import_NodeMCUs()
self.fileNodeMCU.start()
```

## Steps to operate our GUI and how it workes

![](media/ELFI_v2.JPG)

-   The user interface to our project just open **Elfi.exe** and it will
    direct you to the GUI.
	
-   The GUI runs three different threads in the back ground.
1.  Progress: which is responsible of updating the progress bar in the GUI with the percentage of how much of the hex file has been flashed.
2.  Import: which is responsible of getting elf path from the Text Browser, the timestamp of the choosen elf file then passing them both to the **CommReceive.c** and then running it. 
            Also it runs **FirebaseTrial.py**.
3.  Import_NodeMCUs: which is responsible of running the **FetchNodeMCUs.py**.

-   Press the Refresh button to choose one of the hardware targets, those targets are registersd through each user that has a gateway. 
    The script that does this functionality is **FetchNodeMCUs.py** by getting values of NodeMCUs chiled in firebase and pasteing them in NodeMCUs.txt, leaving them for the GUI to fetch and add them to the drop down list.  
	
-   Browse the **Elf file as (Main_APP.elf)** to flash it to the target

-   Press upload and the following will happen:
1. **CommReceive.c** constructs the Marker Frame from the timestamp passed to it, then parsses the elf file and constructs all the Erase, Data, Verify frames. While it costructs those frames it opens **tst.txt** and pastes those frames in order, starting from the Marker frame.

2. **FirebaseTrial.py** It updates the Marker on the firebase for the gateway to fetch it and compare it to the last verision that it has.
   Then it waits for the choosen target to be connected to the firebase server, if it does not, the Status in the GUI will change to **Target not connected**.
   If it is connected but the choosen elf is the same as the one already flashed the gateway will update the Marker on the firebase with "Same_Marker", then **FirebaseTrial.py** will fetch the Marker from the firebase, if it holds "Same_Marker", it will update the **progress.txt** and the GUI will show **Application already exists** Status.
   If it is not the same application the gateway won't change the Marker on the firebase, and the check in the **FirebaseTrial.py** will lead to the start of the erasing and flashing sequence.
   
3. Erase and flash sequence is: the **FirebaseTrial.py** updates Frame in firebase with the Erase frame and waits for response, if the response is ok it sends 200 Data frames at a time and waits again for response if it is ok, it sends a Verify frame, it repeates the sending of Data and Verify Frames untill all Data frames has benn sent.
   Also while uploading frames it writes in the **progress.txt** the number of sent data blocks and the total number of blocks that needs to be sent, so the GUI can update its progress bar.   
   
-  After finishing the process, the GUI will notify you that the flashing is done.
  





 
## References

1. https://randomnerdtutorials.com/how-to-install-esp8266-board-arduino-ide/
2. https://www.javatpoint.com/iot-project-google-firebase-nodemcu
3. https://arduino-esp8266.readthedocs.io/en/latest/exception_causes.html
4. https://github.com/me-no-dev/EspExceptionDecoder
5. https://arduino-esp8266.readthedocs.io/en/latest/faq/a02-my-esp-crashes.html#watchdog
6. https://github.com/mobizt/Firebase-ESP8266/blob/master/README.md
7. https://lastminuteengineers.com/esp8266-nodemcu-arduino-tutorial/
