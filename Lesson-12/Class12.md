# Class 12 - TP Class Assignment
## Group 14
### Question 1.1 - SQL Injection
We will present what was asked in every exercise, and show how we solved each one.
- **1 -** This first page presents only the goals expected to be achieved at the lesson.

- **2 -** The second page gives an introduction to what SQL is, with a brief explanation about databases and an example of a table called "Employees" from a database. Then it asks us to try to retrieve the department of the employee Bob Franco, and is important to note that in this exercise we have Administrator privileges. So this can be solved with:
```SQL
SELECT department FROM Employees 
WHERE first_name='Bob' 
AND last_name='Franco'
```
  
- **3 -** Here is given a small introduction to DML (Data Manipulation Language) and we are asked to change the department of Tobi Barnett to "Sales". This can be achieved with:
```SQL
UPDATE Employees
SET department='Sales'
WHERE first_name='Tobi'
AND last_name='Barnett'
```

- **4 -** On this page it gives a simple definition of DDL (Data Definition Language) and examples of DDL commands. The exercise here is to add the column "phone" to the table, which can be solved with:
```SQL
ALTER TABLE Employees 
ADD phone varchar(20)
```

- **5 -**  Introduction to DCL (Data Control Language), which is used to provide security to database objects, by granting or revoking acess privileges to the users. We are required to grant the user group "UnauthorizedUser" the right to alter tables, by doing so:
```SQL
GRANT ALTER TABLE TO UnauthorizedUser
```

- **6 -** Here is explained what is SQL Injection and how can it occur and we are asked to insert some SQL in the query to see how it changes, for which we used the 3 examples given in that same page.

-  **7 -** On this page there is only theory, explaining what a successful SQL Injection exploit can do and what these attacks allow attackers to do. There is no action requested from the user.

- **8 -** On this page is given some more insight regarding SQL Injection attacks, about it's limitations, in what languages this type of attack is more common, and so on. No action is requested from the user.

- **9 -** This page challenges the user to manipulate the query in order to retrieve all the users from the table. This was accomplished with the query:
```SQL
SELECT * FROM user_data 
WHERE first_name = 'John' 
AND last_name= '' 
OR '1'='1'
```
The fact that ```1 = 1``` is always true for every row of the table allows us to retrieve all the users.

- **10 -** This page is aimed at numeric SQL Injection, and it has two fields to fill, but only one is susceptible to SQL Injection. We are required to find out which one and to exploit it to retrieve all the data. Analyzing the query in the code, we can see that the User_Id field is susceptible to SQL Injection as it is in the end of the query and has the form ```user_id = " + User_ID;``` which allows us to exploit it with the values:
**Login_Count:** 1  (for example)
**User_Id:** '1' OR True

- **11 -** The lesson on this page is aimed at compromising the confidentiality of the data, using String SQL Injection. In this exercise we are given a name and a TAN because every employee in this company can check their own data. However, to exploit the system and retrieve other empoyees' data we will have to exploit this, by using:
**Employee Name:** Smith' OR True - - 
**Authentication Tan:** As in the previous field we comment the rest of the query related to the Authentication Tan, the value passed here doesn't make any difference.

- **12 -** This exercise is aimed at SQL chaining, which is defined as appending one or more queries to the end of the actual query, utilizing de ```;``` character to separate queries. We are required to change the user's salary to be the one who earns the most, so we fill the fields like this:
**Employee Name:** Smith
**Authentication TAN:** 
```SQL
'; UPDATE Employees SET salary=1231231 WHERE last_name='Smith' --
```

- **13 -** This last exercise has the objective of compromising availability, and it suggests that we delete completely the table **access_log** to hide our actions. Therefore, to delete a table we drop it as shown:
```SQL
'; DROP TABLE access_log --
```

### Question 2.1 - XSS (Cross Site Scripting)

- **1 -** On this page no action is requires as is only given an overview on the objectives.

- **2 -** Here is given a brief overview over what is XSS and as exercise it is required to check is the cookies are the same in each tab, which is verified as is shown in the screenshots in the same directory as this report. To do this we opened the developer console and used:
```JS
alert(document.cookie);
```

- **3 -** In this page no action is required. Instead it explains which are the most common locations, in which we can see that is very common especially when the component echoes user supplied data or text.

-  **4 -** Again, in this page is not required any action, serving instead an informative purpose regarding what can be achieved with XSS attacks, like stealing session cookies, redirecting the page to a non-friendly site, stealing confidential information, to give a few examples.

- **5 -** This page talks about the different types of XSS, which divide in Reflected, DOM-based (which is also technically reflected) and Stored/Persistent. There is no required action.

- **6 -** Here is explained more in depth how Reflected XSS attacks work, which basically consists of an attacker sending a malicious URL to the victim, who clicks the link, allowing the malicious script embedded in the URL to execute in the victim's browser, stealing sensitive information and releasing it to the attacker. No action is required on this page.

