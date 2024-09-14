# Machine - Glider



This is a machine I have completed in the past with an XXE / XEE XML External Entity


## demo.php


When filling out the form box at `/demo.php` we are able to do XEE / XML  related attack

![Pasted image 20240719111338](https://github.com/user-attachments/assets/1b36973b-7501-47ad-a191-6d8aecb317a0)




using [HackTricks](https://book.hacktricks.xyz/pentesting-web/xxe-xee-xml-external-entity) we are able to get the `/etc/passwd` file to display 

![Pasted image 20240719111504](https://github.com/user-attachments/assets/497c2723-1a1c-4db6-a337-ea14e0863208)



We are also able to obtain the users flag `steven` 

![Pasted image 20240719111621](https://github.com/user-attachments/assets/73ff1436-176a-47bc-a64b-05f20332e7e3)



We can use this to look at source code of the webpage using php filters and converting to base64


## Read the src luke


### The payload

```
<!DOCTYPE replace [<!ENTITY example SYSTEM "php://filter/convert.base64-encode/resource=/var/www/html/demo.php"> ]>

<users><name>&example;</name>


```


![Pasted image 20240719111931](https://github.com/user-attachments/assets/84f24438-bfa3-4cba-97e1-0a858c05d084)



copy and paste the output to a file:

`cat demo.b64| base64 -d > demo.php`

![Pasted image 20240719112014](https://github.com/user-attachments/assets/bd6f374c-3fb2-446d-993c-5efabe2bfc7c)


## The Plan

We will be using python to get back the base64 of the source code of the web page 



### Libraries 

- base64
- requests
- beautifulsoup
- argparse
