---
title: Konfigurace služby Endpoint Protection
titleSuffix: Configuration Manager
description: Přečtěte si, jak nastavit Configuration Manager pro aktualizaci a distribuci definic malwaru pro Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e48f20dd56f445a10faa485b8bb7e86dbb05f75a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81720881"
---
# <a name="configure-endpoint-protection"></a>Konfigurace služby Endpoint Protection

*Platí pro: Configuration Manager (Current Branch)*

Než budete moci použít Endpoint Protection ke správě zabezpečení a malwaru v Configuration Manager klientských počítačích, je nutné provést kroky konfigurace popsané v tomto článku.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Konfigurace aplikace Endpoint Protection v Configuration Manageru  
 Endpoint Protection v Configuration Manager má vnější závislosti a závislosti v rámci produktu.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Postup konfigurace Endpoint Protection v Configuration Manager  
 V následující tabulce najdete kroky, podrobnosti a další informace, které se týkají konfigurace aplikace Endpoint Protection.  

> [!IMPORTANT]  
>  Pokud spravujete službu Endpoint Protection pro počítače s Windows 10, musíte nakonfigurovat Configuration Manager pro aktualizaci a distribuci definic malwaru pro Windows Defender. Windows Defender je součástí Windows 10, ale SCEPInstall se musí pořád nainstalovat a vlastní nastavení klienta pro Endpoint Protection (**Krok 5** níže) se pořád vyžaduje. </br> </br>
> Od Configuration Manager 1802 nemusí mít zařízení s Windows 10 nainstalovanou Endpoint Protection agenta (SCEPInstall). Pokud je už na zařízeních s Windows 10 nainstalovaná, Configuration Manager se neodebere. Správci můžou odebrat agenta Endpoint Protection v zařízeních s Windows 10, na kterých běží aspoň verze klienta 1802. SCEPInstall. exe může stále existovat v C:\Windows\ccmsetup na některých počítačích, ale nemělo by se stahovat při instalaci nových klientů. Vlastní nastavení klienta pro Endpoint Protection (**Krok 5** níže) se pořád vyžadují. <!--503654-->

|Kroky|Podrobnosti|  
|-----------|-------------|  
|**Krok 1:** [vytvoření role systému lokality bodu Endpoint Protection](endpoint-protection-site-role.md)|Role systému lokality bodu ochrany Endpoint Protection musí být instalovaná dřív než Endpoint Protection. Musí se nainstalovat jenom na jeden server systému lokality a na vrchol hierarchie v lokalitě centrální správy nebo samostatné primární lokalitě. |  
|**Krok 2:** [konfigurace výstrah pro Endpoint Protection](endpoint-configure-alerts.md)|Výstrahy upozorňují správce na výskyt určitých událostí, jako třeba napadení malwarem. Výstrahy se zobrazují v uzlu **Výstrahy** pracovního prostoru **Monitorování** nebo taky můžete nastavit, že se budou odesílat e-mailem určitým uživatelům. |  
|**Krok 3:** [Konfigurace zdrojů aktualizace definic pro klienty Endpoint Protection](endpoint-definition-updates.md)|Endpoint Protection lze nakonfigurovat tak, aby pro stažení aktualizací definic používala různé zdroje. |  
|**Krok 4:** [Konfigurace výchozí antimalwarové zásady a vytvoření vlastních antimalwarových](endpoint-antimalware-policies.md) zásad|Výchozí antimalwarová zásada se použije při instalaci klienta Endpoint Protection. Všechny vlastní zásady, které jste nasadili, se ve výchozím nastavení použijí do 60 minut od nasazení klienta. Před nasazením klienta Endpoint Protection se ujistěte, že jste nakonfigurovali antimalwarové zásady. |  
|**Krok 5:** [Konfigurace vlastního nastavení klienta pro Endpoint Protection](endpoint-protection-configure-client.md)|Pomocí vlastního nastavení klienta můžete nakonfigurovat Endpoint Protection nastavení pro kolekce počítačů ve vaší hierarchii.<br /><br /> Poznámka: nekonfigurujte výchozí Endpoint Protection nastavení klienta, pokud si nejste jistí, jestli chcete toto nastavení použít pro všechny počítače ve vaší hierarchii. |  
