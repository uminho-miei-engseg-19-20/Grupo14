**Question P1.1**

The higher the number the more entropy needed.When using 1024 with random there isn't enough entropy to satisfy the request for random numbers that is why it is taking a long time. While in urandom that is using a seed that the operating system has generated and it's with enough entropy to generate pseudo-randomness
        
**Question P1.2**

Haveged was created to remedy low-entropy conditions so when using random id does not take a long time anymore to generate random bytes.

**Question P2.1**
	
	user@CSI:~/Aulas/Aula2/ShamirSharing$ openssl genrsa -aes128 -out mykey.pem 1024Generating RSA private key, 1024 bit long modulus
```
		user@CSI:~/Aulas/Aula2/ShamirSharing$ openssl req -key mykey.pem -new -x509 -days 365 -out mykey.crt
		Enter pass phrase for mykey.pem:
		You are about to be asked to enter information that will be incorporated
		into your certificate request.
		What you are about to enter is what is called a Distinguished Name or a DN.
		There are quite a few fields but you can leave some blank
		For some fields there will be a default value,
		If you enter '.', the field will be left blank.
		-----
		Country Name (2 letter code) [AU]:PO
		State or Province Name (full name) [Some-State]:kevin kevin
		Locality Name (eg, city) []:damascus
		Organization Name (eg, company) [Internet Widgits Pty Ltd]:kk
		Organizational Unit Name (eg, section) []:it
		Common Name (e.g. server FQDN or YOUR name) []:kevin

		user@CSI:~/Aulas/Aula2/ShamirSharing$ python createSharedSecret-app.py 8 5 kevin mykey.pem
		Private key passphrase: hello
		Secret: Now we have an extremely confidential secret

		user@CSI:~/Aulas/Aula2/ShamirSharing$ python recoverSecretFromComponents-app.py 5 kevin /home/user/Aulas/Aula2/ShamirSharing/mykey.crt

		user@CSI:~/Aulas/Aula2/ShamirSharing$ python recoverSecretFromAllComponents-app.py 5 kevin /home/user/Aulas/Aula2/ShamirSharing/mykey.crt

		user@CSI:~/Aulas/Aula2/ShamirSharing$ python recoverSecretFromAllComponents-app.py 8 kevin /home/user/Aulas/Aula2/ShamirSharing/mykey.crt
```


We should use recoverSecretFromAllComponents-app.py instead recoverSecretFromComponents-app.py when we need all secret holders to unlock the secret.

For example:

Problem: Company XYZ needs to secure their vault's passcode. They could use something standard, such as AES, but what if the holder of the key is unavailable or dies? What if the key is compromised via a malicious hacker or the holder of the key turns rogue, and uses their power over the vault to their benefit?

This is where SSS comes in. It can be used to encrypt the vault's passcode and generate a certain number of shares, where a certain number of shares can be allocated to each executive within Company XYZ. Now, only if they pool their shares can they unlock the vault.

The threshold can be appropriately set for the number of executives, so the vault is always able to be accessed by the authorized individuals. Should a share or two fall into the wrong hands, they couldn't open the passcode unless the other executives cooperated.

**Question P3.1**



**Question P4.1**

Spain Qualified Certificate issued by Autoridad de Certificación de los Registradores - AC Interna:

