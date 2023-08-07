# azure-website
Module 14 My Azure Website

![image](https://github.com/ReVampHer/azure-website/assets/98286483/e7e86b0c-9f6b-4063-ae99-551981d1e9a3)

I created a website with the Azure free domain
Here is the DNS lookup performed in GitBash

![image](https://github.com/ReVampHer/azure-website/assets/98286483/989c973d-f8a2-4db2-9332-9454d1073ffb)

I used the runtime stack of PHP 8.0

the directory /var/ww/html has a directory called assets. The assets directory contain the Cascading Style Sheets (CSS). and the image files containing the background images, LinkedIn-logo image, etc. These files work on the front-end of the website.

A cloud tenant is an organization, or application developer that has a Microsoft cloud service like Azure.

An access policy is important on a key vault to assign who can access/perform different operations on the key vault. This decides if a user, application, or group can access it. If not, they would have access to cryptographic keys, certificates, connections strings, passwords within the cloud. With the cloud you always take extra measures to protect your data/information.

A brief description of the differences between keys, secrets, and certificates within the key vault:
Keys: cryptographic keys (software-protected, Hardware Security Module-protected), associated with certificates
Secrets: database connection strings, passwords
Certificates: built on top of keys and secrets and offers an automated renewal. 

Cryptography:
Advantage of a self-signed certificate:
Free, easy to modify for development/testing or your internal network websites.
Disadvantages of a self-signed certificate:
No trust value and they can be revoked, hence testing or internal use only. 
Wildcard Certificate:
Wildcard character in the domain name field “*” to secure several sub domain names that is on the same domain. It will tend to all the domains with a single certificate. These are not recommended because it could become a single point of failure.

When binding a certificate to my website, Azure only provides TLS versions 1.0, 1.1, and 1.2. But it doesn't include SSL 3.0. The reason SSL 3.0 is not provided is because Microsoft (MS) shut it down to protect from the vulnerabilities and subject to Man-in-the-middle attacks (Padding Oracle on Downgraded Legacy Encryption).

My website has a valid certificate range: Not Before 3/9/23 10:05:55 PM EST, and Not After 3/3/24 10:05:55 PM EST
It also has an intermediate certificate of Microsoft Azure TLS Issuing CA 02, and a root certificate of DigiCert Global Root G2. The root certificate is in a root store of Google.com has GTS Root R1.

Cloud Security:
The similarities and differences between Azure Web Application Gateway and Azure Front Door are:
Similarities:
Both support session affinity (sticky sessions) which is a feature that you can route all request from the client to a replica and enforced with HTTP cookies. Both work on Layer 7 (Application Layer) on Protocols of HTTP, HTTPS.

Differences:
Front Door is a nonregional global service. Applied WAF (filter) at edge location, far out form the reach of the data center. It performs global routing of your traffic, and end-user performance. The health probe is synthetic HTTP/HTTPS request in form of GET, HEAD. No SKU available, work level does not support VM level, and no traffic control. 

Web Application Gateway is a regional service. It applies the WAF (filter) when the packets enter your network. The health probe is not synthetic, and the request is not the form of GET, HEAD. The SKU is in Standard and Basic. Work level in any IP address, the protocols also include Websocket, and the traffic control has a Network security Group (NSG).

SSL offloading and it's benefits:
Its “offload” SSL traffic to a separate server that performs encrypting and decrypting of the traffic.
This will increase the performance of your web server significantly. 

Web Application Firewall (WAF) works on Layer 7 of the OSI Model. I included an image of my WAF custom rule below.

![image](https://github.com/ReVampHer/azure-website/assets/98286483/503d92b6-eb36-4305-87b6-8b662f773492)


I selected the SQL injection rule to define because it is of interest to me. 
SQL injection: It matches keywords like Select, Union, special characters such as ();:, operators like =,><, !=, and comment symbols such as the = or /**/.
My website would be impacted by this vulnerability if Front Door wasn't enabled. Because by default, it protects against the OWASP top 10 security risks. And you can enable bot protection.
Here is my Front Door enabled below:

![image](https://github.com/ReVampHer/azure-website/assets/98286483/755f6aa4-6510-456e-8021-0dd79cd8da8e)

![image](https://github.com/ReVampHer/azure-website/assets/98286483/eb2a6f9c-b692-4051-83f1-bcfe2dae89fe)

Resources below:

msmbaldwin. “Azure Key Vault Security Overview.” Learn.microsoft.com, learn.microsoft.com/en-us/azure/key-vault/general/security-features.

sethmanheim. “Azure App Service on Azure Stack Overview - Azure Stack Hub.” Learn.microsoft.com, 29 July 2022, learn.microsoft.com/en-us/azure-stack/operator/azure-stack-app-service-overview?view=azs-2301. Accessed 27 June 2023.

“What Is a Wildcard Certificate?” Knowledge.digicert.com, digicert, 19 Oct. 2022, knowledge.digicert.com/generalinformation/INFO900.html.

msmbaldwin. “Azure Key Vault Keys, Secrets, and Certificates Overview.” Learn.microsoft.com, 21 Apr. 2023, learn.microsoft.com/en-us/azure/key-vault/general/about-keys-secrets-certificates.

Administrator, SSL Dragon. “Root vs Intermediate Certificates.” SSL Dragon, 9 Jan. 2023, www.ssldragon.com/blog/root-intermediate-certificate/#:~:text=You%20can%20tell%20a%20root. Accessed 27 June 2023.

“What Is SSL Offloading? Definition and Related FAQs.” Avi Networks, avinetworks.com/glossary/ssl-offload/#:~:text=SSL%20offloading%20relieves%20a%20web.

