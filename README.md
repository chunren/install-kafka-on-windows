![[](http://localhost:4200/?repoName=intall-kafka-on-windows&versionNumber=1.0.0)](http://localhost:4200/?repoName=intall-kafka-on-windows&versionNumber=1.0.0)
http://localhost:4200/?repoName=intall-kafka-on-windows&versionNumber=1.0.0
# How To Set Up Apache Kafka on Window 10

By Chunren Lai, Dec. 12, 2020

This article lists steps to install and run Apache Kafka on Windows 10.

## Table of Contents  
[1. Introduction](#1-Introduction)  
[2. Download Files](#2-Download-Files)  
[3. Install the 7zip and Notepad++](#3-Install-the-7zip-and-Notepad-plus-plus)  
[4. Install the Java Runtime](#4-Install-the-Java-Runtime)  
[5. Install ZooKeeper](#5-Install-ZooKeeper)  
[6. Install and Set up Kafka](#6-Install-and-Set-up-Kafka)  
[7. Test Apache Kafka](#7-Test-Apache-Kafka)  

## 1. Introduction
To run Apache Kafka on a windows OS, you will need to download , install, and set up Java, ZooKeeper, and Apache Kakfa. After set up the Apache Kafka, we will run some commands to produce and consume some messages on a test topics on Kafka to ensure Apache Kafka is running properly.

## 2. Download Files
- Upzip and Text Editor tools  
  - If you don't have 7-zip installed on your windows, you are recommended to download the 7-zip from (https://www.7-zip.org/download.html). If your system is 64-bit x64, you can download the exe installer from (https://www.7-zip.org/a/7z1900-x64.exe)
  - You are also recommended to download the text editor Notepad++ from (https://notepad-plus-plus.org/downloads/)
- JRE download
  - You can download the Java runtime from Oracle site ( http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) based on your CPU architecture.
- ZooKeeper download
  - You can download the ZooKeepr from Apache site ( http://zookeeper.apache.org/releases.html)
- Kafka download
  - You can download the Apache Kafka from Apache site ( http://kafka.apache.org/downloads.html)

  The following is a list of my downloads.
 
 ![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/kafka_downloads_chunren_lai_2020.png)


## 3. Install the 7zip and Notepad plus plus
You can directly run the executable installer (e.g., "7z1900-x64.exe" and "npp.7.8.8.Installer.x64.exe")

## 4. Install the Java Runtime
You can run the JRE installer (e.g., "jre-8u271-windows-x64.exe"), and install the Java in its default installation folder (e.g., "C:\Program Files\Java\jre1.8.0_271").
After the installation, you need to set up:
- Environment variable for JAVA_HOME
  Open the "Control Panel" -> "System" -> "Advanced system settings" -> "Environment Variables" -> "System variables" ("New"):

| Item | Value |
| ------ | ------ |
| Variable name | JAVA_HOME|
| Variable value | Java installation folder (e.g., "C:\Program Files\Java\jre1.8.0_271") |


![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/environment_variables_chunren_lai_2020.png)

![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/java_home_chunren_lai_2020.png)

- Add Java path to the "Path" variable
  Select "Path" of the "System variable" section, and the click "Edit..." button to add the java path. In the "Edit environment variable" pop up window, click the "New" button, and add:
```sh
%JAVA_HOME%\bin
```

![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/java_home_bin_chunren_lai_2020.png)

## 5. Install ZooKeeper
- Use 7zip to unzip the ZooKeepr's installation file (e.g., "apache-zookeeper-3.6.2-bin.tar.gz"). You will need to unzip it twice to get the original files.
  ![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/zookeeper_unzip_chunren_lai_2020.png)
- After you fully unzip it, you will have a folder like:
C:\temp\KafkaDownloads\apache-zookeeper-3.6.2-bin.tar\apache-zookeeper-3.6.2-bin\apache-zookeeper-3.6.2-bin
- Move the unzipped bin folder to C:\, and rename it as: C:\zookeeper-3.6.2, and you will see:
    ![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/zookeeper_installfolder_chunren_lai_2020.png)
- Rename the "C:\zookeeper-3.6.2\conf\zoo_sample.cfg" to be "C:\zookeeper-3.6.2\conf\zoo.cfg" 
- add a subfolder "data" under "C:\zookeeper-3.6.2"
- Use Notepad++ to edit the "C:\zookeeper-3.6.2\conf\zoo.cfg" for:
 ```sh
dataDir=C:/zookeeper-3.6.2/data
```
- Similar to the above Java installation, 
1) to add a variable of "ZOOKEEPER_HOME" to the System Variables:
  
| Item | Value |
| ------ | ------ |
| Variable name | ZOOKEEPER_HOME|
| Variable value | C:\zookeeper-3.6.2 | 

![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/zookeeper_home_chunren_lai_2020.png)

 2) to add "%ZOOKEEPER_HOME%\bin" new entry to the System Variable "Path" 

![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/zookeeper_home_path_chunren_lai_2020.png)
- Start the ZooKeeper, by
1) type "cmd" in the Search area (bottom left side)
  2) in the commond line, type 
```sh
cd c:\zookeeper-3.6.2\bin
```
3) type "zkserver", and you will see: 
![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/zookeeper_running_chunren_lai_2020.png)


## 6. Install and Set up Kafka
- Use 7zip to unzip the Kafka's installation file (e.g., "kafka_2.13-2.7.0.tgz"). You will need to unzip it twice to get the original files.
- After you fully unzip it, you will have a folder like:
C:\temp\KafkaDownloads\kafka_2.13-2.6.0\kafka_2.13-2.6.0\kafka_2.13-2.6.0
![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/kafka_unzip_chunren_lai_2020.png)
- Move the unzipped folder to C:\, and rename it as: C:\kafka, and you will see:
    ![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/kafka_installfolder_chunren_lai_2020.png)
- Make a new subfolder C:\kafka\kafka-logs
- Edit the  C:\kafka\config\server.properties, modify the following line with the new value:
```sh
log.dirs=c:/kafka/kafka-logs
```
- If you plan to run Kafka on your loacal machine with other default settings, you are ready to go, otherwise you can change the following default setting:
  zookeeper.connect=localhost:2181 with a proper IP address and a custom port number.
- Open a new command prompt, and:
1) type: 
```sh 
cd c:\kafka, and press enter
```
  2) then press "Enter", and type: 
  ```sh
  .\bin\windows\kafka-server-start.bat .\config\server.properties
  ```
  , and press enter, you will see:
   ![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/kafka_running_chunren_lai_2020.png)
  3) Now you finish installing and setting up Apache Kafka, and the Kafka server is up running.

## 7. Test Apache Kafka
- ### Create a topic called "StudentImport"
 1) Open a new command prompt, and type: cd c:\kafka\bin\windows, press enter
 2) type:
```sh
kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic StudentImport
```
  3) Now the "StudentImport" has been successfully created. See below:
   ![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/kafka_topic_studentImport_chunren_lai_2020.png)

- ### Create a Producer to the Kafka server
 1) Open a new command prompt (called producer command window "P"), and type: cd c:\kafka\bin\windows, press enter
 2) type: 
