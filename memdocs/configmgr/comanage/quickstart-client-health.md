---
title: Stav klienta se spolusprávou
titleSuffix: Configuration Manager
description: Udržujte si přehled o Configuration Manager stav klienta z Intune na Azure Portal
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11fbeaf76737a832afca7351e8587e0d9c4bacac
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81711193"
---
# <a name="client-health-with-co-management"></a>Stav klienta se spolusprávou

Stav vaší sítě je přímo připojený ke stavu zařízení, která se přesunují i z něj. Intune může komunikovat s poškozeným klientem, i když není ve vaší síti. Spoluspráva vám umožní kombinovat tuto funkci s možností Configuration Manager nahlásit zpět 98% známých zdravých klientů. Pak můžete detekovat, hodnotit a poskytovat viditelnost napříč všemi klienty v reálném čase. Intune také přidává podporu potřebnou pro upgrady dodržování předpisů ve všech připojených klientech.

V následujícím videu by měl vedoucí program Rob York a marketingový manažer pro produkty Ainley diskutovat a ukázkový stav klientů pomocí spolusprávy:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Výhody

Hodnocení stavu klienta je nejvyšší priorita. System Center 2012 Configuration Manager přidal **CCMeval**. Tento nástroj je externě pro klienta Configuration Manager. Poskytuje monitorování stavu klienta a automatickou nápravu. Toto generování sestav ale spoléhá na zařízení, které je fyzicky nebo prakticky ve vaší interní síti. Spoluspráva pomáhá vyřešit tento problém.

Díky spolusprávě může Intune ohlásit stav klienta. Poskytuje informace o časovém razítku pro platnost dat. Tyto informace vám sdělí, jestli jsou zařízení v pořádku, schopná se připojit, může nainstalovat aplikace nebo aktualizovat na požadované sestavení operačního systému. 

Podrobný přehled této funkce najdete v tomto videu od [novinky v Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) relace na adrese Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Když Configuration Manager poskytne stav zařízení, který klient nainstaluje, ale ne, Intune může poskytnout další informace, aniž by bylo nutné se připojit ke klientovi. Informace o stavu zařízení v Intune se snadno chápou. Pokud je stav něco jiného než **v pořádku**, poskytne doporučení a další kroky k jeho řešení a opravě.

> [!Note]  
> Následující výhody jsou plánovány pro budoucí verzi:
> - Configuration Manager budou do CCMeval zahrnovat další funkce.  
> - Bude snazší identifikovat potenciálně poškozené počítače v Configuration Manager i Intune.  
> - Data o stavu klienta můžete seskupit do Intune.  



## <a name="value-proposition"></a>Pozice hodnoty

Díky této funkci teď máte v Intune externí zdroj dat. Umožňuje určit další kroky při řešení potíží s rozsáhlými problémy klientů. Nyní není nutné vytvářet další sestavy ani používat jiné nástroje pro vrácení zpět klientských dat.

Pokud máte v pořádku klienty, jste snadno aktualizovali dodržování předpisů pro opravy. Lepší požadavky na opravy znamenají lepší zabezpečení.



## <a name="configure"></a>Konfigurace

Pokud chcete začít s touto funkcí, použijte následující postup:

- Aktualizace zařízení na Windows 10 verze 1709 nebo novější  

- [Povolení spolusprávy](how-to-enable.md)  
    - Nemusíte přepínat žádné úlohy do Intune.  

- Aktualizace Configuration Manager lokality a klientů na *verzi 1806* nebo novější  


### <a name="review-configuration-manager-client-health-in-intune"></a>Kontrola stavu klienta Configuration Manager v Intune

1. Přihlaste se k [Azure Portal](https://portal.azure.com/).  

2. Vyberte **všechny služby** > **Intune**. Intune se nachází v části **Monitorování a správa**.  

3. Po otevření podokna **Microsoft Intune** můžete v nabídce v části **pomoc a podpora**přejít na stránku **Poradce při potížích** .  

4. Pomocí možnosti **Vybrat uživatele** Najděte konkrétní zařízení v seznamu **zařízení** a vyberte ho a otevřete stránku zařízení.  

5. Informace o spolusprávě se zobrazí v dolní části stránky zařízení. Tyto informace obsahují následující pole pro stav klienta:  
    - **Configuration Manager stav agenta**  
    - **Poslední Configuration Manager – vrácení agenta v čase**  

> [!Tip]  
> Zařízení zaregistrovaná v Intune se připojují ke cloudové službě třikrát denně, přibližně každých 8 hodin. 
