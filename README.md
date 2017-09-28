# MIcrosoft Intune - Testing your configuration
![Intune](./media/Sign_In.png)

## PreRequisite Software
- Current stable release of Pester
- AzureAD Powershell module
- Access to Internet to access the Microsoft Graph API

## Tests

### Office 365 Tests
> This tests that Modern Authentication is Enabled
- has Modern Authentication is Enabled

```powershell
Invoke-Pester .\Intune.tests.ps1 -tag O365
```

### Mobile Device Management Tests
> This tests the Mobile Device Management Settings and Policy 
- has the Mobile device management authority set to Intune (Set in Script - Change as required)
- Enrollment restrictions - Device Type Restrictions (Set in Script - Change as required)
  -  has Android platform Enrollment: 'Allowed' 
  -  has Android platform Enrollment: osMinimumVersion= '5.1' 
  - has Android 'Personally Owned Devices' Enrollment: 'Blocked' 
  - has iOS platform Enrollment: 'Blocked' 
  - has macOS platform Enrollment: 'Blocked' 
  - has Windows (8.1+) platform Enrollment: 'Blocked' 
  - has Windows Mobile platform Enrollment: 'Blocked'
- Enrollment restrictions - Device Limit Restrictions (Set in Script - Change as required)
  - has maximum number of devices a user can enroll set as 1
  - has at least one 'Term and Condition' set (Optional)
  - Intune Mobile Device Managment Policy Checks (Referenced from MDM_Policy.json - Add Remove as necessary)
    - Android Device Restrictions checks
      - Minimum password length' is correct
      - Password requirement' is set correctly
      - 'Number of sign-in failures before wiping device' is set correctly

```powershell
Invoke-Pester .\Intune.tests.ps1 -tag MDM
```

### License Tests
> This tests the correct license type and count have been assigned to the tenant (Set in Script - Change as required)
- contains the correct skuPartNumber
- contains the correct skuPartNumber
- has the correct licence type assigned
- has capabilityStatus set to ENABLED
- has the correct amount of licences assigned


```powershell
Invoke-Pester .\Intune.tests.ps1 -tag License
```

### Intune Application Protection Policy Checks
> This tests the various policy settings have been set correctly.
- iOS Application Protection Policy checks  (Referenced from MAM_Policy.json - Add Remove as necessary)
  - contains at least 1 iOS Managed AppProtection policy
  - Prevent iTunes and iCloud backups
  - Allow app to transfer data to other apps
  - Allow app to receive data from other apps
  - Prevent 'Save As'
  - Select which storage service corporate data can be saved to
  - Restrict cut, copy, and paste with other app
  - Restrict web content to display in the Managed Browser
  - Encrypt app data
  - Disable contacts sync
  - Disable printing
  - Require PIN for access
  - Allow simple PIN
  - PIN length
  - Allow fingerprint instead of PIN
  - Disable app PIN when device PIN is managed
  - Require corporate credentials for access
  - Recheck the access interval requirements after (minutes)
  - Offline interval before app data is wiped (days)
  - Require minimum iOS operating system
  - Targeted Security Group count

- Android Application Protection Policy checks  (Referenced from MAM_Policy.json - Add Remove as necessary)
  - contains at least 1 iOS Managed AppProtection policy
  - Prevent Android backups
  - Allow app to transfer data to other apps
  - Allow app to receive data from other apps
  - Prevent 'Save As'
  - Select which storage service corporate data can be saved to
  - Restrict cut, copy, and paste with other app
  - Restrict web content to display in the Managed Browser
  - Encrypt app data
  - Disable contacts sync
  - Disable printing
  - Require PIN for access
  - Allow simple PIN
  - PIN length
  - Allow fingerprint instead of PIN
  - Disable app PIN when device PIN is managed
  - Require corporate credentials for access
  - Recheck the access interval requirements after (minutes)
  - Offline interval before app data is wiped (days)
  - Require minimum iOS operating system
  - Targeted Security Group count

```powershell
Invoke-Pester .\Intune.tests.ps1 -tag Policy
```


