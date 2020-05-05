---
title: Možnosti ve verzi Technical Preview 1512
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1512.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f52d6956cf860de8e45ac4e532500d32bcf077ba
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074499"
---
# <a name="capabilities-in-technical-preview-1512-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1512 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1512. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview. Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.  

 V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.  

##  <a name="device-health-attestation"></a><a name="bkmk_devicehealth"></a>Ověření stavu zařízení  
 Od verze Technical Preview 1512 mohou správci zobrazit stav Windows 10 Ověření stavu zařízení v konzole Configuration Manager.  Tato funkce je k dispozici pro Configuration Manager a Configuration Manager s Microsoft Intune. Ověření stavu zařízení umožňuje správcům zajistit, že klientské počítače mají důvěryhodné konfigurace systému BIOS, čipu TPM a spouštěcího softwaru. Aby bylo možné podporovat ověření stavu zařízení, musí být na klientských zařízeních spuštěná Win10 s povoleným čipem TPM 2. Funkce ověření stavu zařízení zobrazí počet zařízení povolených pro každou z následujících možností:  

-   Antimalware s raným spuštěním  

-   BitLocker  

-   Zabezpečené spouštění  

-   Integrita kódu  

V konzole se zobrazí také nejčastější chybějící nastavení ověření stavu s počtem zařízení.  

Pokud si chcete prohlédnout zobrazení ověření stavu zařízení, v konzole Configuration Manager přejděte do pracovního prostoru **monitorování** , klikněte na uzel **zabezpečení** a pak klikněte na **ověření stavu**.  

##  <a name="in-console-monitoring-for-terms-and-conditions"></a><a name="bkmk_viewterms"></a>Monitorování podmínek a ujednání v konzole  
Od verze Technical Preview 1512 se při integraci Configuration Manager s Microsoft Intune můžete pomocí konzoly pro Configuration Manager zobrazit, kteří uživatelé přijali podmínky a ujednání nakonfigurované vaším IT oddělením a kteří uživatelé ne.  

**Zobrazení souhrnných informací:**  

-   V konzole Configuration Manager přejít na **monitorování** > **Přehled** > **nasazení** a vyberte nasazení podmínek a ujednání, které chcete zobrazit.  

**Zobrazení podrobných informací:**  

1.  V konzole Configuration Manager přejít na **prostředky a kompatibilita** > **Přehled** > **Nastavení** > dodržování předpisů**podmínky a ujednání**a potom vyberte podmínky a ujednání, které chcete zobrazit.  

2.  V dolní části konzoly vyberte kartu **nasazení** , vyberte nasazení a klikněte na **Zobrazit stav.**  

##  <a name="improvements-to-endpoint-protection-policy-settings"></a><a name="bkmk_EPpolicy"></a>Vylepšení nastavení zásad Endpoint Protection  
Ve verzi 1512 Technical Preview jsme do Endpoint Protection antimalwarových zásad přidali Tato nová nastavení:  

-   Ochrana v reálném čase: **blokování potenciálně nežádoucích aplikací při stažení a před instalací**  

    -   Potenciálně nežádoucí aplikace (PUA) je klasifikace hrozby na základě pověsti a identifikace řízené výzkumem. Nejčastěji je to software instalující nežádoucí aplikace nebo jeho balíčky aplikací.  

    -   Nastavení zásad ochrany je ve výchozím nastavení povolené (výchozí nastavení je "Ano"). Když je toto nastavení povolené, blokuje PUA při stažení a v době instalace. Můžete ale vyloučit konkrétní soubory nebo složky, které budou vyhovovat konkrétním potřebám vašeho prostředí.  

-   Nastavení prohledávání: **kontrolovat namapované síťové jednotky při spuštění úplného prohledávání**  

    -   Toto nastavení poskytuje správcům větší členitost, aby umožnila prohledávání síťových souborů na vyžádání bez rizika, že při plánovaném úplném prohledávání vždycky kontroluje mapované síťové jednotky.  

    -   Aby bylo toto nastavení k dispozici pro konfiguraci, musí být nejprve povoleno nastavení **Kontrola síťových souborů** (Ano).  

    -   Ve výchozím nastavení je toto nastavení "ne", což znamená, že úplné prohledávání nebude mít přístup k mapovaným síťovým jednotkám.  

-   Nastavení automatického odesílání ukázkových souborů:  

     Antimalwarový stroj může vyžadovat, aby se Microsoftu odeslaly ukázky souborů k další analýze. Ve výchozím nastavení se před odesláním takových ukázek vždycky dotáže. Správci teď můžou spravovat následující nastavení pro konfiguraci tohoto chování:  

    -   Pokročilé: **Povolit automatické odesílání ukázkových souborů, které pomůže Microsoftu určit, jestli jsou některé zjištěné položky škodlivé**: Pokud chcete povolit automatické odesílání ukázkových souborů, změňte toto nastavení na Ano. Ve výchozím nastavení je toto nastavení "ne", což znamená, že automatické odesílání ukázkových souborů je zakázané a uživatelé budou před odesláním ukázek vyzváni.   (Toto nastavení bylo poprvé zavedeno v produktu System Center 2012 R2 Configuration Manager SP1)  

    -   Upřesnit: **umožňuje uživatelům změnit nastavení automatického odesílání ukázkových souborů**: Toto nastavení určuje, jestli uživatel s právy místního správce v zařízení může změnit nastavení automatického odesílání ukázkových souborů v klientském rozhraní. Ve výchozím nastavení je toto nastavení "ne", což znamená, že nastavení lze změnit pouze v rámci konzoly Configuration Manager a místní správci v zařízení nemůžou tuto konfiguraci změnit.  

         Následující příklad ukazuje nastavení programu Windows Defender ve Windows 10 nastavené správcem jako povolené a uživatel ho nemůže změnit:  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    Kromě toho je vylepšeno nastavení **vyloučit soubory a složky** v antimalwarových zásadách služby Endpoint Protection v části "nastavení vyloučení", což umožňuje vyloučit zařízení. Například teď můžete zadat následující vyloučení: **\device\mvfs** (pro systém souborů MVFS). Tato zásada neověřuje cestu k zařízení. Zásady ochrany koncových bodů se poskytují antimalwarovým modulům v klientovi, který musí být schopný interpretovat řetězec zařízení.  

**Předpoklady použití zásad Endpoint Protection:**  

Než budete moct použít Endpoint Protection zásady, musíte nainstalovat a spravovat klienta Endpoint Protection pomocí Endpoint Protectionho nastavení klienta. To se provádí pomocí klienta System Center Endpoint Protection pro Windows 7, Windows 8, Windows 8.1 nebo spravovaného Windows Defenderu pro Windows 10. Viz [Endpoint Protection](../../protect/deploy-use/endpoint-protection.md).  
