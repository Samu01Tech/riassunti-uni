# Access Control

Access control is the process of granting or denying access to resources. It is a fundamental security mechanism.

Main parts of an access control system are:

- Subjects (any entity including users, processes, devices, etc.)
- Guard (Policy Decision Point)
- Access Control Module

## Access Control Models

### Access Control Matrix

|     | f1  | f2  | f3  |
| --- | --- | --- | --- |
| u1  | r   | r/w | r/w |
| u2  | r   | r/w | r   |
| u3  | r/w | r/w | r   |

**An access control matrix is a table or matrix that defines the permissions, or access rights, that different users or groups have to various resources or objects in a computer system**. The matrix typically includes rows representing the users or groups, columns representing the resources or objects, and cells containing the permissions associated with each user or group for each resource or object.

### Access Control List (AC List)

- An ACL is a list of permissions associated with a specific resource or object.
- The ACL defines which users or groups have what permissions for the resource or object.
- ACLs are often used in file systems, database systems, and operating systems to control access to resources such as files, folders, and database records.
- One advantage of ACLs is that they are easy to understand and implement. However, they can become complex and hard to manage when there are many users or resources, and when permissions need to be granted or revoked frequently.

### Capabilities

- A capability is a token or object that represents a specific permission to access a specific resource or object.
- Capabilities are typically implemented as references or pointers to the resource or object, rather than as a list of permissions.
- Capabilities are often used in operating systems to control access to resources such as memory, I/O devices, and system services.
- One advantage of capabilities is that they can be passed between processes, allowing a process to grant access to a resource to another process without needing to modify an ACL. This makes capabilities more flexible and easier to manage than ACLs in some situations. However, they can be more difficult to understand and implement than ACLs.

### Multi-Level Security (Bell-LaPadula)

The Bell-LaPadula (BLP) access control model is a formal model for specifying and enforcing access control policies in computer systems. It was developed in the 1970s by David Bell and Leonard LaPadula of the U.S. Department of Defense, and is based on **the principle of "no read up, no write down"**, which means that a subject (e.g., a user or process) cannot read a resource at a higher classification level unless it has been granted access to resources at that level, and cannot write to a resource at a lower classification level unless it has been granted access to resources at that level.

The BLP model has three main components:

1. **Classification levels**: The model defines a set of classification levels, such as "secret," "confidential," and "unclassified," which are used to label resources according to their sensitivity or importance. Each subject is also assigned a classification level.

2. **Categories**: Which identifiy the group a resource belong. 

3. **Simple security property (SSP)**: The SSP is the "no read up, no write down" principle described above. It ensures that a subject can only read or write resources at its own classification level or lower, and cannot read or write resources at a higher classification level.

The BLP model is often used in military and government systems to protect sensitive information and prevent unauthorized access or disclosure. It is a widely recognized and respected model, but can be complex to implement and may not be suitable for all environments.

### Role-Based Access Control (RBAC)

Role-Based Access Control (RBAC) is a method of access control in which **users are assigned to roles**, and the **roles are granted permissions to access specific resources or perform specific actions**. RBAC is based on the idea that users should only be granted access to the resources and actions that are necessary for them to perform their job duties.

In an RBAC system, users are typically grouped into roles that correspond to their job functions or responsibilities. 

> For example, a role might be created for "system administrators," "customer service representatives," or "accountants." Each role is then granted specific permissions to access certain resources or perform certain actions. For example, a "system administrator" role might be granted permission to access and modify system configuration files, while a "customer service representative" role might be granted permission to access and modify customer records.

RBAC systems typically include a central policy server or database that defines the roles and permissions, as well as an access control module that enforces the permissions. Users are typically added to or removed from roles as needed, and the permissions associated with a role can be modified as needed.

RBAC is a flexible and widely used method of access control, and is particularly well-suited for environments with a large number of users and resources, or where access control policies may need to be modified frequently. It is used in a variety of contexts, including operating systems, network devices, and web applications.

### Attribute-Based Access Control (ABAC)

Attribute-Based Access Control (ABAC) is a method of access control in which **access to resources is based on the attributes of the user, the resource, and the context in which the access is being requested**. ABAC allows for **fine-grained control** over access to resources, as it takes into account multiple attributes rather than just the identity of the user or the role that the user belongs to.

In an ABAC system, access to resources is governed by a set of policies that specify the conditions under which access is granted. These policies may include attributes such as the user's identity, the user's role or job function, the time of day, the location of the user, and the type of device being used. The policies may also include attributes of the resource itself, such as the classification level or sensitivity of the resource, or the type of resource (e.g., file, database record, etc.).

