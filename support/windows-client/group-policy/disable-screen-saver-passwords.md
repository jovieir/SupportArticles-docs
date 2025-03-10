---
title: Disable screen saver passwords by using policies
description: Describes how to disable screen saver passwords by using policies.
ms.date: 01/15/2025
manager: dcscontentpm
audience: itpro
ms.topic: troubleshooting
ms.reviewer: kaushika, CCLAY
ms.custom:
- sap:group policy\problems applying group policy
- pcy:WinComm Directory Services
---
# Disable screen saver passwords by using policies

This article describes how to make screen saver password locks unavailable on systems in a site, domain, or organizational unit, by using the policies available.

_Applies to:_ &nbsp; Windows Server (All supported versions), Windows client (All supported versions)  
_Original KB number:_ &nbsp; 272304

## Disable screen saver passwords

To make screen saver password locks unavailable, follow these steps:

1. Click Start, and then click **Run**.
2. Type *mmc*, and then click **OK** to start the Microsoft Management Console (MMC).
3. On the Console menu, click **Add/Remove Snap-ins**, and then click **Add**.
4. Click **Group Policy**, and then click **Add**.

    The **Select Group Policy Object** dialog box appears. If you want to apply this policy only to your computer, make sure that your local computer is listed in the Group Policy object, and then click **Finish**.

    Alternatively, if this will be an Active Directory policy, click **Browse**, select the site, domain, or organizational unit to which you want this policy to apply, and then click **Finish**.

5. Click **Close**.
6. Expand **User Configuration**, and then expand **Administrative Templates**.
1. Expand **Control Panel**, and then click **Personalization**.
8. In the right pane, double-click **Password protect the screen saver**.
9. Select Disable on the **Policy** tab. This prevents users from setting passwords on screen savers for this computer or domain.
10. Click the **Explain** tab for information about how to use this policy.
11. Click **Apply**.
12. Click **OK**, and then close the MMC.
