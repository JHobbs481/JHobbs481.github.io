---
layout: single
title: "Microsoft Azure: built, secured, and protected a cloud application"
excerpt_separator: "<!--more-->"
author_profile: true
classes: wide
header:
  overlay_image: 
categories:
  - CyberSecurity Bootcamp
tags:
  - Azure
  - Web app
---
During my studies at the [University of Richmond Cybersecurity Bootcamp](https://bootcamps.richmond.edu/cybersecurity/) I used Microsft Azure to build and host my own web application, secure it with an SSL certificate, and add security features to protect it.

This project was split into three days. On the first day, I started by creating a web app on the [**Azure Portal**](https://learn.microsoft.com/en-us/azure/azure-portal/azure-portal-overview).
Which involved setting a **runtime stack**, **operating system**, and **region**.
Additionally I established an App Service Plan for **2 vCPU**, **1.75 Memory (GB)**, **10 Remote Storage (GB)**.
Once I created the web app, I deployed a [Cyber Blog Framework \- Docker Container](https://hub.docker.com/r/cyberxsecurity/project1-apachewebserver) through Azure Cloud Shell then customized the blog template by **SSHing** into the container and editing the `index.html` file.

On the second day, I started by creating a key vault on the **Azure Portal** and changed from Azure role-based access control to vault access policy.
Then I generated a **Self-Signed** **Certificate** using OpenSSL through the Cloud Shell.
This generated a key and a certification however Azure requires the **PFX format**, the server certificate and private key combined into a single encrypted format, I once again used OpenSSL to reformat it.
I then downloaded and imported the key into my website to analyze what users would see with a **Self-Signed Certificate**.
However, Microsoft provides **Secure SSL Certificates** when using Azure’s free domain so I deleted the Self-Signed certificate I generated.

The third day focused on protecting my web application with Azure’s Security Features.
I started by creating a **Web Application Firewall (WAF)** and analyzed some of the managed rule sets.
I then configured a custom **WAF** rule to block international IPs to protect against potential security attacks.
After all that, I then accessed **Azure Security Center** to analyze and fix the recommendations given to improve the protection of my web app.

Below is the project technical brief which includes questions and pictures I answered throughout the course of this project to submit for a grade. To see the full document click [**Here**](https://docs.google.com/document/d/12EqJ0kQ3rjvRnShevXIOO4h1QBPcprnaVqzn6YaxHFE/edit?usp=sharing).

<center> <h1>Technical Brief</h1> </center>

<center> <h2>My Web Application</h2> </center>

Url for the Web application:
- jakessecurityresume.azurewebsites.net (It has been deactivated)

Pictures below:

<figure class ="align-center">
  <img src="/images/azureblogpic1.png">
</figure>
<figure class ="align-center">
  <img src="/images/azureblogpic2.png">
</figure>

<center> <h2>Day 1 Questions</h2> </center>

### Networking Questions

1. What is the IP address of your webpage
    - 20.211.64.27
2. What is the location (city, state, country) of your IP address?
    - Sydney, New South Wales, AU

### Web Development Questions

1. When creating your web app, you selected a runtime stack.  What was it? Does it work on the front end or the back end?
    - it was PHP 8.2 runtime stack which primarily works on the back-end of a web app.
2. Inside the /var/www/html directory, there was another directory called assets. Explain what was inside that directory.
    - it had all the images and a custom .css file for the template we downloaded
3. Consider your response to the above question. Does this work with the front end or back end?
    - This would be a front end component because the front end is responsible for rendering the visual components that users interact with.


<center> <h2>Day 2 Questions</h2> </center>

### Cloud Questions

1. What is a cloud tenant?
    - A cloud tenant is an individual or organization that essentially rents or leases virtual infrastructures from a cloud provider like azure.
1. Why would an access policy be important on a key vault?
    - An access policy is important because it controls who can manage and access a key vault’s secrets, keys, and certifications. Without it an unauthorized party could access it.
1. Within the key vault, what are the differences between keys, secrets, and certificates?
    - In a key vault, keys are used for encryption and decryption. While secrets are sensitive information such as passwords and certificates are used for secure communication and identity validation. 

### Cryptography Questions

1. What are the advantages of a self-signed certificate?
    - A self-signed certificate is free and quick to deploy, they do not expire or last a lot longer, and there is no limitation to how many you can generate.
1. What are the disadvantages of a self-signed certificate?
    - A huge disadvantage of a self-signed certificate is it’s not secure. As well as, not being issued by a trusted CA which would usually display warning messages to a user.
1. What is a wildcard certificate?
    - A wildcard certificate is used to secure multiple domains. This can be helpful if you have a lot of domains or subdomains.
1. When binding a certificate to your website, Azure only provides TLS versions 1.0, 1.1, and 1.2.  Explain why SSL 3.0 isn’t provided.
    - SSl 3.0 is considered insecure and vulnerable to attacks like POODLE. A POODLE attack works by using a MITM vulnerability to eavesdrop on “secure” communications.
1. After completing the Day 2 activities, view your SSL certificate and answer the following questions:
    1. Is your browser returning an error for your SSL certificate? Why or why not?
        - It is not because Azure has Microsoft deploy trusted certificates for you.
    2. What is the validity of your certificate (date range)?
        - It was issued on March 12th 2024 and expires on march 7th 2025 so basically a year.
    3. Do you have an intermediate certificate? If so, what is it?
        - Microsoft Azure RSA TLS Issuing CA 07
    4. Do you have a root certificate? If so, what is it?
        - DigiCert Global Root G2
    5. Does your browser have the root certificate in its root store?
        - it is in chrome’s root store
    6. List one other root CA in your browser’s root store.
        - DigiCert Assured ID Root G2
   

<center> <h2>Day 3 Questions</h2> </center>

### Cloud Security Questions

1. What are the similarities and differences between Azure Web Application Gateway and Azure Front Door?
    - The similarities between the two is they both work in the front end and operate at the application layer OSI Model. As well as, incorporating a WAF and primarily acting as a load balancer. The main difference is Azure web application gateway is more suited for protecting a single region while Azure front door is better suited for multiple regions.
1. A feature of the Web Application Gateway and Front Door is “SSL Offloading.” What is SSL offloading? What are its benefits?
    - SSL offloading, also known as SSL termination, is a process where encryption and decryption happens before reaching the web server. Usually it is handled by a dedicated device or service that will decrypt incoming traffic before forwarding it to the web server and re-encrypted before being sent to the client.
1. What OSI layer does a WAF work on?
    - Application layer (7)
1. Select one of the WAF managed rules (e.g., directory traversal, SQL injection, etc.), and define it.
    - The SQL injection WAF rule monitors patterns or signatures that would indicate a potential SQL injection attempt and blocks or sanitizes the input before it reaches the web app.
1. Consider the rule that you selected. Could your website (as it is currently designed) be impacted by this vulnerability if Front Door wasn’t enabled? Why or why not?
    - Yes because without the WAF SQL injection rule you would be vulnerable to those types of attacks.
1. Hypothetically, say that you create a custom WAF rule to block all traffic from Canada. Does that mean that anyone who resides in Canada would not be able to access your website? Why or why not?
    - unless they used a VPN to change their location they would not be able to access the website in canada.
1. Include screenshots below to demonstrate that your web app has the following:
    - A WAF custom rule
    <figure class ="align-center">
  <img src="/images/azurewafrule.png">