ABAC systems typically include a policy server or database that stores the policies and an access control module that enforces the policies. When a user requests access to a resource, the access control module retrieves the relevant policies and evaluates them against the attributes of the user, the resource, and the context of the request. If the policies are satisfied, the access control module grants access to the resource.

ABAC is a highly flexible and powerful method of access control, as it allows for the creation of complex and fine-grained access control policies. It is used in a variety of contexts, including operating systems, network devices, and web applications.

---

## XACML

eXtensible Access Control Markup Language (XACML) is a standardized, general-purpose access control policy language that can be used to **specify and enforce access control policies in computer systems**. XACML is based on the concept of attribute-based access control (ABAC), in which access to resources is based on the attributes of the user, the resource, and the context in which the access is being requested.

### XACML policy language

It is for specifying access control policies and algorithms for combining them.

![XACML](./images/ComputerAndNetworkSecurity/XACMLStructure.png)

Each policy has a **Target**, which is a Boolean condition that tells the system if the rule needs to be meet.

There are four types of **combining rules** in XACML:

1. **Deny-overrides**: If any policy or policy set evaluates to "Deny," the request is denied. If all policies and policy sets evaluate to "Permit," the request is permitted. If there are any "Not applicable" or "Indeterminate" evaluations, the request is treated as "Indeterminate."

2. **Permit-overrides**: If any policy or policy set evaluates to "Permit," the request is permitted. If all policies and policy sets evaluate to "Deny," the request is denied. If there are any "Not applicable" or "Indeterminate" evaluations, the request is treated as "Indeterminate."

3. **First-applicable**: The first policy or policy set that applies to the request is used to determine the result. If no policies or policy sets apply, the request is treated as "Not applicable."

4. **Only-one-applicable**: If more than one policy or policy set applies to the request, the request is treated as "Indeterminate." If only one policy or policy set applies, the result of that policy or policy set is used to determine the result of the request. If no policies or policy sets apply, the request is treated as "Not applicable."

An **obligation** is a specific action or requirement that must be carried out or satisfied in order to grant access to a resource. Obligations are often used to enforce additional security measures or to provide additional information or context when granting access to a resource.

### XACML Architecture

![](/home/samu/Documents/Markdown/images/ComputerAndNetworkSecurity/XACMLarchitecture.png)

**Policy Enforcement Point**: It is the front entity wich protect the resource. It performs Access Control by making decision request and enforcing authorization decisions.

**Context Handler**: It is the entity that parse the format of the request in the XACML standard. The **Context** is the canonical representation of a decision request and an authorization decision.

**Policy Decision Point**: This entity as two roles. First it handles the request and retrieves the applicable policy. Than it evaluates the policy and return the auth decision to PEP.

**Policy Administration Point**: It creates and store the policies.

**Policy Information Point**: It collect the data required for policy evaluation (from the attributes)

## OAuth 2.0

OAuth 2.0 (Open Authorization) is a widely used open standard for authorization that **allows users to grant third-party applications access to their resources without sharing their credentials** (such as a username and password). OAuth 2.0 is used by many internet services, including Google, Facebook, and Microsoft, to allow users to authorize third-party applications to access their accounts and data.

OAuth 2.0 is a framework that defines a set of protocols and processes for authorization. It allows users to authorize third-party applications to access their resources without sharing their credentials, and enables applications to obtain **limited access to user resources on an "as needed" basis.** OAuth 2.0 is designed to be flexible and extensible, and can be used in a variety of contexts and scenarios.

> analogy: valet key for cars
> 
> You basically give a custom "token" to an external service which has to access some but not all of your personal resources.
> 
> ie. online printing service

### Flow

1. Authentication

2. User Consent

3. Get OAuth Token (_Bearer_, which contains access rights)

4. Access Resource

### Entities

- Resource Owner (Bearer, which contains access rights)
  
  Access Resource

- Protected Resource

- Client (App or Service)

- Authorization Server

### JSON Web Token (JWT)

It is the standard for OAuth2.0 Access Token. It is made by a **header**, a **payload** and a **signature**. Everything is encoded in base64.

### OAuth 2.0 for Authentication (Bad)?

The assumption that possession of a valid access token is enough to prove that a user

is authenticated is true only in some cases (when the access token was freshly minted)

There are other ways to obtain a valid access tokens than authenticating resource owner.

> ie. using the refresh token

Authentication is about the user and their presence with the application
