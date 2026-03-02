# Day 03 – Active Directory OU Structure, Users & Security Groups

---

## 🎯 Objective

Build the identity and access foundation of the Helpdesk.Lab environment by:

- Creating Organizational Units (OUs)
- Creating domain users
- Creating security groups
- Assigning users to groups following best practices

This establishes Role-Based Access Control (RBAC) principles for future file share and Group Policy configuration.

---

## 🏗️ Organizational Unit (OU) Structure

Instead of using default containers, structured OUs were created:

```
Helpdesk.Lab
├── _Helpdesk.Lab.Users
├── _Helpdesk.Lab.Groups
```

### Why Create OUs?

- Enables Group Policy targeting
- Keeps directory organized
- Separates users from groups
- Scales better in enterprise environments
- Avoids using default “Users” container

---

## 👤 Domain Users Created

Three test users were created inside:

```
_Helpdesk.Lab.Users
```

| Name              | Department  | Username (Example) |
|-------------------|------------|--------------------|
| Muhammad Ali      | Sales      | mali               |
| Mike Tyson        | Finance    | mtyson             |
| Floyd Mayweather  | Helpdesk   | fmayweather        |

### Configuration Notes

- Users created as standard domain users
- Strong passwords set
- Accounts enabled
- No direct permission assignments made

---

## 🔐 Security Groups Created

Inside:

```
_Helpdesk.Lab.Groups
```

The following Global Security Groups were created:

- Sales_SG
- Finance_SG
- Helpdesk_SG

### Naming Convention

```
Department_SG
```

This makes group purpose immediately clear and scalable.

---

## 👥 Group Membership Assignment

Users were added to groups according to department:

| User              | Assigned Group   |
|-------------------|------------------|
| Muhammad Ali      | Sales_SG         |
| Mike Tyson        | Finance_SG       |
| Floyd Mayweather  | Helpdesk_SG      |

Group membership verified via group Properties → Members tab.

---

## 🧠 Key Concepts Practiced

- Active Directory OU structure design
- Creating domain user accounts
- Creating Global Security Groups
- Implementing Role-Based Access Control (RBAC)
- Following enterprise naming conventions
- Assigning permissions via groups (not directly to users)

---

## 🏢 Why Groups Instead of Direct Permissions?

Enterprise best practice:

❌ Do NOT assign permissions directly to users  
✅ Assign permissions to groups  
✅ Add users to groups  

Benefits:

- Easier management
- Scalable access control
- Simplifies onboarding/offboarding
- Cleaner auditing

---

## 📊 Outcome

The domain now contains:

- Structured OU hierarchy
- 3 domain users
- 3 security groups
- Proper group-based membership

This prepares the environment for:

- NTFS file permissions
- Shared folder access control
- Drive mapping via Group Policy
- Helpdesk troubleshooting scenarios

---

## 🚀 Next Steps (Day 04 Preview)

- Create shared folder structure (Sales, Finance, Helpdesk)
- Configure NTFS permissions using security groups
- Share folders properly
- Test access control
- Prepare for drive mapping via GPO

---

## 📌 Lab Reflection

Day 03 focused on identity management and clean directory design.  
By structuring OUs properly and using security groups for access control, the lab now reflects real-world Active Directory administration practices rather than basic test environment setup.

The Helpdesk.Lab environment now has a scalable identity and access foundation.
