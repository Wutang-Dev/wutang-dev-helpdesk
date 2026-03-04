# Day 05 – Domain Join & Authentication Validation

## 🎯 Objective
Join a Windows client machine to the Helpdesk.Lab domain and validate domain authentication before continuing with further lab configurations (GPO, drive mapping, permission testing).

---

## 🖥️ Client Build

**Virtual Machine Configuration**
- Name: CLIENT01
- Generation: 2
- RAM: 4096 MB
- Disk: 20GB (Dynamically Expanding)
- Network: Helpdesk_Lab_Private

---

## 🌐 Manual Network Configuration

Since DHCP has not yet been deployed, network settings were manually configured:

| Setting | Value |
|----------|--------|
| IP Address | 10.0.0.100 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 10.0.0.10 (DC01) |

---

## 🔎 Connectivity Validation

Before attempting domain join, the following tests were performed:

```powershell
ping 10.0.0.10
nslookup helpdesk.lab
ping helpdesk.lab
```

### Results:
- Successful ICMP reply from DC01
- DNS resolved `helpdesk.lab` to 10.0.0.10
- Client confirmed communication with Domain Controller

DNS resolution confirmed Active Directory DNS is functioning correctly.

---

## 🏷️ Machine Rename

Before joining the domain, the computer was renamed:

```
CLIENT01
```

System was rebooted before proceeding.

---

## 🔐 Domain Join

Domain joined:

```
helpdesk.lab
```

Successful message received:

> “Welcome to the Helpdesk.Lab domain.”

System rebooted after join.

---

## 👤 Domain Logon Test

Logged in as domain user:

```
HELPDESK\Muhammad Ali
```

Validation performed:

```powershell
whoami
```

Result:

```
helpdesk\m.ali
```

This confirms:
- Authentication is occurring against Active Directory
- Client is properly joined to domain
- User account and credentials are functioning correctly

---

## 🧠 Key Learning Points

- Active Directory depends heavily on DNS
- Domain join will fail if DNS is misconfigured
- Manual IP configuration reinforces understanding of networking fundamentals
- Domain authentication can be verified using `whoami` and `%logonserver%`
- Proper lab sequencing matters (Client join before GPO/Drive Mapping)

---

## ✅ Lab Status

Current Environment Includes:

- Windows Server 2022 Domain Controller (DC01)
- Active Directory Domain Services
- DNS (AD-integrated)
- Organizational Units
- Security Groups
- NTFS & Share Permissions
- Domain-Joined Client (CLIENT01)
- Verified Domain Authentication

---

## 🚀 Next Steps (Day 06)

- Test departmental share access
- Validate security group permission enforcement
- Implement Drive Mapping via Group Policy

---

End of Day 05.
