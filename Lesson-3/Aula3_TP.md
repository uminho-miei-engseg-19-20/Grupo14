# TP Class Assignment - 02/Mar/2020

## Group 14

### Question 1

The modified files were upoloaded to GithHub, on the /Grupo14/Lesson-3/Files folder.

First the Signer calls the init-app.py, with the -init flag, where he generates the pRDashComponents. Then the Signer sends the pRDashComponents to the Requester.

The Requester starts the blind-app.py, where he states which message he wants tho blind and the pRDashComponents received. It also generates three components: **blindComponents**, **pRComponents** and **blindM**.

### Question 2.1

For this exercise we were asked to test the SSL Server test for the designated sites. Being the group 14, we had to choose two sites of companies listed in the NYSE (New York Stock Exchange), and those companies were **American Airlines Group Inc** and **Berkshire Hathaway Inc**.

** *American Airlines Group Inc* test result:** https://www.ssllabs.com/ssltest/analyze.html?d=www.aa.com

** *Berkshire Hathaway Inc* test result:** https://www.ssllabs.com/ssltest/analyze.html?d=www.berkshirehathaway.com

The site with worst rating is that belonging to **American Airlines Group Inc** with a an overall rating of B, while **Berkshire Hathaway Inc** site has an overall rating of A.
Therefore, the **American Airlines Group Inc** shall be the one to be analyzed here.

Analyzing the result of the SSL Server Test to this site, it is quickly noticeable that this site supports the latest TLS Version, version 1.3, which can be read right below the overall rating. It also supports TLS versions 1.2 and 1.1. Furthermore it is relevant to notice that this site possesses a valid certificate and does not have DNS CAA.

In the Cipher Suites section, we can see that it has 5 strong ciphers options to TLS 1.3 and for TLS 1.2 it has 3 strong cipher options plus 10 weak options. All of these weak options present at least one of these "bad smells":

  * The usage of SHA which was withdrawn shortly after publication due to an undisclosed significant flaw. The recommended would be to use SHA-256 or SHA-384 as some of the cipher optins do.

  * A great part of these cipher options make use of CBC mode when GCM would be more recommended, considering GCM is all around safer than CBC and CBC is vulnerable to padding oracle attacks, which exploit the tendency of block ciphers to add arbitrary values onto the end of the last block in a sequence in order to meet the specified block size.

  * Last but not least, we can see that many of them use RSA instead of ECDHE, being this last more secure.

  In the Protocol Details section of the result of the SSL Server test can be read that it is safe against the attacks tested, for example Heartbleed, Zombie POODLE, GOLDENDOODLE, not possessing any of these vulnerabilities.
  In this same section it can also be read the information "Public Key Pinning", which is a security feature that tells a web client to associate a specific public key with a certain web server to decrease the risk of forged certificates attacks. If the server delivers an unknown public key, the user should be warned of such.


### Question 3.1

For this question we chose **American Airlines Group Inc** and **Agilent Technologies**, and after some search on Shodan the respective servers on 192.168.212.154 and 69.12.214.215 were found. The results of the SSH-audit to both servers are in this same repository as text files.

The **American Airlines Group Inc** server is running OpenSSH 5.3 and the **Agilent Technologies** server is running OpenSSH 7.4.

According to cvedetails.com OpenSSH 7.4 has 2 vulnerabilities and OpenSSH 5.3 has 10, being this version the one with the most vulnerabilities from the two analyzed here.

The version (from these two) with the most severe vulnerability is OpenSSH 5.3, that possesses the vulnerability CVE-2014-1692 with a score of 7.5.

Considering it has partial impact on confidentiality, integrity of the data, availability of the service and has Low access complexity with no authentication needed, it could be considered serious. However, as this is an old version of OpenSSH not many severs should be running it.
