# ActiveDirectoryBasics

Use the table of content in the header for skipping to your desired topic -
![table of content](https://github.com/darkoid/ActiveDirectoryBasics/assets/81341961/2d473c0b-c727-4c00-82ad-fd78279eacae)

## Description

This project will contain the fundamentals of active directory that will set the baseline for all my active directory projects. I will be explaining the **physical components** like domain service, domain controller and AD DS data store as well as **logical components** like trees, forest, trusts & object, etc. After that I will talk about types of **authentication** for an AD server.

## Definition of Active Directory (AD):

- Directory service developed by Microsoft to manage windows domain networks.
- It's like a ***phonebook*** containing information related to objects, like Computers, users, printers, etc.

## Why Active Directory(AD) is used?

- Active Directory is most commonly used identity management service in the world. (95% of Fortune 1000 companies)
- It allows for the control and monitoring of their user's computers through a single domain controller.

## What is Active Directory for?
You could see Active Directory as a service / database which stores records data on users, devices, applications, groups, give permissions and manage all this information in a hierarchical structure, its primary function is to AuthN and AuthZ users and computers.
![image](https://github.com/darkoid/ActiveDirectoryBasics/assets/81341961/f64ba1b9-fc76-4679-a3b2-37c34130ebc5)

## Active Directory Abbreviation
- AD: Active Directory
- AD DS: Active Directory Domain Services
- DC: Domain Controller
- DNS: Domain Name System
- LDAP: Lightweight Directory Access Protocol
- OU: Operational Units
- OS: Operating System

## Physical AD Component
This is the servers and machines on-premise, these can be anything from domain controllers and storage servers to domain user machines; everything needed for an Active Directory environment besides the software.
![image](https://github.com/darkoid/ActiveDirectoryBasics/assets/81341961/b270b31e-1580-4f6f-b469-b21883651ff9)

### Domain Controller(DC)
A domain controller is a Windows server that has Active Directory Domain Services (AD DS) installed and has been promoted to a domain controller. **AD DS** is the core of any Windows Domain. This service acts as a catalogue that holds the information of all of the objects that exist on your network.

Domain controllers are the center of Active Directory - they control the rest of the domain. They are responsible for -

- Hosting the AD DS Data Store (will talk later)
- Providing authentication and authorisation services
- Replicating updates from other domain controllers in the forest
- Allowing administrative access to manage domain resources such as user accounts and network services.

#### AD DS Data Store
Active Directory Data Store stores the databases files and processes that store and manage directory information such as users, groups, and services. The AD DS Data Store -

- Contains the NTDS.dit file - a database that contains all of the information of an AD DC as well as password hashes for domain users
- Stored by default in %SystemRoot%\NTDS
- accessible only by the domain controller

## Logical AD Component
Logical AD Componets consists of Schema, Forests, Trees, Domains, Organizational Units, Trusts and Objects. These components can be described by the following AD Structure -
![image](https://github.com/darkoid/ActiveDirectoryBasics/assets/81341961/fa2eeeb1-5607-48c7-a733-8c18ed9227f5)

### Schema
A blueprint that defines of how objects can be created, stored and configured in AD, every object is an instance of a class and every class has their own attributes. We can define object types as follows -

| Object Types     | Function                                      | Examples       |
| ---------------- | ----------------------------------------------| -------------- |
| Class Object     | What objects can be created in the directory  | User<br>Computer |
| Attribute Object | Information that can be attached to an object | Display name   |

### Domains
The fundamental unit of AD.

### Trees
A Tree or a Domain Tree is a set of domains in AD DS. All domains of a tree -

- share a common namespace with the parent domain
- can have additional child domains
- by default create a two-way trust with other domains

### Forests
A forest is a collection of one or more trees. All domains in a forest -

- share a common schema, a common configuration partition, common global catalog to enable searching
- enable **trusts** between each other
- share the Enterprise Admin and Schema Admin groups

### Organizational Units (OUs)
OUs are AD containers that contain users, groups, computers, and other OUs. They are used to -

- represent your organisation hieararchically and logically
- manage a colection of objects in a cosistent way
- delegate permissions to administer groups of onjects
- apply policies

### Trusts
Trust provides a mechanism for users to gain access to resources in another domain. All domains in a forest trust all other domains in the forest. Trust can extent outside the forest.
| Types of Trusts | Description                    | Diagram        |
| --------------- | ------------------------------ | -------------- |
| Directional     | The trust direction flows from trusting domain to the trusted damain | ![image](https://github.com/darkoid/ActiveDirectoryBasics/assets/81341961/2ca6435b-629d-47c3-a534-b49ec558a0af) |
| Transitive      | The trust relationship is extended beyond a two-domain trust to include other trusted domains | ![image](https://github.com/darkoid/ActiveDirectoryBasics/assets/81341961/71628bb2-fc5f-4b96-9f23-378a9347061e) |

### Objects
| Object | Description |
| ----------| -----------|
|User|Enables network resource access for a user|
|InetOrgPerson|Similar to a user account<br>Used for compatibility with other directory services|
|Contacts|Used primarily to assign e-mail addresses to external users<br>Does not enable network access|
|Groups|Used to simplify the administration of access control|
|Computers|Enables authentication and auditing of computer access to resources|
|Printers|Used to simplify the process of locating and connecting to printers|
|Shared folders|Enables users to search for shared folders based on properties|

## AD Authentication
This topic is most important for Network Pentesting. I read above topics just to make more sense when I read the following. Lets begin!

**For Windows System**, There are two authentication protocols/methods provided by microsoft - **Kerberos** and **NTLM**. By default kerberos is the authentication protocol for Active Directory as it is more secure hence recommended.

**For Linux System**, There are other protocols available which are not build by microsoft. The two prominent ones are **LDAP** and **Samba**. These were created to make AD works seamlessly with linux-based systems and services.

**For Mac System**, There are no seperate protocol available but **LDAP** and **AD connector** can be used together to configure Macs to access basic account details in AD DS. This isn't a good method of authenticating macs through AD as compared to Linux or Windows yet.

### NTLM Authentication
As I said Kerberos is more secure (and we'll understand why we learn more about both methods) so why is NTLM still supported.
#### Why use NTLM instead of kerberos?
- Its a Legecy Method. Many old systems might not support Kerberos. So NTLM allows these legacy systems to continue functioning without disruption.
- NTLM is supported across different OS.

History of NTLM: **LAN Manager (LM)** : Oldest and weakest authentication protocol created for AD. Then **NTLM version 1** which is more secure than LM. And current version is NTLM version 2. MS keeps on improving NTLM as vulnerabilities are discovered or better algorithm is found.

#### Working of NTLM Authentication
Why is NTLM a weaker authentication method? It is because of how it works. NTLM relies on a three-way handshake between the client and server to authenticate a user.

The following steps present an outline of NTLM non-interactive authentication. The first step provides the user's NTLM credentials and occurs only as part of the interactive authentication (logon) process.

![image](https://github.com/darkoid/ActiveDirectoryBasics/assets/81341961/5c1bbea9-6f33-4f73-b230-fe352b10e3cf)

- i. A user accesses a client computer and provides a domain name, user name, and a password.The client computes a cryptographic hash of the password and discards the actual password. The client sends the user name to the server (in plaintext).
- ii. The server generates a 16-byte random number, called a challenge or Nonce and sends it back to the client.
- iii. The client encrypts this challenge with the hash of the user's password and returns the result to the server. This is called the response.
- iv. The server sends the following three items to the domain controller:- User Name- Challenge sent to the client- Response received from the client.
- v. The domain controller uses the user name to retrieve the hash of the user's password. It compares the encrypted challenge with the response by the client (in step 4). If they are identical, authentication is successful, and the domain controller notifies the server.
- vi. The server then sends the appropriated response back to the client.

### Kerberos Authentication
Kerberos is default for AD. It is intended to be more "secure" than NTLM by using third party ticket authorization and stronger encryption. Even though NTLM has a lot more attack vectors, Kerberos still has a handful of underlying vulnerabilities just like NTLM that can be exploited.

#### Working of Kerberos Authentication
Kerberos uses a two-part process that leverages a ticket granting service or key distribution center. Didn't understand well let me explain by a diagram. But before reading the diagram read these terms to make more sense -
- **Ticket Granting Ticket (TGT)** - A ticket-granting ticket is an authentication ticket used to request service tickets from the TGS for specific resources from the domain.
-  **Key Distribution Center (KDC)** - The Key Distribution Center is a service for issuing TGTs and service tickets that consist of the Authentication Service(AS) and the Ticket Granting Service(TGS).
- **Authentication Service (AS)** - The Authentication Service issues TGTs to be used by the TGS in the domain to request access to other machines and service tickets.
- **Ticket Granting Service (TGS)** - The Ticket Granting Service takes the TGT and returns a ticket to a machine on the domain.
- **Service Principal Name (SPN)** - A Service Principal Name is an identifier given to a service instance to associate a service instance with a domain service account. SPNs are used by **Kerberos** authentication to associate a service instance with a service logon account. This allows a client application to request that the service authenticate an account even if the client does not have the account name.
- **Session Key** - Issued by the KDC when a TGT is issued. The user will provide the session key to the KDC along with the TGT when requesting a service ticket.
- **Privilege Attribute Certificate (PAC)** - The PAC holds all of the user's relevant information, it is sent along with the TGT to the KDC to be signed by the Target LT Key and the KDC LT Key in order to validate the user.

![image](https://github.com/darkoid/ActiveDirectoryBasics/assets/81341961/be901080-8ed4-4f61-9249-8d359e8e1763)
</p> <p align="right">Ignore the yellow tag about kerberoasting, I was lazy to remove it.</p>

1. When a user logs on to Active Directory, the user authenticates to the Domain Controller (DC) using the user’s password which of course the DC knows.
2. The DC sends the user a Ticket Granting Ticket (TGT) Kerberos ticket. The TGT is presented to any DC to prove authentication for Kerberos service tickets.
3. The user opens up Skype which causes the user’s workstation to lookup the Service Principal Name (SPN) for the user’s Exchange server.
4. Once the SPN is identified, the computer communicates with a DC again and presents the user’s TGT as well as the SPN for the resource to which the user needs to communicate.
5. The DC replies with the Ticket Granting Service (TGS) Kerberos service ticket.
6. The user’s workstation presents the TGS to the Exchange server for access.
7. Skype connects successfully

### LDAP Authenticaiton
LDAP(Lightweight Directory Access Protocol) is an open-source and cross-platform protocol that provides AD authentication services. There are two options associated with LDAP-based authentication in AD -
- **Simple authentication**. LDAP uses login credentials to create a request to the server. It also supports anonymous and unauthenticated requests to corporate resources.
- **Simple authentication and security layer (SASL)**. The SASL approach uses other authentication services such as Kerberos to connect to the LDAP server. This way it is as secure as kerberos.

We won't talk about Samba as its a very different method of authentication compared to others but you can make a pull requests to help others.

## Azure AD
In recent years, many companies have started using Active Directory in cloud and most notably Azure AD. Because it is cheaper and comes with default settings for creating users & groups which are much more secure than an on-premise physical AD network. As they have been carefully selected by experts at microsoft who know more about AD which they should as they are the ones who build it. However the cloud AD may still have vulnerabilities.

### Overview
Azure acts as the middle man between your physical Active Directory and your users' sign on which builds a more secure transaction between domains, making a lot of AD attacks ineffective.
![image](https://github.com/darkoid/ActiveDirectoryBasics/assets/81341961/05074db3-a506-41f7-8274-76a316576960)

### Cloud Security in comparasion with physical network

I didn't do much research on this but when i do I will definetly post more projects on my github. I may already have check go check on [my github](https://github.com/darkoid). I read an interesting and detailed comparasion between AD and Azure AD [here](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/compare). Here is the short summary -
| Windows Server AD | Azure AD |
| --- | --- |
| LDAP | Rest APIs |
| NTLM | OAuth/SAML |
| Kerberos | OpenID |
| OU Tree | Flat Structure |
| Domains and Forests | Tenants |
| Trusts | Guests |

# More Terminologies
Here is a set of definitions/terminologies that I read while learning the basics active directory. I started learning this for the purpose of Network Pentesting. I would say the following never came to be useful in term of testing but I read them so I'm providing them here for you as well.

## Active Directory Services 
Active Directory includes several other services that fall under the Active Directory Domain Services, these services include: 

### Active Directory Certificate Services (AD CS)
This is a server role that allows you to build a public key infrastructure (PKI) and provide digital certificates for your organization. Certificates can be used to encrypt network traffic, application traffic, and used to authenticate users and computers. When you see https in a browser address that means it is using a certificate to encrypt the communication from the client to the server.

### Active Directory Domain Services (AD DS)
Already Discussed
### Active Directory Federation Services (AD FS)
The federation service allows single sign on to external systems like websites and applications. Office 365 is a common use for federation services. When you sign into office 365 the username and password is redirected through the federation server and the credentials are checked against your on-premise Active Directory. So this allows you to provide authentication to external systems by using your local Active Directory to authenticate the username and password. 

### Active Directory Lightweight Directory Services (AD LDS)
This service provides directory services using the LDAP protocol without the need to deploy domain controllers. This is primarily used to provide directory service functionally to directory enabled applications. This does not replace AD DS.

### Active Directory Rights Management Services (AD RMS)
This service provides methods for protecting information on digital content. It protects documents by defining who can open, modify, print, forward or take other actions on documents. You can also use certificates to encrypt documents for better security. 
