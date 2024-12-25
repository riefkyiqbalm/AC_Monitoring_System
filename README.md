<p align="center">
  <a href="" rel="noopener">
 <img src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/Air_Conditioner%20v3.jpg" alt="Project Design"></a>
</p>
<h3 align="center">Air Condtioner Monitoring System</h3>

<div align="center">

  In this project i was developing the air conditioner monitoring system to find out the evaporator and condensor filter condition during the COVID-19 pandemic by collected the temperature and humidity data and send it to the dashboard User Interface.

  To achieve that goal we need to implement several hardware and software:

  1. BME280 ➡️ Gathers and sense the temperature and humidity data.
  2. ESP32 WEMOS Lolin ➡️ Read the data, convert data to digital or analog signal, and send it to the cloud connection. 
  3. Router or Mobile Hotspot ➡️ Recieve the data and send it to the database.
  4. MQTT Protokol ➡️ Package the data and ensure the data was have security systems.
  5. XAMPP ➡️ Turn the client laptop to become SQL server database.
  6. SQL Database ➡️ Store the data and convert prepared meta data.
  7. NODE RED ➡️ Design the user interface system to inform the filter condition and the temperature and humidity value.
  8. Arduino IDE ➡️ Write the program to connect the ESP32, BME280, MQTT, Router and SQL database.
  9. DAIKIN Air Conditioner ➡️ Object to collect the data.
  10. Microsoft Excel ➡️ Analyze the data using logistic regression and wilcoxon rank sum test statistical method.

<p align = "center" >
<img alt="gambar_komunikasi" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/Communication_Design.jpg"/>
</p>

<p align = "center" >
Picture 1 Communication Design
</p>

## ❗❗ Disclaimer ❗❗

This project is for "educational and research purposes only".

  - Not intended for real maintenance
  - No warranties or guarantees provided
  - Past performance does not indicate future results
  - Creator assumes no liability for the kind of damage
  - Consult a maintenance enginner for maintenance deccision

By using this resource, you agree to use it solely for learning purposes.

