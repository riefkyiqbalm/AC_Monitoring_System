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
    
<img width="1025" alt="Screenshot 2024-12-11 at 12 20 37 AM" src="https://github.com/riefkyiqbalm/AC_Monitoring_System/blob/master/Picture/Communication_Design.jpg">
Picture.1 Communication Design

## Disclaimer

This project is for "educational and research purposes only".

- Not intended for real maintenance
- No warranties or guarantees provided
- Past performance does not indicate future results
- Creator assumes no liability for the kind of damage
- Consult a maintenance enginner for maintenance deccision

By using this resource, you agree to use it solely for learning purposes.
