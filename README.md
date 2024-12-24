# AC Monitoring System

In this project i was developing the air conditioner monitoring system to find out the evaporator and condensor filter condition during the COVID-19 pandemic by collected the temperature and humidity data and send it to the dashboard User Interface.

To achieve that goal we need to implement several hardware and software:

1. BME280 - Gathers and sense the temperature and humidity data.
2. ESP32 WEMOS Lolin - Read the data, convert data to digital or analog signal, and send it to the cloud connection. 
3. Router or Mobile Hotspot - Recieve the data and send it to the database.
4. MQTT Protokol - Package the data and ensure the data was have security systems.
5. XAMPP - Turn the client laptop to become SQL server database.
6. SQL Database - Store the data and convert prepared meta data.
7. NODE RED - Design the user interface system to inform the filter condition and the temperature and humidity value.
8. Arduino IDE - Write the program to connect the ESP32, BME280, MQTT, Router and SQL database.
9. DAIKIN Air Conditioner - Object to collect the data.
10. Microsoft Excel - Analyze the data using logistic regression and wilcoxon rank sum test statistical method.
    
<img width="1025" alt="gambar_komunikasi" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/Communication_Design.jpg">
Picture 1 Communication Design

## ❗❗ Disclaimer ❗❗

This project is for "educational and research purposes only".

- Not intended for real maintenance
- No warranties or guarantees provided
- Past performance does not indicate future results
- Creator assumes no liability for the kind of damage
- Consult a maintenance enginner for maintenance deccision

By using this resource, you agree to use it solely for learning purposes.

## 📝 Table of Contents

- [Hardware Wiring](#hardware_wiring)
- [Installation](#installation)
  - [MQTT Setup](#mqtt_setup)
  - [NODE-RED_Setup](#node_red_setup)
  - [XAMPP Setup](#xampp_setup)
- [MySQL Tabel Design](#mysql_tabel_design)
- [UI DESIGN](#ui_design)
- [Acknowledgments](#acknowledgments)

## 🔌 Hardware Wiring <a name = "hardware_wiring"></a>

<img width="1025" alt="gambar_harware_wiring" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/Hardware_Wiring.jpg">

Picture 2 Hardware Wiring

This is the connection between the bme280 sensor and the microcontroller, in this connection based on 12C protocol which is was the half-duplex communication

<img width="1025" alt="half_duplex" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/12C_Half_Duplex.jpg">

Picture 3 Half-Duplex

## 💻 Installation <a name = "installation"></a>

Installation start by [Arduino IDE](https://docs.arduino.cc/software/ide-v1/tutorials/Windows/), [Node-Red](https://nodered.org/docs/getting-started/windows), and [XAMPP](https://www.apachefriends.org/download.html) from the each software website. For the Node-Red installation if you running on windows you must insttall the [node.js enviroment](https://nodejs.org/en/).

### 🔧 MQTT Setup <a name = "mqtt_setup"></a>

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
client.publish("Topic that you want use", "Dataset it mustbe in array data structure");
```
You can use this format value to change your data structure to array and data tipe will be change from float to the string. For more information you can visit this website [documentation](https://www.programmingelectronics.com/dtostrf/).
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
### 🔧 NODE-RED Setup <a name = "node_red_setup"></a>
After the Nodejs and Node-red installation complete you can open the Nodejs CMD and write this command.
 ```
C:\Users\Admin>node-red
```
Node-Red was a web based application, so you must open the latest browser and go to [http://localhost:1880/](http://localhost:1880/). After the Node-Red is fully installed you can manage the pallete, because the MySQL pallete do not installed in Node-Red as default. Go to Pallete ➡️ Install ➡️ Type MySQL in search bar ➡️ Find the library and click install button. It was show in Picture 4 

<img width="400" height = "500" alt="gambar_my_sql" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/MySQL_Library.jpg">

Picture 4 MySQL Library
### 🔧 XAMPP Setup <a name = "xampp_setup"></a>
After XAMPP installed open the XAMPP app ➡️ click start button on the Apache module and SQL module ➡️ go to browser and type [localhost](http://localhost/dashboard/), once you in XAMPP dashboard go to phpMyAdmin ➡️ click new to create a new database or you can see full documentation in [here](https://www.phpmyadmin.net/docs/).

## 📒 MySQL Tabel Design <a name = "mysql_table_design"></a>
You can generate database in MySQL by following this query.
```
CREATE DATABASE NAME_OF_YOUR_DATABASE
CREATE TABLE NAME_OF_YOUR_TABLE (
    FRIST_COLOUMN_NAME TypeData,
    SECOND_COLOUMN_NAME TypeData
);
```