## 📝 Table of Contents

  🔌   [Hardware Wiring](#hardware_wiring)
  💻   [Installation](#installation)
     ⛓️   [MQTT Setup](#mqtt_setup)
    🔴   [Node-Red_Setup](#node_red_setup)
    ⛏️   [XAMPP Setup](#xampp_setup)
  📒  [MySQL Table Design](#mysql_table_design)
  📱   [UI Design](#ui_design)
  🎉  [Acknowledgments](#acknowledgments)

## 🔌 Hardware Wiring <a name = "hardware_wiring"></a>
<p align = "center" >
<img  alt="gambar_harware_wiring" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/Hardware_Wiring.jpg"/>
</p>

<p align = "center" >
Picture 2 Hardware Wiring
</p>
  This is the connection between the bme280 sensor and the microcontroller, in this connection based on 12C protocol which is was the half-duplex communication
  
<p align = "center" >
<img alt="half_duplex" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/12C_Half_Duplex.jpg"/>
</p>

<p align = "center" >
Picture 3 Half-Duplex
</p>

## 💻 Installation <a name = "installation"></a>

  Installation start by [Arduino IDE](https://docs.arduino.cc/software/ide-v1/tutorials/Windows/), [Node-Red](https://nodered.org/docs/getting-started/windows), and [XAMPP](https://www.apachefriends.org/download.html) from the each software website. For the Node-Red installation if you running on windows you must insttall the [node.js platform](https://nodejs.org/en/).

  ### ⛓️ MQTT Setup <a name = "mqtt_setup"></a>

  This project was using mousquito eclipse MQTT broker, to connect the microcontroller to broker write this following code below in your Arduino IDE.

  - Import Library
```
  #include <PubSubClient.h>
```
  - Define the Variable of Broker as a server and Microcontroller as a Client.
```
  const char* mqtt_server = "test.mosquitto.org";
  PubSubClient client(espClient);
```
  - Write this code in the "void setup()" function.
```
  client.setServer("Broker_Address", "PORT that you use");
```
  In this project based on the mousquitto [information](https://test.mosquitto.org/) we use the 1883 port.
  - To send your data to MQTT server you can use this code below.
```
  client.publish("Topic that you want use", "DataVariabelName");
```
  We must change the data type from float to stting because in Node-Red application data will be combaine in array data sturcture. You can use dtostrf() function to change your data tipe from float to the string. For more information you can visit this website [documentation](https://www.programmingelectronics.com/dtostrf/).
```
dtostrf ("Float variabel_name that contain you data","How many digit your data","The precision your data","Array Name");
```
If the connection was failed you can develop this function.
```
void reconnect() {
  // Reconnect loop 
  while (!client.connected()) {
    Serial.print("Attempting MQTT connection...");
     String clientId = "ESP32Client-";
      clientId += String(random(0xffff), HEX);

      // If the reconnection was succes
      if (client.connect(clientId.c_str()))  {   
      Serial.println("connected");
      }
```
  ### 🔴 Node-Red Setup <a name = "node_red_setup"></a>
  After the Nodejs and Node-Red installation complete you can open the Nodejs CMD and write this command.
 ```
  C:\Users\Admin>node-red
```
  If there is no error massage you must open the lastest browser because Node-Red was a web-based application and go to [http://localhost:1880/](http://localhost:1880/). After the Node-Red is fully installed you can manage the pallete, because the MySQL pallete do not installed in Node-Red as default. Go to Pallete ➡️ Install ➡️ Type MySQL in search bar ➡️ Find the library and click install button. It was show in Picture 4.

<p align = "center" >
<img width="400" height = "500" alt="gambar_my_sql" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/MySQL_Library.jpg"/>
</p>


<p align = "center" >
Picture 4 MySQL Library
</p>

  ### ⛏️ XAMPP Setup <a name = "xampp_setup"></a>
  After XAMPP installed open the XAMPP app ➡️ click start button on the Apache module and SQL module ➡️ go to browser and type [localhost](http://localhost/dashboard/), once you in XAMPP dashboard go to phpMyAdmin ➡️ click new to create a new database or you can see full documentation in [here](https://www.phpmyadmin.net/docs/).

## 📒 MySQL Table Design <a name = "mysql_table_design"></a>

You can generate database in MySQL by following this query.
```
CREATE DATABASE NAME_OF_YOUR_DATABASE
CREATE TABLE NAME_OF_YOUR_TABLE (
    FRIST_COLOUMN_NAME TypeData,
    SECOND_COLOUMN_NAME TypeData
);
```
  Picture 5 show the example database in this project with 4 column name (ID, Temperature Masuk (_Temperature in_), Humidity Masuk (_Humidity in_), Tanggal (_Date_).

<p align = "center" >
<img alt="gambar_my_sql" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/Data_Storing.jpg"/>
</p>


<p align = "center" >
Picture 5 MySQL Example
</p>

## 📱 UI Design <a name = "ui_design"></a>

  Picture 6 show us about this project Node-Red block configuration and Picture 7 showed the result of our design dashboard. Each blocks in picture 6 need to be configurate, so i am attached a file with a name ["Node-Red configuration"](https://github.com/riefkyiqbalm/AC_Monitoring_System/tree/master/Node-Red%20Configuration) in this repostory which is contain picture of all block configuration.

<p align = "center" >
<img alt="block_configurate" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/Node-RED_design.jpg"/>
</p>


<p align = "center" >
Picture 6 Block Configuration
</p>

<p align = "center" >
<img alt="dashboard_result" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/UI_Node-RED.jpg"/>
</p>

<p align = "center" >
Picture 7 Dashboard Example
</p>

To get more clear information this is was the function of each block.

  - Purple color block (communication block) ➡️ Recieve a message that contain data from router/mobile hotspot and inject it to block with the blue color and yellow color.
  - Blue color block (dashboard block) ➡️ Display the data to the dashbord with GAUGE fitur.
  - Yellow color block (array bloc) ➡️ Combaine two message from MQTT Broker and store it in array data structure.
  - Cream color block (function block) ➡️ Recieve the array dataset and store it to the variabel and send it to the MySQL database.
  - Green color block (Payload Block) ➡️ Inform the developer about the dataset condition (for debugging) before data send it to the MySQL database.
  - Orange color block (SQL block) ➡️ Initiation the database address, name and user.

## 🎉 Acknowledgments <a name = "acknowledgments"></a>

This project was my final project during my time as student at Islamic University Of Indonesia. Special thank's for my lecturer because I can't completed this project without 
my lecturer ([Agung Nugroho Adi, ST., MT](https://mechanical.uii.ac.id/agung-nugroho-adi-st-mt/)) feedback and insight and for the mor information you can read my [full 
report](https://dspace.uii.ac.id/handle/123456789/33358).




