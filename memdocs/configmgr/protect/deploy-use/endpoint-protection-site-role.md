---
title: Vytvoření role systému lokality bodu Endpoint Protection
titleSuffix: Configuration Manager
description: Naučte se konfigurovat Endpoint Protection pro správu zabezpečení a malwaru v Configuration Manager klientských počítačích.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a8714f5bacf97e440bae07834ee6df5430a3d37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81710829"
---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Vytvoření role systému lokality bodu Endpoint Protection

*Platí pro: Configuration Manager (Current Branch)*

Role systému lokality bodu ochrany Endpoint Protection musí být instalovaná dřív než Endpoint Protection. Musí se nainstalovat jenom na jeden server systému lokality a na vrchol hierarchie v lokalitě centrální správy nebo samostatné primární lokalitě.

Použijte jeden z následujících postupů v závislosti na tom, zda chcete nainstalovat nový server systému lokality pro Endpoint Protection nebo použít stávající server systému lokality:
- [Nainstalovat na nový server systému lokality](#new-site-system-server)
- [Nainstalovat na existující server systému lokality](#existing-site-system-server)

> [!IMPORTANT]
>  Při instalaci Endpoint Protectionho bodu je klient Endpoint Protection nainstalován na server, který je hostitelem Endpoint Protectionho bodu. V tomto klientovi jsou zakázané služby a kontroly, aby nevznikaly konflikty s antimalwarovým řešením, které může být na serveru nainstalované. Pokud později povolíte tento server pro správu pomocí Endpoint Protection a vyberte možnost odebrání antimalwarového řešení jiného výrobce, produkt třetí strany nebude odebrán. Produkt musíte odinstalovat ručně.

## <a name="new-site-system-server"></a>Nový server systému lokality

1.  V konzole Configuration Manager klikněte na možnost **Správa**.

2.  V pracovním prostoru **Správa** rozbalte nabídku **Konfigurace lokality**a klikněte na možnost **Servery a role serveru**.

3.  Na kartě **Domů** ve skupině **Vytvoření** klikněte na možnost **Vytvořit server systému lokalit**.

4.  Na stránce **Obecné** definujte obecné nastavení systému lokalit a klikněte na **Další**.

5.  Na stránce **Výběr systémové role** vyberte v seznamu dostupných rolí možnost **Bod ochrany koncového bodu Endpoint Protection** a potom klikněte na **Další**.

6.  Na stránce **Endpoint Protection** zaškrtněte políčko **Přijímám licenční podmínky ochrany koncového bodu Endpoint Protection** a potom klikněte na **Další**.

    > [!IMPORTANT]
    >  Pokud nepřijímáte licenční podmínky, nemůžete použít Endpoint Protection v Configuration Manager.

7.  Na stránce **Cloud Protection Service** vyberte úroveň informací, které chcete odeslat společnosti Microsoft, abyste mohli pomáhat s vývojem nových definic, a potom klikněte na tlačítko **Další**.

    > [!NOTE]
    >  Tato možnost konfiguruje službu ochrany cloudu (dříve označovanou jako služba Microsoft Active Protection Service nebo MAPS), která se používá ve výchozím nastavení. Potom můžete nakonfigurovat vlastní nastavení pro každou antimalwarovou zásadu, kterou vytvoříte. Připojte se ke Cloud Protection Service, abyste mohli lépe zabezpečit počítače tím, že poskytnete Microsoft s ukázkami malwaru, které můžou Microsoftu pomáhat zajistit aktuálnost antimalwarových definic. Kromě toho, když se připojíte ke službě Cloud Protection, může klient Endpoint Protection použít službu Dynamic Signature ke stažení nových definicí před jejich publikováním do web Windows Update. Další informace najdete v tématu [Vytvoření a nasazení antimalwarových zásad pro Endpoint Protection](endpoint-antimalware-policies.md).

8.  Dokončete průvodce.


## <a name="existing-site-system-server"></a>Existující server systému lokality

1.  V konzole Configuration Manager klikněte na možnost **Správa**.

2.  V pracovním prostoru **Správa** rozbalte nabídku **Konfigurace lokality**, klikněte na možnost **servery a role systému lokality**a pak vyberte server, který chcete použít pro Endpoint Protection.

3.  Na kartě **Domů** ve skupině **Server** klikněte na **Přidat role systému lokality**.

4.  Na stránce **Obecné** definujte obecné nastavení systému lokalit a klikněte na **Další**.

5.  Na stránce **Výběr systémové role** vyberte v seznamu dostupných rolí možnost **Bod ochrany koncového bodu Endpoint Protection** a potom klikněte na **Další**.

6.  Na stránce **Endpoint Protection** zaškrtněte políčko **Přijímám licenční podmínky ochrany koncového bodu Endpoint Protection** a potom klikněte na **Další**.

    > [!IMPORTANT]
    >  Pokud nepřijímáte licenční podmínky, nemůžete použít Endpoint Protection v Configuration Manager.

7.  Na stránce **Cloud Protection Service** vyberte úroveň informací, které chcete odeslat společnosti Microsoft, abyste mohli pomáhat s vývojem nových definic, a potom klikněte na tlačítko **Další**.

    > [!NOTE]
    >  Tato možnost nakonfiguruje nastavení služby Cloud Protection (dříve označované jako MAPS), která se používají ve výchozím nastavení. Můžete nakonfigurovat vlastní nastavení pro každou antimalwarovou zásadu, kterou vytvoříte. Další informace najdete v tématu [Vytvoření a nasazení antimalwarových zásad pro Endpoint Protection](endpoint-antimalware-policies.md).

8.  Dokončete průvodce.
