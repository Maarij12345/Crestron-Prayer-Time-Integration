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

Add the SIMPL+ Modules to the prayers that you want to receive the strings from
![image](https://github.com/user-attachments/assets/1fb4967e-67a0-4c29-ba23-ac7eea9cfe5b)


