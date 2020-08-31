---
title: 'Zastaralé funkce:'
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích, které Configuration Manager už nepodporují.
ms.date: 08/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: aca9dc5c2ff2d88155ab19656f391cf87a4e977f
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068085"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Odebrané a zastaralé funkce pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Tento článek obsahuje seznam funkcí, které jsou zastaralé nebo odebrané z podpory pro Configuration Manager. Zastaralé funkce budou v budoucí aktualizaci odebrány. Tyto budoucí změny můžou ovlivnit použití Configuration Manager.  

Tyto informace se mohou v budoucích verzích změnit. Nemusí obsahovat všechny zastaralé funkce Configuration Manager.

## <a name="deprecated-features"></a>Zastaralé funkce:

Následující funkce jsou zastaralé. Můžete je dál používat teď, ale Microsoft plánuje ukončit podporu v budoucnu.

|Funkce|Zastarání poprvé oznámeno|Podpora &nbsp; odebrána|
|-----------|---|--------------|
|Zeměpisné zobrazení v uzlu **hierarchie lokality** v pracovním prostoru **monitorování** v konzole nástroje Configuration Manager.<!--8116777-->|Srpen 2020|Bude doplněno|
|Implementace pro sdílení obsahu z Azure se změnila. Použijte bránu pro správu cloudu s podporou obsahu. V budoucnu nebudete moci vytvořit tradiční distribuční bod cloudu.|Únor 2019|TBD –<sup>[Poznámka 1](#bkmk_note1)</sup>|
|Nasazení klasické služby do Azure pro bránu pro správu cloudu a distribuční bod cloudu. Další informace najdete v tématu [plánování pro CMG](../../../clients/manage/cmg/plan-cloud-management-gateway.md#azure-resource-manager).|Listopad 2018|TBD –<sup>[Poznámka 1](#bkmk_note1)</sup>|

### <a name="note-1-support-removed-tbd"></a><a name="bkmk_note1"></a> Poznámka 1: byla odebrána podpora – TBD

Konkrétní časový rámec má být stanoven (TBD). Microsoft doporučuje, abyste změnili na nový proces nebo funkci, ale můžete dál používat zastaralý proces nebo funkci v blízké budoucnosti.

## <a name="unsupported-and-removed-features"></a>Nepodporované a odebrané funkce

Následující funkce již nejsou podporovány. V některých případech už nejsou v produktu.

|Funkce|Zastarání poprvé oznámeno|Podpora &nbsp; odebrána|  
|-----------|---|--------------|  
| Možnost Analytics pro stolní počítače, která **zobrazí poslední data** pro registraci zařízení a aktualizace zabezpečení.<!-- 7080949 --> Další informace najdete v tématu [latence dat](../../../../desktop-analytics/troubleshooting.md#data-latency).|Květen 2020|Červenec 2020|
| Integrace Windows Analytics a Upgrade Readiness. Další informace najdete v [článku KB 4521815: vyřazení služby Windows Analytics na 31. ledna 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement). | 14. října 2019 | 31. ledna 2020 |
| Vyhodnocení ověření stavu zařízení pro zásady dodržování předpisů podmíněného přístupu <!--1235616 aka 3608202--> Další informace najdete v tématu [co se stalo s hybridní MDM](../../../../mdm/understand/what-happened-to-hybrid.md).| 3. července 2019 | Verze 1910 |
| Aplikace Configuration Manager Portál společnosti | 21. května 2019 | Verze 1910 |
| Katalog aplikací, včetně obou rolí systému lokality: bod webu Katalog aplikací a bod webové služby. Další informace najdete v tématu [Odebrání katalogu aplikací](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat). | 21. května 2019 | Verze 1910 |
|Ověřování založené na certifikátech s nastavením Windows Hello pro firmy v Configuration Manager<br>Další informace najdete v tématu [nastavení Windows Hello pro firmy](../../../../protect/deploy-use/windows-hello-for-business-settings.md).|Prosinec 2017|Verze 1910|
|System Center Endpoint Protection pro Mac a Linux<br>Další informace najdete v [příspěvku blogu konec podpory](https://techcommunity.microsoft.com/t5/configuration-manager-blog/end-of-support-for-scep-for-mac-and-scep-for-linux-on-december/ba-p/286257).|Říjen 2018|31. prosince 2018|
|Místní podmíněný přístup<br>Další informace najdete v tématu [co se stalo s hybridní MDM](../../../../mdm/understand/what-happened-to-hybrid.md).|30. ledna 2019|Od 1. září 2019|
|Hybridní Správa mobilních zařízení (MDM)<br>Další informace najdete v tématu [co se stalo s hybridní MDM](../../../../mdm/understand/what-happened-to-hybrid.md).<br><br>Od verze 1902 Intune, která se očekává na konci února 2019, noví zákazníci nemůžou vytvořit nové hybridní připojení.<!--Intune feature 2683117-->|14. srpna 2018|Od 1. září 2019|
|Rozšíření SCAP (Security Content Automation Protocol). <!--3607889--><br>Předchozí certifikovaná verze je stále k dispozici na [webu služby Stažení softwaru](https://www.microsoft.com/download/details.aspx?id=48741).|Září 2018|Verze 1810|
|**Uživatelské prostředí Silverlight** pro bod webu Katalog aplikací už není podporované. Uživatelé by měli používat nové centrum softwaru. Další informace najdete v tématu [Konfigurace centra softwaru](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex).<!--1358309-->|11. srpna 2017| Verze 1806|
|Předchozí verze centra softwaru.<br><br>Další informace o novém centru softwaru najdete v tématu [plánování a konfigurace správy aplikací](../../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_userex).|13. prosince 2016|Verze 1802|
|Správa virtuálních pevných disků (VHD) pomocí Configuration Manager. <br><br>Toto vyřazení zahrnuje odebrání možností pro vytvoření nového virtuálního pevného disku nebo správu VHD pomocí pořadí úkolů a odebrání uzlu virtuálních pevných disků z konzoly Configuration Manager. <br><br>Existující virtuální pevné disky se neodstraňují, ale už nejsou dostupné v konzole Configuration Manager.  |6. ledna 2017 |Verze 1710|
|Pořadí úloh: <br /> – Převést disk na dynamický <br /> – Instalace nástrojů pro nasazení |18. listopadu 2016|Verze 1710|
|Nástroj pro vyhodnocení upgradu<br><br>Nástroj pro vyhodnocení upgradu závisí na Configuration Manager a sadě Application Compatibility Toolkit (ACT) 6. x. Konečná verze ACT byla expedována ve Windows 10 v1511 ADK. Neexistují žádné další aktualizace, které by FUNGOVALy, podpora nástroje pro vyhodnocení upgradu je zastavená. Oznámení o zastarání se přidalo na [stránku pro stahování pro UAT](https://www.microsoft.com/software-download/windows10) 12. září 2016. | 12. září 2016  | 11. července 2017 |
|Body aktualizace softwaru s clusterem služby Vyrovnávání zatížení sítě (NLB) | 27. února 2016 | Verze 1702 |
|Pořadí úloh: <br /> - OSDPreserveDriveLetter  <br /><br /> Při nasazení operačního systému ve výchozím nastavení instalační program systému Windows nyní určuje nejvhodnější písmeno jednotky, které se má použít (obvykle C:). Pokud chcete určit jinou jednotku, kterou chcete použít, můžete změnit umístění v kroku pořadí úkolů použít operační systém. V části **Vyberte umístění, kde chcete použít toto nastavení operačního systému** . Vyberte **konkrétní písmeno logické jednotky** a zvolte jednotku, kterou chcete použít. |20. června 2016 |Verze 1606 |
|Architektura NAP (Network Access Protection) – jak se nachází v nástroji System Center 2012 Configuration Manager|10. července 2015|Verze 1511|  
|Vzdálená správa – jak se nachází na portálu System Center 2012 Configuration Manager|16. října 2015|Verze 1511|

### <a name="features-removed-in-version-1511"></a>Funkce odebrané ve verzi 1511

Následující části obsahují další podrobnosti o funkcích odebraných pomocí verze 1511:

#### <a name="out-of-band-management"></a><a name="bkmk_amt"></a> Vzdálená správa  

Při Configuration Manager byla odebrána nativní podpora pro počítače na bázi AMT z konzoly Configuration Manager.  

- Počítače na bázi AMT zůstanou plně spravované, pokud používáte [doplněk Intel SCS pro Configuration Manager](https://www.intel.com/content/www/us/en/software/setup-configuration-software.html). Doplněk poskytuje přístup k nejnovějším funkcím pro správu AMT při odebrání zavedených omezení, dokud by tyto změny nemohly začlenit Configuration Manager.  

- Vzdálená správa v System Center 2012 Configuration Manager není touto změnou ovlivněná.  

#### <a name="network-access-protection"></a><a name="bkmk_nap"></a> Ochrana přístupu k síti

Configuration Manager odebrala podporu pro NAP (Network Access Protection). Tato funkce se v systému Windows Server 2012 R2 nepoužívá a je odebrána z Windows 10.  

Alternativy ochrany síťového přístupu najdete v části *Deprecated functionality* (Zastaralé funkce) v článku [Network Policy and Access Services Overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831683(v=ws.11)) (Přehled služeb síťových zásad a přístupu).

## <a name="see-also"></a>Viz také

- [Odebrané a zastaralé](removed-and-deprecated.md)
- [Životní cyklus podpora Microsoftu](https://support.microsoft.com/lifecycle)
- [Podpora pro aktuální verze větví Configuration Manager](../../../servers/manage/current-branch-versions-supported.md)