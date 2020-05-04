---
title: Stáhnout definice ze sdílené síťové složky
titleSuffix: Configuration Manager
description: Naučte se, jak ručně stáhnout nejnovější aktualizace definic od Microsoftu a potom nakonfigurovat klienty tak, aby si tyto definice stáhli.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9afeee7f7111994f0ae3891c7ecd99a11d7edd7d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715680"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share"></a>Povolit Endpoint Protection definice malwaru ke stažení ze sdílené síťové složky

*Platí pro: Configuration Manager (Current Branch)*

 Nejnovější aktualizace definic od Microsoftu můžete stáhnout ručně a potom nakonfigurovat klienty tak, aby si tyto definice stáhli ze sdílené složky v síti. Pokud používáte tento zdroj aktualizací, aktualizace definic můžou také spouštět uživatelé.

> [!NOTE]
>  Klienti můžou stahovat aktualizace definic jenom v případě, že mají k dané sdílené složce oprávnění ke čtení.

 Další informace o tom, jak stáhnout definici a aktualizace modulu pro uložení ve sdílené složce, najdete v tématu [Instalace nejnovějšího antimalwarového a antispywarového softwaru společnosti Microsoft](https://www.microsoft.com/wdsi/definitions).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Postup konfigurace stahování definic ze sdílené složky

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.

2.  V pracovním prostoru **Prostředky a kompatibilita** rozbalte položku **Endpoint Protection**a potom klikněte na **Antimalwarové zásady**.

3.  Otevřete stránku vlastností pro **Výchozí antimalwarové zásady** nebo vytvořte novou antimalwarovou zásadu. Další informace o tom, jak vytvořit antimalwarové zásady, najdete v tématu [Postup vytvoření a nasazení antimalwarových zásad pro Endpoint Protection](endpoint-antimalware-policies.md).

4.  V části **aktualizace Security Intelligence** v dialogovém okně antimalwarové vlastnosti klikněte na **nastavit zdroj**.
    - Oddíl **aktualizace definic** se přejmenoval na **aktualizace Security Intelligence** začínající v Configuration Manager verze 1902.

5.  V dialogu **Konfigurovat zdroje aktualizace definice** vyberte **Aktualizace ze sdílených složek souboru UNC**.

6.  Kliknutím na **OK** zavřete dialog **Konfigurovat zdroje aktualizace definice** .

7.  Klikněte na **Nastavit cesty**. Potom v dialogu **Konfigurovat cesty UNC aktualizace definice** přidejte jednu nebo několik cest UNC k umístění souborů aktualizací definic ve sdílené síťové složce.

8.  Kliknutím na **OK** zavřete dialog **Konfigurovat cesty UNC aktualizace definice** .


> [!div class="button"]
> [Další krok >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Zpět >](endpoint-configure-alerts.md)
