# 🏛️ Active Directory Lab

## 🎯 Objective

This repository documents the construction and administration of an Active Directory environment from scratch. The goal is to demonstrate practical skills in:

- Domain Controller promotion and configuration
- User and group management
- Organizational Unit (OU) design
- Permission delegation and verification
- Security best practices in identity management

## 🛠️ Environment

| Component | Details |
|-----------|---------|
| **Domain** | `practica.local` |
| **Domain Controller** | Windows Server (Evaluation) |
| **Client OS** | Linux Mint (for administration) |
| **Networking** | Isolated virtual network |

## 📚 Completed Modules

| Module | Topic | Status |
|--------|-------|--------|
| 1 | Active Directory Fundamentals | ✅ |
| 2 | AD Protocols (Kerberos, LDAP, SMB) | ✅ |
| 3 | Populating the Domain (Users & Groups) | ✅ |
| 4 | Permissions and Delegation | ✅ |
| 5 | AD Attack Techniques | 🔜 Coming soon |

## 🔧 Key Commands Used

```cmd
:: List all users in the domain
dsquery user -limit 0

:: Create a new user inside a delegated OU
dsadd user "CN=TestUser,OU=Practica_Users,DC=practica,DC=local" -samid testuser -p P@ssw0rd123 -display "Test User" -u "practica\estudiante1" -p "P@ssw0rd123"

:: Run a command as a delegated user
runas /user:practica\estudiante1 "cmd.exe" :: List all users in the domain
dsquery user -limit 0

:: Create a new user inside a delegated OU
dsadd user "CN=TestUser,OU=Practica_Users,DC=practica,DC=local" -samid testuser -p P@ssw0rd123 -display "Test User" -u "practica\estudiante1" -p "P@ssw0rd123"

:: Run a command as a delegated user
runas /user:practica\estudiante1 "cmd.exe"
```

🧠 Lessons Learned

· Delegation is applied to the OU, not to the user. The Practica_Admins group receives permissions over the Practica_Users OU. Users inherit those permissions by being members of the group.
· The runas command requires the correct syntax. Using runas /user:practica\estudiante1 "cmd.exe" works, while runas /user:practica\estudiante1 "dsa.msc" fails because dsa.msc is not a valid Win32 application.
· Error 740 (elevation required) is expected when a delegated user tries to open administrative tools on the Domain Controller. Delegation does not grant local administrator rights on the DC.
· Error 1385 (logon failure) occurs when a delegated user attempts to log on locally to the DC. Windows Server restricts local logon to administrators by default.

🎯 Future Work

· Implement Kerberoasting and AS-REP Roasting attacks in a controlled lab environment.
· Explore Pass-the-Hash and NTLM Relay techniques.
· Integrate BloodHound for domain mapping and attack path visualization.
· Document detection and mitigation strategies for each attack.

📌 Notes

· This lab is built entirely in an isolated virtual environment for educational purposes.
· No production systems or real user data are involved.
· All techniques are practiced under the Grey Hat code of ethics: never harm an innocent, defend the weak without expecting payment, punish the abuser without feeling guilt.

```