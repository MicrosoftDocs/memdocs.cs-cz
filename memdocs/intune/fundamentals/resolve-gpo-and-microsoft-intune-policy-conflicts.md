---
title: Řešení konfliktů GPO a zásad Intune
titleSuffix: Microsoft Intune
description: Přečtěte si o řešení konfliktů mezi zásadami skupiny a zásadami konfigurace Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e76af5b7-e933-442c-a9d3-3b42c5f5868b
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a159d9d2cb31090fdb38ef2fc692f6af0297166
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79330683"
---
# <a name="resolve-group-policy-objects-gpo-and-microsoft-intune-policy-conflicts"></a>Řešení konfliktů objektů zásad skupiny (GPO) a zásad Microsoft Intune

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> Informace v tomto tématu se vztahují jenom na desktopové systémy Windows, které spravujete jako počítače pomocí softwarového klienta Intune.

Intune používá zásady, které vám pomůžou spravovat nastavení na počítačích s Windows. Pomocí zásad můžete třeba na počítačích řídit nastavení brány Windows Firewall. Mnohá nastavení služby Intune se podobají nastavením, která nejspíš konfigurujete pomocí zásad skupiny Windows. Někdy se ale může stát, že se tyto dvě metody dostanou vzájemně do konfliktu.

Dojde-li ke konfliktům, má Zásady skupiny na úrovni domény přednost před zásadami Intune, pokud se počítač nemůže přihlásit k doméně. V takovém případě se na klientském počítači použijí zásady Intune.

## <a name="what-to-do-if-you-are-using-group-policy"></a>Co je potřeba udělat, když používáte zásady skupiny
Zkontrolujte, že žádné zásady, které používáte, nejsou spravované zásadami skupiny. Abyste lépe zabránili konfliktům, můžete využít některé z těchto metod:

- Před instalací klienta Intune přesuňte počítače do organizační jednotky služby Active Directory, u které se nepoužívá nastavení zásad skupiny. V organizačních jednotkách obsahujících počítače zaregistrované v Intune, u kterých nechcete používat nastavení zásad skupiny, můžete taky zablokovat dědičnost zásad skupiny.

- Pomocí filtru skupiny zabezpečení omezte objekty GPO jenom na počítače, které nespravuje Intune.

- Zakažte nebo odeberte objekty zásad skupiny, které jsou v konfliktu se zásadami Intune.

Další informace o službě Active Directory a zásadách skupiny Windows najdete v dokumentaci k Windows Serveru.

## <a name="how-to-filter-existing-gpos-to-avoid-conflicts-with-intune-policy"></a>Jak filtrovat stávající objekty GPO, aby nedocházelo ke konfliktům se zásadami Intune
Pokud jste našli objekty GPO s nastavením, které je v konfliktu se zásadami Intune, můžete pomocí filtrů skupiny zabezpečení omezit tyto objekty zásad skupiny jenom na počítače, které nespravuje Intune.

<!--- ### Use WMI filters
WMI filters selectively apply GPOs to computers that satisfy the conditions of a query. To apply a WMI filter, deploy a WMI class instance to all PCs in the enterprise before you enroll any PCs in the Intune service.

#### To apply WMI filters to a GPO

1. Create a management object file by copying and pasting the following into a text file, and then saving it to a convenient location as **WIT.mof**. The file contains the WMI class instance that you deploy to PCs that you want to enroll in the Intune service.

    ```
    //Beginning of MOF file.
    #pragma classflags("forceupdate")
    #pragma namespace ("\\\\.\\Root")
    instance of __Namespace
    {
       Name = "WindowsIntune";
    };

    #pragma namespace ("\\\\.\\Root\\WindowsIntune")
    [
       Description("This class defines Microsoft Intune common properties")
    ]
    class WindowsIntune_ManagedNode
    {
       [ read, Description("This defines whether Microsoft Intune Policy is enabled"): DisableOverride ToSubClass ]
       boolean WindowsIntunePolicyEnabled;
       [ read, key, Description("This property defines the version." "Example: 1.0"): ToSubClass ]
       string Version;
    };

    instance of WindowsIntune_ManagedNode
    {
       Version = "1.0";
       WindowsIntunePolicyEnabled = 1;
    };
    ```

2. Use either a startup script or Group Policy to deploy the file. The following is the deployment command for the startup script. The WMI class instance must be deployed before you enroll client PCs in the Intune service.

    **C:/Windows/System32/Wbem/MOFCOMP &lt;path to MOF file&gt;\wit.mof**

3. Run either of the following commands to create the WMI filters, depending on whether the GPO you want to filter applies to PCs that are managed by using Intune or to PCs that are not managed by using Intune.

    - For GPOs that apply to PCs that are not managed by using Intune, use the following:

        ```
        Namespace:root\WindowsIntune
        Query:  SELECT WindowsIntunePolicyEnabled FROM WindowsIntune_ManagedNode WHERE WindowsIntunePolicyEnabled=0
        ```

    - For GPOs that apply to PCs that are managed by Intune, use the following:

        ```
        Namespace:root\WindowsIntune
        Query:  SELECT WindowsIntunePolicyEnabled FROM WindowsIntune_ManagedNode WHERE WindowsIntunePolicyEnabled=1
        ```

4. Edit the GPO in the Group Policy Management console to apply the WMI filter that you created in the previous step.

    - For GPOs that should apply only to PCs that you want to manage by using Intune, apply the filter **WindowsIntunePolicyEnabled=1**.

    - For GPOs that should apply only to PCs that you do not want to manage by using Intune, apply the filter **WindowsIntunePolicyEnabled=0**.

For more information about how to apply WMI filters in Group Policy, see the blog post [Security Filtering, WMI Filtering, and Item-level Targeting in Group Policy Preferences](https://go.microsoft.com/fwlink/?LinkId=177883). --->


Můžete použít objekty zásad skupiny jenom na skupiny zabezpečení, které jsou pro vybraný objekt zásad skupiny zadané v oblasti **Filtrování zabezpečení** konzoly pro správu zásad skupiny. Objekty zásad skupiny se ve výchozím nastavení používají pro skupinu *Authenticated Users*.

- V modulu snap-in **Uživatelé a počítače služby Active Directory** vytvořte novou skupinu zabezpečení obsahující účty počítačů a uživatelské účty, které nechcete spravovat pomocí Intune. Vaši skupinu můžete třeba pojmenovat *Není v Microsoft Intune*.

- V konzole pro správu zásad skupiny klikněte na kartě **Delegování** pro vybraný objekt zásad skupiny pravým tlačítkem na novou skupinu zabezpečení a udělte uživatelům i počítačům v této skupině zabezpečení příslušná oprávnění **Číst** a **Používat zásady skupiny**. (Oprávnění**Používat zásady skupiny** jsou dostupná v dialogovém okně **Upřesnit** .)

- Pak u vybraného objektu zásad skupiny použijte nový filtr skupin zabezpečení a odeberte výchozí filtr **Authenticated Users**.

S novou skupinou zabezpečení se musí ve změnách služby Intune nakládat jako s registrací.

## <a name="see-also"></a>Viz také
[Správa počítačů s Windows pomocí Intune](manage-windows-pcs-with-microsoft-intune.md)
