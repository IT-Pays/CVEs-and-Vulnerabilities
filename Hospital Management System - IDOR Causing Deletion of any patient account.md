Exploit Title: CVE-2024-11073 Hospital Management System - IDOR Causing Deletion of any patient account

Application: Hospital Management System

Date: 11.09.2024

Bugs: IDOR 

Exploit Author: Salah Tayeh

Vendor Homepage: https://www.sourcecodester.com/

Software Link: https://www.sourcecodester.com/php/16720/free-hospital-management-system-small-practices.html

Version: 1.0

# Description
Insecure Direct Object References (IDOR) vulnerability in the "Vaidya Mitra" healthcare Hospital Management System 1.0, specifically in the patient's "Delete Account" feature. 
The issue arises due to broken access control on the ID parameter, allowing an attacker to delete any patient account permanently.

# Proof of Concept (PoC)

1. Login as a patient
1. Go to http://localhost/vm/patient/settings.php
1. Attempt to delete the account and before confirming with yes intercept the request in Burp Suite 
1. Send the request POST /vm/patient/delete-account.php?id=9 HTTP/1.1 to repeater in Burp Suite
1. Modify the id parameter value to that of another patient to delete their account permanently


**PoC Video** https://drive.google.com/file/d/1yFo0re8taTry7oR4-EDg3UHwO2lkqO9N/view