```sh
kafka-console-producer.bat --broker-list localhost:9092 --topic StudentImport
```
  3) Now it is ready for you to enter any message in the Producer console. See below:
   ![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/kafka_producer_ready_chunren_lai_2020.png)

- ### Create a Consumer to the Kafka server
1) Open a new command prompt (called consumer command window "C"), and type: cd c:\kafka\bin\windows, press enter
2) type: 
```sh 
kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic StudentImport
```
  3) Now it is listening any messages in the Producer console. 

- ### Testing message communications
1) In the producer command window "P" (see above), when you type: "Hello, it is Chunren", and press enter, then in the consumer command window "C" (see above), you will see the message "Hello, It is Chunren" being displayed.
  2) In the producer command window "P", when you type: "We are going to import student rosters soon.", and press enter, then in the consumer command window "C", uou will see the message "We are going to import student rosters soon." being displayed.
  3) See below the results:
In the producer command window "P":
![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/kafka_producer_window_chunren_lai_2020.png)
In the consumer command window "C":
![N|Solid](https://raw.githubusercontent.com/chunren/markdown-src/master/raw/images/kafka_consumer_window_chunren_lai_2020.png)

#### Congratulations! You have successfully set up Apache Kafka on your Windows 10.


![[](http://localhost:4200/?repoName=intall-kafka-on-windows&versionNumber=1.0.1)](http://localhost:4200/?repoName=intall-kafka-on-windows&versionNumber=1.0.1)
