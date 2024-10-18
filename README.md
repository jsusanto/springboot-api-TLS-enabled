# springboot-api-TLS-enabled

# Starting with Spring Initializr
1. Navigate to https://start.spring.io. This service pulls in all the dependencies you need for an application and does most of the setup for you.

2. Choose either Gradle or Maven and the language you want to use. This guide assumes that you chose Java.

3. Click Dependencies and select Spring Web.

4. Click Generate.

5. Download the resulting ZIP file, which is an archive of a web application that is configured with your choices.

![image](https://github.com/user-attachments/assets/32ebd709-5d0c-4ccb-870e-ea5433abf6b7)

# IDE - Intellij IDEA 2024.2.2 (Community Edition)
![image](https://github.com/user-attachments/assets/6e747fda-cb38-46af-955e-1a740d719960)

# Run your project (boot run)

![image](https://github.com/user-attachments/assets/6f530a58-6998-42fb-ae44-4993019c54cb)

# Enable TLS in Spring Boot
<h3>1. TLS Protocol</h3>
TLS provides protection for data in transit between client and server and is a key component of the HTTPS protocol. 
The Secure Sockets Layer (SSL) and TLS are often used interchangeably, but they aren’t the same. 
In fact, TLS is the successor of SSL. TLS can be implemented either one-way or two-way.

<h3>1.1 One-Way TLS</h3>
In one-way TLS, only the client verifies the server to ensure that it receives data from the trusted server. For implementing one-way TLS, the server shares its public certificate with the clients.

<h3>1.2 Two-Way TLS</h3>
In two-way TLS or Mutual TLS (mTLS), both the client and server authenticate each other to ensure that both parties involved in the communication are trusted. For implementing mTLS, both parties share their public certificates with each other.

<h3>2. Configuring TLS in Spring Boot</h3>
<h3>2.1 Generating a Key Pair</h3>
The keystore file can be in different formats. The two most popular formats are Java KeyStore (JKS) and PKCS#12. <br/>

JKS is specific to Java, while PKCS#12 is an industry-standard format belonging to the family of standards defined under Public Key Cryptography Standards (PKCS).
<pre>
keytool -genkeypair -alias baeldung -keyalg RSA -keysize 4096 \
  -validity 3650 -dname "CN=localhost" -keypass changeit -keystore keystore.p12 \
  -storeType PKCS12 -storepass changeit
</pre>

<h3>2.2 Configuring TLS in Spring</h3>
Let’s start by configuring one-way TLS. We configure the TLS related properties in the application.properties file:
<pre>
# enable/disable https
server.ssl.enabled=true
# keystore format
server.ssl.key-store-type=PKCS12
# keystore location
server.ssl.key-store=classpath:keystore/keystore.p12
# keystore password
server.ssl.key-store-password=changeit
</pre>
<br/>
When configuring the SSL protocol, we’ll use TLS and tell the server to use TLS 1.2:
<pre>
#trust store location
server.ssl.trust-store=classpath:keystore/truststore.p12
#trust store password
server.ssl.trust-store-password=changeit
</pre>

# References
- https://spring.io/guides/gs/rest-service
- https://www.baeldung.com/spring-tls-setup
