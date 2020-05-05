---
title: Klientská Endpoint Protectionová ochrana
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích a vylepšeních v Endpoint Protection, které vám pomůžou lépe chránit počítač před hrozbami.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: eba7de1705212bb5cb329282bc407317995b82f3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724339"
---
# <a name="endpoint-protection-client-help"></a>Klientská Endpoint Protectionová ochrana

*Platí pro: Configuration Manager (Current Branch)*


Tato verze Windows Defenderu nebo Endpoint Protection obsahuje následující funkce, které vám pomůžou chránit váš počítač před hrozbami:  

-   **Integrace brány Windows Firewall.** Při instalaci Endpoint Protection můžete zapnout nebo vypnout bránu Windows Firewall.  
-   **Systém kontroly sítě.** Tato funkce vylepšuje ochranu v reálném čase tím, že kontroluje síťový provoz a může aktivně blokovat zneužití známých chyb zabezpečení sítě.  
-   **Modul ochrany.** Ochrana v reálném čase vyhledává a brání v instalaci nebo spuštění malwaru v počítači. Aktualizovaný modul ochrany nabízí rozšířené detekční a čisticí funkce s lepším výkonem.  

Windows Defender přichází jako součást operačního systému Windows 10.  V dřívějších verzích systému Windows může správce poskytnout program Windows Defender nebo Endpoint Protection pomocí softwaru pro správu.

Můžete také vyhledat seznam [nejčastějších dotazů pro program Windows Defender a Endpoint Protection](endpoint-protection-client-faq.md). Pomoc při řešení potíží najdete v tématu [řešení potíží s Windows Defenderem nebo Endpoint Protection klientem](troubleshoot-endpoint-client.md). Seznam nových funkcí najdete v tématu [co je nového klienta Windows Defenderu](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender).

## <a name="windows-firewall-integration"></a>Integrace brány Windows Firewall  
 Brána Windows Firewall může zabránit útočníkům nebo škodlivému softwaru získat přístup k vašemu počítači přes internet nebo síť. Když teď instalujete Endpoint Protection, průvodce instalací ověřuje, jestli je brána Windows Firewall zapnutá. Pokud jste bránu Windows Firewall záměrně vypnuli, můžete jejímu zapnutí zabránit tím, že zrušíte zaškrtnutí políčka. Nastavení brány Windows Firewall můžete kdykoli změnit v Ovládacích panelech pomocí nastavení Systém a zabezpečení.  

## <a name="network-inspection-system"></a>Systém kontroly sítě  
 Útočníci stále častěji uskutečňují síťové útoky na existující chyby zabezpečení dřív, než dodavatelé softwaru stihnou vyvinout a distribuovat aktualizace zabezpečení. Studie chyb zabezpečení ukazují, že od počátečního ohlášení útoku může trvat měsíc i déle, než se podaří vyvinout, otestovat a vydat vhodnou aktualizaci zabezpečení. Během této poměrně dlouhé doby je mnoho počítačů ohrožených útoky a pokusy o zneužití. Systém kontroly sítě pracuje s ochranou v reálném čase, aby vás lépe chránil před síťovými útoky. Značně zkracuje dobu mezi zjištěním chyby zabezpečení a vytvořením aktualizace – z týdnů na pár hodin.  

## <a name="award-winning-protection-engine"></a>Vysoce hodnocený modul ochrany  
 Pod digestoří programu Windows Defender nebo Endpoint Protection je jeho oceněný modul ochrany, který se pravidelně aktualizuje. Za tímto modulem stojí tým antimalwarových výzkumných pracovníků z Centra společnosti Microsoft pro ochranu před škodlivým softwarem, který 24 hodin denně reaguje na nejnovější malwarové hrozby.  

## <a name="windows-defender-settings"></a>Nastavení programu Windows Defender
Nastavení Windows Defenderu umožňují nastavení, které vám pomůžou chránit váš počítač před škodlivým softwarem. Správce může pro vás spravovat některá nastavení Windows Defenderu. Můžete spravovat ostatní pomocí nastavení Windows Defenderu. Doporučujeme povolit nastavení Windows Defenderu, abyste chránili počítač a data.

Pokud chcete zobrazit nastavení Windows Defenderu, `Windows Defender` vyhledejte ho v počítači. Otevřete **program Windows Defender** a vyberte **Nastavení**. Mezi nastavení Windows Defenderu patří:
- **Ochrana v reálném čase** – vyhledání a zastavení malwaru v počítači, který je nainstalován nebo spuštěn.
- **Cloudová ochrana** – Windows Defender posílá Microsoftu informace o potenciálních bezpečnostních hrozbách.
- **Automatické odesílání vzorků** – umožní programu Windows Defender odeslat ukázek podezřelých souborů do Microsoftu, aby se zlepšila detekce malwaru.
- **Vyloučení** – můžete vyloučit konkrétní soubory, složky, přípony souborů nebo procesy z kontroly v programu Windows Defender.
- **Rozšířené oznámení** – povolí oznámení, která informují o stavu počítače. I **když vám** přijdete o kritická oznámení.
- **Windows Defender Offline** – Windows Defender můžete spustit offline, aby se mohl najít a odebrat škodlivý software. Tato kontrola restartuje počítač a bude trvat asi 15 minut.

### <a name="see-also"></a>Viz také  
 [Endpoint Protection nejčastějších dotazech klienta](endpoint-protection-client-faq.md)   
 [Řešení potíží s programem Windows Defender nebo klientem Endpoint Protection](troubleshoot-endpoint-client.md)
