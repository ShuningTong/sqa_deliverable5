# sqa_deliverable5
I found three vulnerabilities for this homework assignment.
## 1. Code Injection Vulnerability
[The URL of the website with the described vulnerability](http://demo.testfire.net/bank/login.aspx)

Steps taken to exploit the vulnerability:

* Open the above url.
* Type ```ZAP' OR '1' = '1' --``` in Username input field and any password in Password input filed.
* Click Login button.
* You will login successfully.

Screenshots:

![](/pics/vul1_site.png)
![](/pics/vul1_zap.png)

1. According to InfoSec Triad, this vulnerability attacks the confidentiality part. I am an unauthorized user, but I can read data like an authorized admin user. This vulnerability also attacks the integrity part. I can edit user information or transfer funds if I want.
2. Interception and modification kind of security attack can exploit this vulnerability. An Interception attack is an attack on confidentiality. Modification attacks modify already-existing data.
3. Attacks that exploit this vulnerability can be active or passive. I can modify admin user information or just eavesdrop.
4. Business value of authorized access would be lost due to exploiting this vulnerability. Users will not trust your business if unauthorized user can read and write data in the system.
5. These steps should be taken to fix this vulnerability:
	- Do not trust client side input, even if there is client side validation in place.  
	- In general, type check all data on the server side.
	- If the application uses JDBC, use PreparedStatement or CallableStatement, with parameters passed by '?'
	- Find all places where user input is accepted and ensure that sending in code will not result in it being executed.


## 2. Command Injection Vulnerability
[The URL of the website with the described vulnerability](http://www.webscantest.com/osrun/whois.php)

Steps taken to exploit the vulnerability:

* Open the above url.
* Type ```ZAP&cat /etc/passwd&``` in the input field and hit Lookup button.
* You will see a list of  all the necessary details about every account in the Linux system like following:

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
```

Screenshots:

![](/pics/vul2_site.png)
![](/pics/vul2_zap.png)

1. According to InfoSec Triad, this vulnerability attacks the confidentiality part. I'm unauthorized, but I'm able to know the information of all registered users. 
2. Interception kind of security attack can exploit this vulnerability. An Interception attack is an attack on confidentiality. 
3. Attacks that exploit this vulnerability is passive. I can read the information, but may not be able to write to it, since the passwd file is only writable by root or superuser.
4. Business value of authorized access would be lost due to exploiting this vulnerability. Users will not trust your business if unauthorized user can read data in the system.
5. These steps should be taken to fix this vulnerability:
	- Ideally, a developer should use existing API for their language. For example (Java): Rather than use Runtime.exec() to issue a 'mail' command, use the available Java API located at javax.mail.*
	- If no such available API exists, the developer should scrub all input for malicious characters. Implementing a positive security model would be most efficient. Typically, it is much easier to define the legal characters than the illegal characters.
	- Run your code in a "jail" or similar sandbox environment that enforces strict boundaries between the process and the operating system. This may effectively restrict which files can be accessed in a particular directory or which commands can be executed by your software.

## 3. Cross-site Scripting Vulnerability
[The URL of the website with the described vulnerability](http://testaspnet.vulnweb.com/ReadNews.aspx?NewsAd=javascript%3Aalert%281%29%3B&id=0)

Steps taken to exploit the vulnerability:

* Open the above url.
* You will see a javascript alert window saying "1".

Screenshots:

![](/pics/vul3_site.png)
![](/pics/vul3_zap.png)

1. According to InfoSec Triad, this vulnerability attacks the confidentiality part, integrity part and availability part. The most severe XSS attacks involve disclosure of the user’s session cookie, allowing an attacker to hijack the user’s session and take over the account so that he or she may read or write. What's worse, hackers can exploit this vulnerability to preform an XMLHttpRequest to the victim domain on a continuous loop to flood the target with rogue GET requests.
2. Interruption, interception and modification kind of security attack can exploit this vulnerability. Interruption attack is focused on availability. Interception attack is on confidentiality. Modification attack modifies already-existing data.
3. Attacks that exploit this vulnerability can be active or passive. If hackers take over user's account information, he or she can read or write.
4. Business value of authorized access, data integrity and service availability would be lost due to exploiting this vulnerability. Users will not trust your business if unauthorized user can read and write data in the system. Data is under risk of lost since hackers can take over user's account. Possible denial of service due to DDoS attack can destroy the reliability of the product.
5. These steps should be taken to fix this vulnerability:
	- Use a vetted library or framework that does not allow this weakness to occur or provides constructs that make this weakness easier to avoid.
	- For any security checks that are performed on the client side, ensure that these checks are duplicated on the server side. Attackers can bypass the client-side checks by modifying values after the checks have been performed, or by changing the client to remove the client-side checks entirely. Then, these modified values would be submitted to the server.
	- For every web page that is generated, use and specify a character encoding such as ISO-8859-1 or UTF-8. When an encoding is not specified, the web browser may choose a different encoding by guessing which encoding is actually being used by the web page. This can cause the web browser to treat certain sequences as special, opening up the client to subtle XSS attacks.