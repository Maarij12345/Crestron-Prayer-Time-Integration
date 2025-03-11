# Crestron Prayer Time Integration

This project integrates Crestron systems with an API to fetch daily Islamic prayer times and trigger the Adhan (call to prayer) when the current time matches a prayer time.

## Overview
This guide is divided into two parts:
1. **Fetching Prayer Times** – Retrieving prayer time data from an API.
2. **Playing the Adhan** – Automatically playing the call to prayer when the time matches.

## Part 1: Fetching Prayer Times

To get prayer times, we use the **IslamicFinder API**: https://www.islamicfinder.us/index.php/api

### Example API Endpoint:
```http
GET /index.php/api/prayer_times?country=US&zipcode=44333&juristic=1 HTTP/1.1
Host: www.islamicfinder.us
```
### Example JSON Response
```
{
  "Fajr": "05:30 AM",
  "Dhuhr": "12:45 PM",
  "Asr": "04:15 PM",
  "Maghrib": "07:30 PM",
  "Isha": "09:00 PM"
}
```
We use the Serial I/O symbol to send the api request and then individually parse out the Prayer times. 
![image](https://github.com/user-attachments/assets/ce972ffc-3895-4351-894c-d831bdea6388)

Add the SIMPL+ Modules and the input string would be the JSON response and the string output would be the Prayer parse time string. For example the serial output of Fajr time would be "05:30AM"
![image](https://github.com/user-attachments/assets/1fb4967e-67a0-4c29-ba23-ac7eea9cfe5b)

Since the prayer times update every day at 12:00 AM use a when symbol to parse out the JSON response every day so that it updates.
![image](https://github.com/user-attachments/assets/75eeec6f-c0c7-4b49-9284-557bcd366904)

## Part 2: Playing the Adhan
You would need an oscillator so that everytime the digital output goes high(which is every second), the time match checker SIMPL+ would run
![image](https://github.com/user-attachments/assets/411b7d26-2bb2-464c-b8a3-08f339de23e7)
Because the prayer time string would be parsed out in this format: "5:30AM", you would need a current time string in that same format. Example: if oscollator output goes high, check if current inputstring(12:10PM) is equal to fajir parse string (5:30AM). If it is then send digital output high if not then set digital output low. The program will continously check until the times meet and then the digital output would go high. The reason why this program has to be run like 
![image](https://github.com/user-attachments/assets/077ee9b8-e7bf-4d96-b2d7-7baa4e4df6bc)

