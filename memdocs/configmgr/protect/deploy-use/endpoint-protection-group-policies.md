---
title: Správa řešení Endpoint Protection pomocí zásad skupiny
titleSuffix: Configuration Manager
description: Naučte se spravovat Endpoint Protection pomocí zásad skupiny.
ms.date: 08/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d028dc6149ae1fee2d61634b96ccf450fc8f4b24
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700595"
---
# <a name="use-group-policy-settings-to-manage-endpoint-protection-in-previous-versions-of-windows"></a>Použití nastavení Zásady skupiny pro správu Endpoint Protection v předchozích verzích Windows

**Platí pro:**

- [Rozšířená ochrana před internetovými útoky v programu Microsoft Defender (ATP v programu Microsoft Defender)](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE2O8jv)
- System Center Endpoint Protection na následujících zařízeních nižší úrovně:
    - Windows Server 2012 R2
    - Windows 8.1
    - Windows Server 2012
    - Windows 8
    - Windows Server 2008 R2 SP1
    - Windows 7 SP1
    - Windows Server 2008 SP2
    - Windows Vista

Je možné, že máte několik zařízení s Windows nižší úrovně nebo starší verze, která jsou povolená v Endpoint Protection, ale jsou mimo vaši Configuration Manager hierarchii. Například zařízení v zóně demilitarizovaná nebo zařízeních, která jsou integrovaná prostřednictvím fúzí a akvizic. 

V těchto zařízeních můžete spravovat Endpoint Protection pomocí nastavení Zásady skupiny, která jsou popsaná takto:

- [Kopírování definic zásad Endpoint Protection](#copy-endpoint-protection-policy-definitions)
- Načtěte Endpoint Protection definice zásad do některého z následujících umístění:
    - [Centrální obchod na řadiči domény (doporučeno)](#load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller)
    - [Místní zařízení](#load-endpoint-protection-group-policy-settings-into-your-local-device)

> [!NOTE]
> Informace o tom, jak pomocí nastavení Zásady skupiny spravovat antivirovou ochranu v programu Microsoft Defender ve Windows 10, Windows Server 2019 a Windows Server 2016, najdete v tématu [použití zásady skupiny nastavení ke konfiguraci a správě antivirové ochrany v programu Microsoft Defender](/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus).

## <a name="copy-endpoint-protection-policy-definitions"></a>Kopírování definic zásad Endpoint Protection

Na zařízení s Windows na nižší úrovni, které je spravované pomocí Endpoint Protection zkopírujte soubory definice zásad Endpoint Protection.

1. Přejít do složky **C:\Program Files\Microsoft Security Client\Admx**. 

2. Zkomprimujte následující soubory do souboru zip, například **SCEP_admx.zip**:
    - **EndPointProtection.adml**
    - **EndPointProtection. admx**
3. Zkopírujte soubor zip do dočasné složky. Například **c:\ temp_SCEP_GPO_admx**.
4. Soubor extrahujte. 

> [!NOTE]
> Klíče registru pro konfiguraci nastavení zásad Endpoint Protection najdete v části **HKEY_LOCAL_MACHINE \software\policies\microsoft\microsoft antimalware**.

## <a name="load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller"></a>Načtení nastavení Zásady skupiny Endpoint Protection do centrálního úložiště na řadiči domény

Pokud používáte [centrální úložiště pro Zásady skupiny šablony pro správu](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra), proveďte následující kroky, abyste načetli a nakonfigurovali Endpoint Protection nastavení zásad skupiny. Toto je doporučená metoda.

1. Přejít do složky, do které jste extrahovali soubory definic zásad Endpoint Protection.
2. Zkopírujte soubory. admx a. adml do složky **PolicyDefinitions** na řadiči domény:
    1. Zkopírujte **EndPointProtection. admx** do ** \\ \\ \<forest.root\> \\ zásad adresáře SYSVOL \\ \<domain\> \\ \\ PolicyDefinitions**. 
    2. Zkopírujte **EndPointProtection. adml** do ** \\ \\ \<forest.root\> \\ \\ \<domain\> \\ zásad SYSVOL \\ PolicyDefinitions \\ en-US**.  

    Příklad:
    
    - Zkopírujte **EndPointProtection. admx** do ** \\ DC\SYSVOL\contoso.com\Policies\PolicyDefinitions**.
    - Zkopírujte **EndPointProtection. adml** do ** \\ DC\SYSVOL\contoso.com\Policies\PolicyDefinitions\en-US**.
    
    kde **DC** je název vašeho řadiče domény a **contoso.com** je vaše doména.

3. Otevřete [Konzola pro správu zásad skupiny](/internet-explorer/ie11-deploy-guide/group-policy-and-group-policy-mgmt-console-ie11) a v doméně vytvořte nový objekt Zásady skupiny (GPO), například **Endpoint Protection**.
4. Klikněte pravým tlačítkem na objekt zásad skupiny pro Endpoint Protection a klikněte na **Upravit**.
5. V Editor pro správu zásad skupiny jděte do části zásady **Konfigurace počítače**  >  **Policies**  >  **šablony pro správu: definice zásad**  >  **Windows**  >  **Endpoint Protection**.

   Zobrazí se seznam Endpoint Protectionch zásad skupiny.

6. Rozbalíte část obsahující nastavení, které chcete nakonfigurovat, dvojím kliknutím na toto nastavení otevřete a proveďte změny konfigurace.

## <a name="load-endpoint-protection-group-policy-settings-into-your-local-device"></a>Načtení nastavení Zásady skupiny Endpoint Protection do místního zařízení

Místo použití centrálního úložiště pro načítání definic zásad Endpoint Protection je můžete uložit místně do svého zařízení.

1. Přejít do složky, do které jste extrahovali soubory definic zásad Endpoint Protection.
2. Zkopírujte soubory. admx a. adml do místní složky PolicyDefinitions.
    1. Zkopírujte **EndPointProtection. admx** do **složky% SystemRoot%/PolicyDefinitions**. 
    2. Zkopírujte **EndPointProtection. adml** do **složky% SystemRoot%/PolicyDefinitions/en-US**.
    
    Příklad:

    - Zkopírujte **EndPointProtection. admx** do **C:\Windows\PolicyDefinitions**.
    - Zkopírujte **EndPointProtection. adml** do **C:\Windows\PolicyDefinitions\en-US**.
    
3. Otevřete Editor místních zásad skupiny.
4. Přejít na **Konfigurace počítače**  >  **šablony pro správu**  >  **součásti systému Windows**  >  **Endpoint Protection**.

    Zobrazí se seznam Endpoint Protectionch zásad skupiny.

5. Rozbalíte část obsahující nastavení, které chcete nakonfigurovat, dvojím kliknutím na toto nastavení otevřete a proveďte změny konfigurace.

## <a name="next-steps"></a>Další kroky
- Přehled Endpoint Protection najdete v tématu [Endpoint Protection](endpoint-protection.md).
- Informace o ruční konfiguraci Endpoint Protection u samostatného klienta najdete v tématu [konfigurace Endpoint Protection na samostatném klientovi](endpoint-protection-configure-standalone-client.md).