```
user@CSI:~/Aulas/Aula2$ fold -w67 cert.crt > cert1.crt
user@CSI:~/Aulas/Aula2$ openssl x509 -in cert1.crt -text -noout
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            19:03:bc:e3:42:82:77:60:57:55:8a:f9:e9:b7:7e:2b
    Signature Algorithm: sha512WithRSAEncryption
        Issuer: C = ES, 2.5.4.97 = VATES-Q2863012G, O = Colegio de Registradores de la Propiedad y Mercantiles, CN = Autoridad de Certificaci\C3\B3n Ra\C3\ADz de los Registradores
        Validity
            Not Before: Jun  6 14:38:48 2016 GMT
            Not After : Jun  6 14:38:48 2028 GMT
        Subject: C = ES, 2.5.4.97 = VATES-Q2863012G, O = Colegio de Registradores de la Propiedad y Mercantiles, CN = Autoridad de Certificaci\C3\B3n de los Registradores - AC Interna
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (4096 bit)
                Modulus:
                    00:93:02:8c:36:fc:e5:25:ab:14:a6:29:ed:d1:5a:
                    16:e1:67:d7:1f:f2:6f:d0:c6:92:ce:fb:08:f9:51:
                    21:c7:47:a3:c7:cf:05:ec:b3:78:0b:a8:0c:72:c5:
                    6c:73:d0:dc:87:96:60:d4:11:ab:a7:da:af:5a:52:
                    78:da:62:c2:9f:e5:59:c2:a4:ee:0d:ad:ae:58:9b:
                    2e:e6:e1:28:ec:6f:39:c9:a8:62:11:5c:08:1a:bb:
                    0d:ba:fb:fe:22:8b:c4:97:01:16:36:08:63:98:70:
                    ac:df:c1:22:e5:04:25:d1:39:77:b2:9a:c5:c9:33:
                    26:5c:2b:32:24:6b:08:94:ff:49:7a:ba:21:0a:ab:
                    2b:eb:7e:7e:24:51:6d:f0:01:70:66:a6:7b:ef:0e:
                    87:68:14:91:1d:aa:22:f4:1a:d7:5c:80:39:3b:48:
                    9e:64:b8:9e:c1:63:ac:7f:ca:e6:83:a3:cd:97:e6:
                    e1:0a:74:2f:3c:5a:c7:c8:05:8a:25:a6:66:14:25:
                    30:a2:f1:7a:43:c5:c1:e4:15:81:7c:c3:13:77:42:
                    6f:03:78:b6:27:e0:cc:23:07:4e:41:1b:cc:28:0d:
                    3f:7c:ac:b9:e9:f0:c8:02:4a:33:4f:5f:02:d3:b3:
                    07:dd:d9:c3:72:ff:2d:0a:3d:77:24:d7:16:b4:f5:
                    32:23:4c:23:81:21:16:f4:de:1f:fd:ed:51:db:9c:
                    b2:cc:8e:9a:07:84:ba:e3:17:52:2f:c4:cc:97:c2:
                    13:24:a0:ba:3b:73:c7:4c:7c:62:5b:d3:7f:c2:6f:
                    18:50:85:1f:78:8b:0f:db:89:bb:df:69:53:12:08:
                    6c:c4:06:b3:d2:ae:6e:fc:b5:91:e2:39:0f:15:08:
                    1d:84:f5:98:bc:dc:ef:8a:c3:9f:7b:fb:c3:1a:f4:
                    80:b3:9e:11:51:4d:be:93:60:ab:e2:73:41:49:1b:
                    ba:e9:df:55:e0:a4:b9:70:11:81:a2:e9:c1:ee:fc:
                    6c:32:95:ce:ca:c0:24:da:f8:93:9c:b3:5f:8d:24:
                    fc:7c:38:93:97:30:cf:6d:fa:0e:98:4b:df:9a:b0:
                    96:4f:66:83:03:7a:a7:8e:12:95:21:85:5a:6f:3e:
                    98:4f:18:00:f9:4c:74:02:b4:1d:7b:a1:8c:a5:f1:
                    8f:15:02:32:7b:48:ca:81:f8:a5:24:61:e7:20:7c:
                    72:9c:4b:43:4e:14:75:ca:27:dd:6b:07:58:d7:b8:
                    23:0c:61:2a:02:59:9c:03:e0:b5:ec:45:96:c5:f4:
                    9c:a2:b4:44:31:5d:fe:dc:57:fc:85:13:1f:54:6c:
                    25:1a:4b:f5:b6:c9:7b:5e:ac:c3:04:b1:1b:4b:8c:
                    de:52:ef
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Basic Constraints: critical
                CA:TRUE, pathlen:0
            X509v3 Key Usage: critical
                Certificate Sign, CRL Sign
            X509v3 Subject Key Identifier: 
                D8:B0:59:A1:94:05:12:2B:6E:A1:17:57:28:D3:11:01:5B:AF:81:0D
            X509v3 Certificate Policies: 
                Policy: X509v3 Any Policy
                  CPS: http://pki.registradores.org/normativa/index.htm
                  User Notice:
                    Explicit Text: Certificado sujeto a la Declaraci�n de Pr�cticas de Certificaci�n del Colegio de Registradores de la Propiedad y Mercantiles de Espa�a (� 2016)

            Authority Information Access: 
                CA Issuers - URI:http://pki.registradores.org/certificados/ac_raiz_psc_corpme.crt

            X509v3 Authority Key Identifier: 
                keyid:DA:72:38:61:40:06:97:E5:02:F1:6D:69:DB:04:01:E9:E7:0C:A3:E7

            X509v3 CRL Distribution Points: 

                Full Name:
                  URI:http://pki.registradores.org/crls/arl_psc_corpme.crl
                  URI:ldap://ldap.registradores.org/CN=AC%20RAIZ,O=Colegio%20de%20Registradores%20-%20Q2863012G,C=ES?authorityRevocationList?base?objectclass=cRLDistributionPoint

    Signature Algorithm: sha512WithRSAEncryption
         4d:13:0b:be:d3:86:d9:a6:85:97:fd:ce:1e:9d:42:5f:c1:dc:
         88:d9:f2:e3:11:54:43:8a:7e:fb:bc:b3:7a:8b:e1:a6:f3:e2:
         89:24:d3:f4:38:41:e0:1a:f1:a6:8c:9a:0d:b3:30:e9:ab:b5:
         bb:32:70:6f:81:3d:e3:a0:ef:db:27:8e:a4:c2:82:2a:4e:48:
         6f:8a:0a:b3:33:1f:12:72:36:bf:b2:4e:d9:46:16:f4:c8:16:
         8c:a6:52:61:af:06:f3:07:11:98:7f:74:be:7a:e5:54:1a:a9:
         b2:0c:ba:4f:52:dd:4c:bc:8a:00:f6:3e:fc:b7:a9:87:80:f2:
         40:64:4b:85:ca:54:4c:46:22:e1:3e:de:eb:85:12:65:6c:de:
         34:a9:8e:66:c1:83:76:6f:82:98:45:2a:87:14:87:48:a6:9d:
         bb:08:df:38:fc:41:5a:7b:6f:16:3e:b5:27:8e:f0:28:42:21:
         52:28:b7:53:ed:aa:07:97:21:e1:04:e8:b4:14:b9:40:1a:04:
         9a:7d:a7:09:da:9c:d6:61:7a:c6:0d:13:80:b2:73:e6:84:69:
         6b:38:12:31:8c:a9:47:3f:55:ad:4d:c0:9e:cb:f3:b6:74:1b:
         c4:ed:67:6a:67:49:42:4e:ab:cb:3d:42:53:93:92:5f:af:ae:
         b5:17:6d:85:47:c2:d7:1b:1b:b4:9c:c4:95:98:2a:9c:20:ff:
         8d:92:ab:f6:b1:3e:1e:b4:6a:8c:26:e2:f0:96:5d:18:da:01:
         39:b6:ba:66:2d:ee:6b:ed:6c:54:c9:5f:70:08:f2:98:13:ac:
         c4:66:cd:5c:fa:92:aa:a8:15:64:76:18:83:c2:6d:6c:90:57:
         48:87:dc:15:b1:02:ac:fe:aa:69:e5:f1:98:39:c3:86:76:b9:
         7e:ed:9c:16:cc:2e:dc:2d:2c:20:a9:88:e0:9d:59:64:24:f4:
         48:de:c6:e0:71:94:61:84:dd:c0:ec:e3:c6:db:e6:ea:d7:4f:
         d5:97:74:dd:5b:27:07:1b:07:02:f7:c5:7d:68:b2:13:48:a7:
         87:9d:f1:e6:11:fe:d5:a7:96:5d:82:86:73:7a:78:78:34:92:
         31:f2:42:be:be:b8:cd:8f:c2:75:ce:b4:9a:be:2e:08:24:27:
         90:77:d1:c5:4f:31:52:59:80:e4:24:43:77:62:47:3d:86:bd:
         c5:47:de:9b:79:55:e7:ba:5f:df:7c:dd:62:0f:a8:d9:b9:92:
         ca:57:9b:0c:ef:ad:a1:2d:fb:76:1a:05:7f:6b:15:5b:bb:62:
         f8:43:af:68:a7:bf:f1:49:89:1e:26:56:7c:3d:a3:c2:a6:ba:
         f6:48:82:2a:f5:89:7a:53

 Signature Algorithm: sha512WithRSAEncryption
 Public Key Algorithm: rsaEncryption
 Public-Key: (4096 bit)
 ```
 
 Since the certificate is valid until 2028 so the algorithms and key sizes used in the certificate are appropriate.
