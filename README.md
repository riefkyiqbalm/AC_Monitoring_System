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
    
<img width="1025" alt="gambar_komunikasi" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/Picture/Communication_Design.jpg">
Picture.1 Communication Design

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
- [MQTT Setup](#mqtt_setup)
- [Installation](#installation)
  - [NODE-RED_Installation](#node_red_installation)
  - [XAMPP Installation](#xampp_installation)
- [MySQL Tabel Design](#mysql_tabel_design)
- [UI DESIGN](#ui_design)
- [Acknowledgments](#acknowledgments)

## 🔌 Hardware Wiring <a name = "hardware_wiring"></a>

<img width="1025" alt="gambar_harware_wiring" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/Picture/Hardware_Wiring.jpg">

Picture.2 Hardware Wiring

This is the connection between the bme280 sensor and the microcontroller, in this connection based on 12C protocol which is was the half-duplex communication

<img width="1025" alt="Screenshot 2024-12-11 at 12 20 37 AM" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/Picture/12C_Half_Duplex.jpg">

## 📭 MQTT Setup <a name = "mqtt_setup"></a>

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


