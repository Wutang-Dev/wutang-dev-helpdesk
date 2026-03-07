# Day 07 – Drive Mapping via GPO Preferences (Department-Based Access Control)

## 🎯 Objective

Implement automated departmental drive mapping using:

- Group Policy Preferences
- Security Group targeting
- NTFS permission enforcement
- Item-level targeting

This simulates a real-world enterprise environment where users automatically receive mapped drives based on department membership.

---

## 🏗 Lab Environment

**Domain:** Helpdesk.Lab  
**Domain Controller:** DC01  
**Client Machine:** CLIENT01 (Windows 11)  

### Departmental Security Groups

- `Sales_SG`
- `Finance_SG`
- `Helpdesk_SG`

### Shared Folders on DC01

| Department | Share Path         | Drive Letter |
|------------|-------------------|--------------|
| Sales      | \\DC01\Sales      | S:           |
| Finance    | \\DC01\Finance    | F:           |
| Helpdesk   | \\DC01\Helpdesk   | H:           |

---

## 🛠 Implementation Steps

### 1️⃣ Edited Existing GPO

Used previously created GPO:

```
Workstation_Users_Restrictions
```

Navigated to:

```
User Configuration
  → Preferences
      → Windows Settings
          → Drive Maps
```

---

### 2️⃣ Created Drive Mappings

For each department:

- Action: `Update`
- Reconnect: Enabled
- Label set appropriately
- Assigned correct drive letter

Example (Sales):

```
Location: \\DC01\Sales
Drive Letter: S:
Label: Sales Drive
Action: Update
Reconnect: Enabled
```

---

### 3️⃣ Configured Item-Level Targeting (Critical Step)

Under **Common tab** → Enabled:

```
✔ Item-level targeting
```

Configured targeting:

- Sales drive → `Sales_SG`
- Finance drive → `Finance_SG`
- Helpdesk drive → `Helpdesk_SG`

This ensures:

Users only receive drives for their department.

---

## 🧪 Validation & Testing

### 🔹 Test 1 – Sales User (Muhammad Ali)

Group Membership:
```
Sales_SG
```

After running:

```
gpupdate /force
```

Logged out and back in.

Result:

- ✅ S:\ drive mapped
- ❌ No Finance drive
- ❌ No Helpdesk drive

Verified using:

```
gpresult /r
```

Confirmed:
```
Workstation_Users_Restrictions
```
was applied.

---

### 🔹 Test 2 – Finance User (Mike Tyson)

Group Membership:
```
Finance_SG
```

Result after login:

- ✅ F:\ drive mapped
- ❌ No Sales drive
- ❌ No Helpdesk drive

Confirmed correct security targeting and enforcement.

---

## 🔐 Access Control Model Implemented

User → Security Group → NTFS Permissions  
GPO Preferences → Drive Automation  
OU → Policy Scope  

This ensures:

- Least privilege access
- Centralised management
- Automated provisioning
- Clean separation of departments

---

## 🧠 Key Concepts Practiced

- Group Policy Preferences vs Policies
- Drive mapping automation
- Item-level targeting
- Security group-based access control
- NTFS + Share permission alignment
- GPO validation using gpresult
- Real-world departmental segmentation

---

## 🎓 Real-World Relevance

This configuration mirrors enterprise IT environments where:

- Users are added to department security groups
- Drive access is automatically provisioned
- Access is controlled centrally via AD
- No manual drive mapping is required

This is a standard MSP / corporate Active Directory workflow.

---

## ✅ Outcome

Successfully implemented:

- Department-based drive mapping
- Security group targeting
- Automated provisioning
- Verified enforcement through live endpoint testing

Day 07 complete.
