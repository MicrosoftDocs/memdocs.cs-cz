---
title: Konfigurace aktualizací definic
titleSuffix: Configuration Manager
description: Naučte se, jak vybrat a nakonfigurovat metody s Endpoint Protection v Configuration Manager, aby se antimalwarové definice v klientských počítačích udržovaly v aktuálním stavu.
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce11ba0cbe4298d32a11de409910ebc3e14c097b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81715764"
---
# <a name="configure-definition-updates-for-endpoint-protection"></a>Konfigurace aktualizací definic pro službu Endpoint Protection  

*Platí pro: Configuration Manager (Current Branch)*

 Díky Endpoint Protection v Configuration Manager můžete použít některou z několika dostupných metod, které udržují aktuální definice antimalwarových definic v klientských počítačích ve vaší hierarchii. Informace v tomto tématu vám můžou pomoct vybrat a nakonfigurovat tyto metody.

 Pokud chcete aktualizovat definice malwaru, můžete použít jednu nebo několik z těchto metod:

- [Aktualizace distribuované z Configuration Manager](endpoint-definitions-configmgr.md) – Tato metoda používá Configuration Manager aktualizace softwaru k doručování definic a aktualizací stroje do počítačů ve vaší hierarchii.

- [Aktualizace distribuované z Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) – Tato metoda používá vaši infrastrukturu WSUS k doručování definic a aktualizací stroje do počítačů.

- [Aktualizace distribuované z Microsoft Update](endpoint-definitions-microsoft-updates.md) – Tato metoda umožňuje počítačům přímé připojení k Microsoft Update, aby bylo možné stahovat definice a aktualizace stroje. Tato metoda může být užitečná pro počítače, které se moc často nepřipojují k podnikové síti.

- [Aktualizace distribuované z centra společnosti Microsoft pro ochranu před škodlivým softwarem](endpoint-definitions-protection-center.md) – Tato metoda bude stahovat aktualizace definic z centra společnosti Microsoft pro ochranu před škodlivým softwarem.

- [Aktualizace ze sdílených složek souboru UNC](endpoint-definitions-network.md) – pomocí této metody můžete uložit nejnovější definice a aktualizace stroje do sdílené složky v síti. Klienti potom můžou nainstalovat aktualizace přes síť.

  Můžete nakonfigurovat několik zdrojů aktualizace definic a určit pořadí, ve kterém se mají vyhodnotit a použít. To se provádí v dialogu **Konfigurovat zdroje aktualizace definice** při vytváření antimalwarových zásad.

> [!IMPORTANT]
>  U počítačů s Windows 10 je potřeba nakonfigurovat Endpoint Protection pro aktualizaci definicí malwaru pro Windows Defender.

## <a name="how-to-configure-definition-update-sources"></a>Konfigurace zdrojů aktualizace definic
 Následující postup umožňuje konfiguraci zdrojů aktualizací definic, které se mají používat u jednotlivých antimalwarových zásad.

1.  V konzole Configuration Manageru klikněte na **Prostředky a kompatibilita**.

2.  V pracovním prostoru **Prostředky a kompatibilita** rozbalte položku **Endpoint Protection**a potom klikněte na **Antimalwarové zásady**.

3.  Otevřete stránku vlastností pro **Výchozí antimalwarové zásady** nebo vytvořte novou antimalwarovou zásadu. Další informace o tom, jak vytvořit antimalwarové zásady, najdete v tématu [Postup vytvoření a nasazení antimalwarových zásad pro Endpoint Protection](endpoint-antimalware-policies.md).

4.  V části **aktualizace Security Intelligence** v dialogovém okně antimalwarové vlastnosti klikněte na **nastavit zdroj**.
    - Oddíl **aktualizace definic** se přejmenoval na **aktualizace Security Intelligence** začínající v Configuration Manager verze 1902.

5.  V dialogu **Konfigurovat zdroje aktualizace definice** vyberte zdroje, které chcete použít pro aktualizace definic. Kliknutím na **Nahoru** nebo **Dolů** můžete upravit pořadí, ve kterém se tyto zdroje mají použít.

6.  Kliknutím na **OK** zavřete dialog **Konfigurovat zdroje aktualizace definice** .

## <a name="configure-endpoint-protection-definitions"></a>Konfigurace Endpoint Protection definice

-   [Aktualizace distribuované z Configuration Manager](endpoint-definitions-configmgr.md) – Tato metoda používá Configuration Manager aktualizace softwaru k doručování definic a aktualizací stroje do počítačů ve vaší hierarchii.

-   [Aktualizace distribuované z Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) – Tato metoda používá vaši infrastrukturu WSUS k doručování definic a aktualizací stroje do počítačů.

-   [Aktualizace distribuované z Microsoft Update](endpoint-definitions-microsoft-updates.md) – Tato metoda umožňuje počítačům přímé připojení k Microsoft Update, aby bylo možné stahovat definice a aktualizace stroje. Tato metoda může být užitečná pro počítače, které se moc často nepřipojují k podnikové síti.

-   Aktualizace distribuované z centra společnosti Microsoft pro ochranu před škodlivým softwarem – Tato metoda bude stahovat aktualizace definic z centra společnosti Microsoft pro ochranu před škodlivým softwarem.

-   [Aktualizace ze sdílených složek souboru UNC](endpoint-definitions-network.md) – pomocí této metody můžete uložit nejnovější definice a aktualizace stroje do sdílené složky v síti. Klienti potom můžou nainstalovat aktualizace přes síť.