- **7 -** In this page we are supposed to find out which field is susceptible to a Reflected XSS attack, which can be done by following the suggestion of inserting one of those methods in the fields. We found out it's the Credit Card Number field that is vulnerable, passing as input:
```JS
<script>alert()</script>
```
This outputs an empty alert window, revealing the susceptibility to Reflected XSS attacks on this field.

- **8 -** This is yet again just an informative page, differentiating Self XSS and reflected XSS. No action is required here.

- **9 -** Another informative page, this time about Reflected and DOM-Based XSS and the characteristics of these attacks. No action required.

- **10 -** In this exercise aimed at DOM-Based XSS, we are required to find what is the route for the test code. To find this, we first open the debugger, and go to the file GoatRouter.js in the **view** directory, and we can see that the part of the code refering to routes has one called *test*. So the answer is ```start.mvc#test```.

- **11 -** In this exercise we are challenged to try a DOM-Based XSS attack, by executing the function **webgoat.customjs.phoneHome()**, and to do this we must go to ```localhost:8080/WebGoat/start.mvc#test/<script>webgoat.customjs.phoneHome()<%2Fscript>```
Then we must open a console in the developer tools, where we will be able to see the result and use that number to complete the test.

- **12 -** In this last page we must complete a quiz, and to do so we must check the OWASP Cross-Site Scripting explanations. The answers are:
**1-** Option 4;
**2-** Option 3;
**3-** Option 1;
**4-** Option 2;
**5-** Option 4.

### Question 3.1 - Password Reset

- **1 -** Page with the goals of the class.

- **2 -** This page serves the only purpose of checking if we can use WebWolf.

- **3 -** This page explains how to find out if an account exists, which can be shown by the message that appears when trying to reset the password, considering it can be different when one has an account in the website or not.

- **4 -** In this page we learn about Security questions and its risks, because the only correct way of using this is if the user creates his own question amd type in the answer. It has a small challenge that consists in finding the answer to a security question of one of the given users. For this we chose the user **admin** and by successive attempts (brute force) we found out the answer for this user's favorite color is **green**. We also found that the answer to the user **tom** is **purple**,  and for **larry** it's **yellow**.

- **5 -** This page is aimed at the problems with security questions and as exercise we have to choose two questions to see which is the problem with them. The results were:
**What is your favorite animal?**
Problem: The answer can easily be guesses and figured out through social media.
**Who was your childhood hero?**
Problem: Most heroes we had as a child were quite obvious ones.

- **6 -** This page has aims at creating a password reset link to the user Tom with the email tom@webgoat-cloud.org.

- **7 -** Here is presented a summary of what was talked about in this class on password reset, mentioning topics such as "How to use security questions for user verification", "Sending data over the network", "Two factor authentication", among others.

### Question 4.1 - Vulnerable Components

- **1 -** This page works as an introduction to the topic of Vulnerable components, presenting also the goals of this class.

- **2 -** This page gives a brief overview on the Open Source Ecosystems topic, like an estimative of the number of repositories and the difference between some of them.

- **3 -** On this page is presented the 2013 OWASP Top 10 - A9.

- **4 -** On this page, to give an example of how components are everywhere, is given the example of webgoat, which uses almost 200 Java and Javascript libraries. It is also shown that when this class was created, webgoat contained more than a dozen high security risks within it's components.

- **5 -** On this page is shown an example of an exploit found in one of the used libraries, which allows the user to specify the content of the "close text" button for the jquery-ui dialog.

- **6 -** Here is presented the concept of "Bill of materials" in software development and some questions to which we should know the answer to, for example "How do we define the risk of open source components?" and "How do we know if a new vulnerability is found on what was previously a "good" component?".

- **7 -** Here is explained how to generate the Bill of materials, and is given the example of OWASP Dependency Check, a tool that provides the ability to generate a bill of materials and identify potential security risk.

- **8 -** The class here aims at Security Information Overload, answering questions like "What's important?" and giving an overview of how security information is everywhere.

- **9 -** Here is the same as the previous page but with another topic, being this one aimed at License information overload.

- **10 -** This one talks about Architecture Information, talking about what's important to know and giving a brief summary, comparing the components' use versus the vulnerabilities.

- **11 -** In this page two examploes of OSS Risk are given, being one of them the Apache Commons Collections in 2015 and the other one the Dinis Cruz and Alvaro Munoz exploit of XStream.

- **12 -** In this page close to the end, we are challenged to exploit CVE-2013-7285 (XStream), by entering the XML which represents a contact directly in the given text box.

- **13 -** Finally, a brief summary is given about the topic of this class, denoting that **Open source components are the new attack vector**.


