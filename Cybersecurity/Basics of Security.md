# Basics of Security

## The CIA Triad

The CIA Triad stands for:

- **Confidentiality**: The information is only available to authorized users.

- **Integrity**: The information is not modified in an unauthorized way.

- **Availability**: The information is available when needed.

CIA Triad is essential to achieve security through security policies and mechanisms [🔗](#security-policies-and-mechanisms).

### Confidentiality

Confidentiality is the property that information is not made available or disclosed to unauthorized individuals, entities, or processes. Confidentiality is a key property of information security. Confidentiality is also a key property of data privacy.

Unauthorized access to sensitive information could be _intentional_ (intruder breaking into the network) or _unintentional_ (careless people).

Confidentiality is achieved by:

- **Encryption**: The process of encoding information. This prevents unauthorized individuals from reading the information.

- **Access Control**: The process of restricting access to a resource. This prevents unauthorized individuals from accessing the resource.

<mark>ChatGPT</mark>:

Confidentiality in the CIA triad refers to the protection of information from unauthorized access. It is achieved through the use of various security measures such as encryption, access controls, and data masking. Encryption is the process of converting plaintext into ciphertext, which is unreadable without a decryption key. Access controls are used to restrict access to sensitive information based on a person's identity and clearance level. Data masking is the process of obscuring sensitive data so that it is not visible to unauthorized individuals.

### Integrity

Integrity means guarding against improper information modification or destruction, including information _non-repudiation_ (individual falsely denying having performed a particular operation) and _authenticity_ (property can be verified and trusted).

Integrity also means to have the ability to detect even the smallest change in the data.

Data integrity is compromised both through _human errors_ and _malicious attacks_.

Data integrity can be achieved by:

- **Version Control and Audit Trails**: The process of tracking and controlling changes to documents, computer programs, large web sites, and other collections of information.

It is and essential component for organizations whith certain regulations (ie. finanacial sector).

> Violation of data integrity can lead to _loss of trust_ and _loss of business_. [ie. bots on social media]

<mark>ChatGPT</mark>:

Integrity, in the CIA triad, refers to the protection of information from unauthorized modification or destruction. It is achieved through the use of various security measures such as access controls, input validation, and data backup.

Access controls are used to ensure that only authorized individuals can modify or delete sensitive information. Input validation is a process of checking the data entered by users to ensure that it is in the correct format and within acceptable limits. Data backup is the process of creating copies of important data and storing them in a secure location, in order to ensure that it can be recovered in case of loss or damage.

Hashing is also commonly used to ensure the integrity of data, by creating a unique 'hash' or fingerprint of the data, that can be used to validate that the data has not been tampered with by comparing it to the original hash.

Additionally, integrity can be ensured through the use of digital signatures and non-repudiation mechanisms, which are used to guarantee the authenticity of a message or transaction and prevent any party from denying its involvement in it.

### Availability

Availability is the property that ensures information is accessible and usable upon request by an authorized entity. It also require the data to be protected from accidental interruption of access to the data.

Violation in availability is usually caused by an _infrastructure failure_ or a _DDoS attack_.

Availability can be achieved by:

- **Backup Systems and Disaster Recovery**: The process of creating a copy of data and storing it in a different location. This allows the data to be recovered in case of a disaster.

- **Cloud Computing**: The process of storing data on a remote server. This allows the data to be accessed from anywhere.

Low availability can impact _economy_ and _fundamental rights_.

<mark>ChatGPT</mark>:

Availability, in the CIA triad, refers to the protection of information systems and the data they contain from disruption, whether intentional or accidental. It is achieved through various security measures such as redundancy, disaster recovery, and incident response.

Redundancy refers to the duplication of critical components, such as servers and network connections, to ensure that the system remains operational even if one component fails. Disaster recovery plans are used to restore normal operations as quickly as possible after a disaster or interruption. Incident response is the process of identifying and responding to security incidents in a timely and effective manner, in order to minimize the impact on the availability of the system.

Additionally, load balancing is also used to ensure availability by distributing the workload across multiple servers, in order to prevent any one server from becoming overwhelmed and causing a disruption in service.

Availability is also closely related to business continuity, which is the ability of an organization to keep its operations running during and after a disruption. Ensuring the availability of IT systems and infrastructure is critical for maintaining business continuity.

## Security Policies and Mechanisms

**Security Policies** are the rules and guidelines that organizations put in place to ensure the protection of their information systems and data. They are usually written in a document and are enforced by the system administrators.

**Security Mechanisms** are the technical solutions (usually rated) that implements the security policies. They are usually implemented by the system administrators.

**Security Services** are the capabilities that supports one or more of the security requirements (ie. CIA).

In short: services are like all building blocks to build a security mechanism, which is a procedure to implement policies.

> Example: A company X can have a security policy that states that all employees must use a strong password. The security mechanism can be a password policy that requires a minimum of 8 characters, a mix of upper and lower case letters, numbers and special characters. The security service can be the password hashing algorithm. They might also have policies for visitors.

Some examples of security services are:

- **Authentication**: The process of verifying the identity of a user.

- **Authorization**: The process of giving access to a resource based on the user's identity.

- **Access Control**: The process of restricting access to a resource.

Some examples of security mechanisms are:

- **Firewalls**
- **Encryption**

CIA Triad is also essential not only to achieve security but also understand security violations.

> In a ramnsonware attack _Availability_ is violated, because access to file is blocked, but also _Confidentiality_ is violated, because the attacker could exfiltarte and read the files, and _Integrty_, beacuse files are encrypted and could be modified.

One way to mitigate security violations is **Zero Trust** which is a security model that requires all users to be authenticated, authorized and continuously validated to grant access to applications and data. This is a **Risk Management** approach.

## Risk

**Vulnerabilities** are weaknesses in a system that can be exploited by a threat to violate the security policy (ie. hidden backdoors, unknown software bugs, weak passwords).

**Threats** are potential sources of harm to a system (ie. hackers, viruses, natural disasters).

**Attack** is the exploitation of a vulnerability through a malicious activity to gain unauthorized access or attempt to compromise a system CIA.

[Cyber attacks try to reach as many victims as possible]

**Risk** is the probability of a threat exploiting a vulnerability to cause harm to the system.

![Risk matrix image](/home/samu/Documents/Markdown/images/ComputerAndNetworkSecurity/rIskMatrix.jpeg)

**Considerations**:

- The human factor is crucial in mitigation measures: UX should be as frictionless as possible.

- A threat model is based on simplifying assumptions concerning the system/service and the capabilities of the attacker: we usually trust programmers (**trust assumptions**).

- Threat models are usefull for security experts but in reality they are **limited by budget and security skills**.

- Impact of an attack is relative to the stakeholder: a company might be more concerned about the loss of data than a user.

## Security and Human Factors

It is essential to understand that security is not only about technology, but also about people. They should be aware of the basics of security policies and mechanisms.

## More

- Threat modellling is crucial

- Deploying security controls requires to consider several different aspects

- Security and Trust assumptions are essential

- Be careful with security control

- Security violations can be traced back to the CIA triad
