# 📋 App Permissions Report — Microsoft Entra ID

A PowerShell script that exports all **App Registration API permissions** (Delegated & Application) from **Microsoft Entra ID (Azure AD)** to a CSV file using **Microsoft Graph PowerShell SDK**.

---

## 📌 What It Does

- Retrieves **all App Registrations** from your Entra ID tenant
- Maps each permission to its readable name using **Service Principals**
- Identifies whether each permission is:
  - ✅ **Application Permission** (App Role)
  - ✅ **Delegated Permission** (OAuth2 Scope)
- Exports the results to a **CSV file**

---

## 📂 Output

The CSV is saved at:
```
D:\Scripts\Data Import\AppPermissionsReport.csv
```

### CSV Columns

| Column            | Description                              |
|-------------------|------------------------------------------|
| `ApplicationName` | Display name of the App Registration     |
| `ApplicationId`   | Application (Client) ID                  |
| `ResourceAPI`     | Name of the resource API (e.g., MS Graph)|
| `PermissionName`  | Permission name (e.g., `User.Read.All`)  |
| `PermissionType`  | `Application` or `Delegated`             |

---

## ✅ Prerequisites

### 1. Install Microsoft Graph PowerShell SDK
```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```

### 2. Required Permissions (Admin consent required)

| Permission                  | Type        |
|-----------------------------|-------------|
| `Application.Read.All`      | Delegated   |
| `ServicePrincipal.Read.All` | Delegated   |

### 3. Connect to Microsoft Graph
```powershell
Connect-MgGraph -Scopes "Application.Read.All","ServicePrincipal.Read.All"
```

---

## ▶️ How to Run

1. Clone this repository or download `AppPermissionsReport.ps1`
2. Open **PowerShell** as Administrator
3. Connect to Microsoft Graph (see above)
4. Run the script:

```powershell
.\AppPermissionsReport.ps1
```

---

## 🖥️ Sample Output

```
Fetching Service Principals...
Fetching App Registrations...
Processing permissions...
Export complete! File saved at:
D:\Scripts\Data Import\AppPermissionsReport.csv
```

---

## 📝 Notes

- The script uses a **hashtable lookup** for Service Principals, making it efficient even in large tenants.
- If a permission ID cannot be resolved, `PermissionName` will show `UNKNOWN`.
- The output folder is created automatically if it does not exist.

---

## 📄 License

This project is licensed under the **MIT License** — feel free to use and modify.
