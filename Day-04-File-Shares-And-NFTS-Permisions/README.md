# Day 04 – File Shares & NTFS Permissions (Department Access Control)

---

## 🎯 Objective

Build the resource access layer of the Helpdesk.Lab environment by:

- Creating departmental shared folders
- Publishing SMB shares
- Configuring NTFS permissions
- Disabling inheritance
- Implementing group-based access control

This simulates a real-world departmental file server setup.

---

## 🗂️ Folder Structure Created

On DC01:

```
C:\Shares\
├── Sales
├── Finance
├── Helpdesk
```

Each folder represents a department within the organization.

---

## 🌐 SMB Shares Created

Each department folder was published as an SMB share:

| Share Name | Local Path              | Protocol |
|------------|------------------------|----------|
| Sales      | C:\Shares\Sales        | SMB      |
| Finance    | C:\Shares\Finance      | SMB      |
| Helpdesk   | C:\Shares\Helpdesk     | SMB      |

System shares (SYSVOL, NETLOGON) remain present from Domain Controller configuration.

---

## 🔐 NTFS Permissions Configuration

### 🔒 Inheritance Disabled

Inheritance was disabled on each departmental folder to prevent unintended permission propagation from parent directories.

This ensures:

- No accidental access from inherited groups
- Full control over explicit access assignments
- Clear and predictable permission structure
- Better troubleshooting visibility

---

## 👥 Group-Based Access Model

Permissions were assigned to Security Groups (not individual users).

---

### 🟦 Sales Folder Permissions

```
HELPDESK\Sales_SG        → Modify
BUILTIN\Administrators   → Full Control
NT AUTHORITY\SYSTEM      → Full Control
CREATOR OWNER            → Full Control (subfolders/files only)
```

---

### 🟦 Finance Folder Permissions

```
HELPDESK\Finance_SG      → Modify
BUILTIN\Administrators   → Full Control
NT AUTHORITY\SYSTEM      → Full Control
CREATOR OWNER            → Full Control (subfolders/files only)
```

---

### 🟦 Helpdesk Folder Permissions

```
HELPDESK\Helpdesk_SG     → Modify
BUILTIN\Administrators   → Full Control
NT AUTHORITY\SYSTEM      → Full Control
CREATOR OWNER            → Full Control (subfolders/files only)
```

---

## 🧠 Key Concepts Practiced

- SMB share creation
- NTFS permission configuration
- Disabling inheritance
- Explicit vs inherited permissions
- Role-Based Access Control (RBAC)
- Department-level resource isolation
- Enterprise permission design principles

---

## 🏢 Why Assign Permissions to Groups?

Best practice:

❌ Do NOT assign NTFS permissions directly to users  
✅ Assign permissions to security groups  
✅ Add users to groups  

Benefits:

- Scalable management
- Simplified onboarding/offboarding
- Cleaner auditing
- Easier troubleshooting
- Reduced permission sprawl

---

## 📊 Outcome

The Helpdesk.Lab environment now contains:

- Structured departmental file shares
- Clean NTFS permissions
- Inheritance disabled for isolation
- Group-based access control
- Clear separation of departmental resources

The environment now reflects a realistic small-to-medium business file server deployment.

---

## 🚀 Next Steps (Day 05 Preview)

- Deploy Windows 10 client VM
- Join client to Helpdesk.Lab domain
- Log in as departmental users
- Test access to:
  ```
  \\DC01\Sales
  \\DC01\Finance
  \\DC01\Helpdesk
  ```
- Validate permission enforcement
- Begin drive mapping via Group Policy (GPO)

---

## 📌 Lab Reflection

Day 04 transitioned the lab from identity management to resource control. By disabling inheritance and implementing explicit group-based permissions, the environment now mirrors enterprise file server best practices.

This layer introduces realistic helpdesk troubleshooting scenarios related to access control and permission management.
