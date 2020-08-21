---
title: Nejčastější dotazy k produktu a licencování
titleSuffix: Configuration Manager
description: Vyhledejte odpovědi na nejčastější dotazy k produktu a licenci pro Configuration Manager.
ms.date: 07/07/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf69dfd73472cb252d2d821dd8e5fb5eb5a6302f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695762"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Nejčastější dotazy týkající se Configuration Manager větví a licencování

*Platí pro: Configuration Manager (Current Branch) & System Center Configuration Manager (dlouhodobá údržba Branch)*

Tato Nejčastější dotazy řeší běžné otázky k licencování týkající se Configuration Manager aktuální větve a verze LTSB (Long-Term Servicing Branch), které jsou k dispozici v rámci multilicenčních programů společnosti Microsoft. Tento článek slouží k informativním účelům. Nenahrazuje ani nenahrazuje žádnou dokumentaci zahrnující Configuration Manager licencování. Další informace najdete v tématu věnovaném [podmínkám produktu](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). Podmínky produktu popisují podmínky použití pro všechny produkty společnosti Microsoft v rámci multilicenčních produktů.

### <a name="whats-current-branch"></a><a name="bkmk_cb"></a> Co je aktuální větev?

Aktuální větev je sestavení Configuration Manager připravené pro produkční prostředí, které poskytuje aktivní model údržby. Tento model údržby se podobá prostředí s Windows 10. Tento přístup podporuje zákazníky, kteří přecházejí do cloudové tempo a chtějí rychleji inovovat. V rámci aktuálního modelu údržby bran budete nadále dostávat nové funkce a funkce. Z tohoto důvodu můžou nainstalovat a používat aktuální větev Configuration Manager jenom zákazníci s aktivním softwarem Software Assurance na Configuration Manager licencích nebo s ekvivalentními právy k předplatnému.

### <a name="whats-the-long-term-servicing-branch-ltsb"></a><a name="bkmk_ltsb"></a> Co je to LTSB (Long-Term Servicing Branch)?  

LTSB je sestavení Configuration Manager připravené pro produkční prostředí. Je určená pro zákazníky, kteří umožňují vypršení platnosti práva Software Assurance nebo ekvivalentní předplatné. Ve srovnání s aktuální větví má LTSB [omezenou funkčnost](introduction-to-the-ltsb.md#features-that-arent-available). Zákazníci, kteří povolí vypršení platnosti práva Software Assurance nebo ekvivalentní předplatné, musí odinstalovat aktuální větev Configuration Manager. Zákazníci, kteří mají Trvalá licenční práva k Configuration Manager, mohou nainstalovat a používat LTSB sestavení Configuration Manager verze, která je aktuální v době vypršení platnosti.

### <a name="what-do-the-acronyms-sa-and-lsa-mean-in-regard-to-configuration-manager"></a><a name="bkmk_licensing-acronyms"></a> Co akronymy *SA* a *L&SA* znamenají v souvislosti s Configuration Manager?

**Program Software Assurance** (SA) i **License and Software Assurance** (&SA) jsou licenční možnosti, které udělují práva k používání Configuration Manager. SA je možnost pro zákazníka, který obnovuje pokrytí SA z předchozí smlouvy. L&SA je možnost pro zákazníky, kteří kupují novou licenci a pokrytí SA.

- **Software Assurance (SA)**: aby zákazníci mohli nainstalovat a používat možnost aktuální větve Configuration Manager, musí mít k dispozici aktivní SA pro licence Configuration Manager nebo ekvivalentní práva k předplatnému.

  I když je přidružení zabezpečení pro některé produkty Microsoftu volitelné, jediný způsob, jak získat práva k použití Configuration Manager aktuální větvi, je SA *nebo ekvivalentní práva k předplatnému*. Další informace najdete v tématu [Nejčastější dotazy k programu Software Assurance](https://www.microsoft.com/licensing/licensing-programs/FAQ-Software-Assurance.aspx).

- **Microsoft License and Software Assurance (L&SA)**: zákazníci, kteří kupují nové licence pro Configuration Manager musí získat L&SA (licence a pokrytí SA).

  - SA uděluje práva k používání aktuální větve.

  - Pokud vaše SA vyprší a stále máte licenci pro Configuration Manager, nebudete už moct používat aktuální větev. Další informace najdete v nejčastějších dotazech, [Pokud platnost svého přidružení zabezpečení vyprší a jsem L&SA, co můžu získat?](#bkmk_sa-expires)

Další informace o nabídkách licencí najdete v tématu [způsoby nákupu](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs) a [licencování podmínek produktu](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64).  

### <a name="what-are-equivalent-subscriptions"></a><a name="bkmk_equiv-sub"></a> Co jsou *ekvivalentní předplatné*?

Ekvivalentní odběry odkazují na programy, jako je [Enterprise mobility + Security](https://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) nebo [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise). Můžou to být i další, ale tyto programy jsou nejběžnější. Podmínky produktu multilicenčního programu společnosti Microsoft se vztahují na tyto programy jako licence na licence pro správu s ekvivalentními oprávněními.

Configuration Manager je zahrnutý v následujících plánech:

- Licence k předplatnému uživatele Intune (USL)
- EMS E3
- EMS E5
- Microsoft 365 E3
- Microsoft 365 E5
- Microsoft 365 F3 (dříve Microsoft 365 F1)

<!-- Sources:
https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans
https://www.microsoft.com/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing
-->

> [!IMPORTANT]
> Configuration Manager není součástí plánu [Microsoft 365 Business](https://www.microsoft.com/microsoft-365/business) .

### <a name="what-changes-with-licensing-for-co-management-in-microsoft-endpoint-manager"></a><a name="bkmk_mem"></a> Jaké změny mají licencování pro spolusprávu ve službě Microsoft Endpoint Manager?

<!-- 7202432 -->

Licence spolusprávy umožňuje Configuration Manager zákazníkům se Software Assurance získat práva pro správu počítačů v Intune, aniž by museli kupovat a přiřazovat jednotlivé licence Intune uživatelům. Tato licence usnadňuje správu zařízení s Windows pomocí služby Microsoft Endpoint Manager.

- Zařízení, která jsou už spravovaná pomocí Configuration Manager kterou zaregistrujete do Intune pro spolusprávu, mají skoro stejná práva jako samostatný počítač spravovaný pomocí Intune. Pokud na tomto zařízení resetujete Windows, nemůžete ho zřídit pomocí Windows autopilotu. Autopilot vyžaduje úplnou licenci Intune.

- Pokud zařízení s Windows 10 zaregistrujete do Intune jiným způsobem, budete ještě potřebovat úplnou licenci Intune. Pomocí nástroje autopilot můžete například zřídit zařízení nebo uživatel ručně provede samoobslužnou registraci.

- U stávajících zařízení spravovaných Configuration Manager k registraci do Intune pro spolusprávu se škálováním bez zásahu uživatele používá spoluspráva funkci Azure Active Directory (Azure AD) s názvem Windows 10 Autoenrollment. Automatický zápis s spolusprávou vyžaduje licence pro Azure AD Premium (AADP1) i Intune. Od 1. prosince 2019 už nemusíte pro tento scénář přiřazovat jednotlivé licence Intune. Microsoft Endpoint Manager teď zahrnuje licence Intune pro spolusprávu. Samostatný požadavek na licencování AADP1 zůstává pro fungování tohoto scénáře stejný. K dalším scénářům registrace stále potřebujete přiřadit licence Intune.

- Pokud chcete Intune používat ke správě zařízení se systémem iOS, Android nebo macOS, budete potřebovat příslušné předplatné Intune prostřednictvím samostatné licence Intune, Enterprise Mobility + Security (EMS) nebo Microsoft 365.

- Pokud nemáte žádný plán předplatného s Intune, abyste mohli podporovat spolusprávu, musíte si koupit aspoň jednu licenci Intune. Tato licence je určena pro správce, aby mohl aktivovat plán předplatného a získat přístup k centru pro správu služby Microsoft Endpoint Manager.

- Pokud používáte Microsoft 365 integrovanou [základní mobilitu a zabezpečení](https://support.microsoft.com/office/capabilities-of-built-in-mobile-device-management-for-microsoft-365-a1da44e5-7475-4992-be91-9ccec25905b0), nemůžete použít novou licenci spolusprávy pro uživatele, který má také zařízení spravovaná základní mobilitou a zabezpečením. Chcete-li použít licenci spolusprávy pro zařízení spravované uživatelem Configuration Manager, proveďte jednu z následujících akcí:

  - Přiřaďte uživateli úplnou licenci na Intune a spravujte svá zařízení přes Intune.
  - Zruší registraci zařízení ze základní mobility a zabezpečení.

- Licencování, které jste předtím používali pro System Center Configuration Manager, se stále vztahuje na službu Microsoft Endpoint Configuration Manager. Pokud instalujete novou lokalitu, použijte existující kódy Product Key.

|Funkce | Licence pro spolusprávu | Úplná licence Intune |
|---------|---------|---------|
|Registrace Windows 10|Ano (jenom pro existující zařízení spravovaná nástrojem ConfigMgr)|Ano|
|iOS, Android, registrace macOS|Ne|Ano|
|Autopilot|Ne|Ano|
|Správa mobilních aplikací (MAM)|Ne|Ano|
|Podmíněný přístup<br>(vyžaduje se další AADP1.)|Ano|Ano|
|profily zařízení|Ano|Ano|
|Správa aktualizací softwaru|Ano|Ano|
|inventář|Ano|Ano|
|Správa aplikací|Ano|Ano|
|Vzdálená pomoc<br>(Vyžaduje se licence TeamVieweru)|Ano|Ano|
|Desktop Analytics<br>(Vyžaduje se licence předplatného systému Windows|Ano|–|
|Připojení tenanta|Ano|–|
|Analýza koncového bodu|Ano|Ano|

Další informace najdete v následujících článcích:

- [Požadavky společné správy](../../comanage/overview.md#prerequisites)
- [Požadavky na Windows autopilot](/windows/deployment/windows-autopilot/windows-autopilot-requirements)
- [Požadavky na Desktop Analytics](../../desktop-analytics/overview.md#prerequisites)
- [Předpoklady pro připojení tenanta](../../tenant-attach/device-sync-actions.md#prerequisites)
- [Požadavky na licencování služby Endpoint Analytics](../../../analytics/overview.md#licensing-prerequisites)
- [Použití podmíněného přístupu s Intune](../../../intune/protect/conditional-access.md#use-conditional-access-with-intune)
- [Požadavky TeamVieweru](../../../intune/remote-actions/teamviewer-support.md#prerequisites)

### <a name="i-have-enterprise-mobility--security-and-it-expired-what-must-i-do-now"></a><a name="bkmk_ems-expires"></a> Mám Enterprise Mobility + Security a její platnost vypršela, co se teď musí udělat?  

EMS uděluje práva k použití Configuration Manager aktuální větvení a dlouhodobé větvi služby. Po vypršení platnosti těchto práv už nemáte práva k používání žádné větve a musíte ji odinstalovat.  

### <a name="if-my-sa-expires-and-i-had-lsa-what-do-i-get"></a><a name="bkmk_sa-expires"></a> Pokud moje přidružení zabezpečení vyprší, i když jsem&SA, co získám?

Pokud platnost vašeho přidružení zabezpečení vyprší od 1. října 2016, v závislosti na tom, jaký program jste získali L&SA v rámci, byste si měli zachovat trvalou licenci k používání LTSB. Pokud aktuálně používáte aktuální větev, je nutné ji odinstalovat a pak nainstalovat LTSB. Neexistuje žádná podpora pro migraci nebo převod na LTSB z aktuální větve.

Pokud platnost vašeho přidružení zabezpečení vyprší před 1. října 2016 a trvale jste zachovali trvalou licenci k Configuration Manager, pak je k dispozici pouze možnost instalace a používání nástroje System Center 2012 R2 Configuration Manager a dostupných aktualizací Service Pack. Pokud vaše SA vyprší, budete muset odinstalovat aktuální větev a znovu ji nainstalovat. Neexistuje žádná podpora migrace na nebo downgrade z Configuration Manager aktuální větve na předchozí verze Configuration Manager.

Pokud používáte System Center Endpoint Protection a platnost vašeho přidružení zabezpečení vyprší, musíte ji odinstalovat. System Center Endpoint Protection nabízí žádná práva na *licence* a žádná netrvalá práva.<!--506238-->

### <a name="do-i-own-the-current-branch"></a><a name="bkmk_owncb"></a> Mám "vlastní" aktuální větev?

Ne. Máte licenci na používání aktuální větve, když máte aktivní SA. Pokud třeba *SA* vyprší, můžete například prostřednictvím služby *l&SA*použít jenom *L (licence)* , která nezahrnují práva k používání aktuální větve. Pokud vaše L poskytuje trvalá práva, můžete místo aktuální větve použít Configuration Manager LTSB. Pokud vaše přidružení zabezpečení vypršelo před 1. října 2016, můžete také použít System Center 2012 R2 Configuration Manager.

### <a name="can-i-purchase-configuration-manager-standalone-without-sa"></a><a name="bkmk_standalone"></a> Můžu Configuration Manager samostatně koupit bez SA?

Ne. Jediným způsobem, jak získat práva k používání Configuration Manager, je získat licenci pomocí SA nebo přes ekvivalentní předplatné. K dispozici jsou vývojářské programy, jako je například MSDN, kde se Configuration Manager nabízet pro účely vývoje a testování, ale ne produkční využití.

### <a name="does-a-non-production-environment-for-testing-or-development-require-an-explicit-license"></a><a name="bkmk_lab"></a> Vyžaduje prostředí, které není v provozu, pro testování nebo vývoj určitou explicitní licenci?

<!-- SCCMDocs#1848 -->

- Pokud používáte stejný software pro vytváření bran jako v produkčním prostředí, budete potřebovat explicitní licenci. Pokud chcete zjistit, jestli vaše konkrétní licenční smlouva pokrývá víc instancí ve více prostředích, obraťte se na tým vašeho účtu.

- Některé vývojářské programy, jako je MSDN, nabízejí produkty, jako je Configuration Manager pro vývoj a testování, ale ne pro produkční použití.

- V případě dočasného prostředí můžete [zkušební verzi](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) použít po dobu 180 dnů.

- V testovacím prostředí můžete použít [větev Technical Preview](../get-started/technical-preview.md). Technical Preview má stejné funkce jako aktuální větev, ale má určitá omezení z hlediska škálování a podporovaných platforem.

### <a name="do-i-have-rights-to-install-any-update-in-the-configuration-manager-console"></a><a name="bkmk_update-rights"></a> Mám v konzole pro Configuration Manager práva k instalaci jakékoli aktualizace?

Pokud máte aktivní *SA*, máte oprávnění.

Pokud nemáte aktivní přidružení zabezpečení (SA), odinstalujte aktuální větev a pak nainstalujte LTSB Configuration Manager. LTSB nepřijímá aktualizace pro přírůstkové verze Configuration Manager, ale přijímá aktualizace zabezpečení na základě životního cyklu podpory.

### <a name="i-have-purchased-ems-or-microsoft-365-through-a-cloud-solution-provider-csp-do-i-have-rights-to-use-configuration-manager"></a><a name="bkmk_csp"></a> Koupil (a) jsem EMS nebo Microsoft 365 prostřednictvím poskytovatele Cloud Solution Provider (CSP), mám oprávnění používat Configuration Manager?

Ano, máte práva k používání Configuration Manager ke správě klientů, na které se vztahuje licence EMS. Nejdřív Stáhněte a nainstalujte [zkušební software](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection). Potom kontaktujte podpora Microsoftu a Získejte licenční klíč.<!--issue472--> Když budete mluvit s podpora Microsoftu, požádejte je, aby odkazovali na interní článek s ID 4033838.<!-- SCCMDocs issue 493 -->

### <a name="is-my-subscription-end-date-the-same-as-an-sa-expiration-date"></a><a name="bkmk_expiration-date"></a> Má moje předplatné datum ukončení stejné jako datum vypršení platnosti SA?

Pokud je *přidružení zabezpečení (SA* ) nebo předplatné aktivní, máte práva k používání Configuration Manager aktuální větvi. Aktivní předplatné je ekvivalentem aktivního *SA*, ale netrvalá *"L" (licence)*. Po skončení předplatného odinstalujte aktuální větev. V tuto chvíli nemáte práva k používání LTSB.  

### <a name="what-are-the-use-rights-associated-with-the-sql-technology-provided-with-configuration-manager"></a><a name="bkmk_sql"></a> Jaká jsou práva k používání přidružená k technologii SQL dodávané s Configuration Manager?

Configuration Manager zahrnuje technologii SQL Server. Licenční podmínky Microsoftu pro tento produkt umožňují používat technologii SQL Server jenom pro podporu Configuration Managerch komponent. SQL Server licence pro klientský přístup nejsou pro toto použití požadovány.

Schválená práva k používání funkcí SQL s Configuration Manager zahrnují:

- Role databáze webu
- Windows Server Update Services (WSUS) pro roli bodu aktualizace softwaru
- SQL Server Reporting Services (SSRS) pro roli bodu hlášení
- Role bodu služby datového skladu
- Repliky databáze pro role bodu správy

Licence SQL Server, která je součástí Configuration Manager, podporuje každou instanci SQL Server, kterou nainstalujete pro hostování databáze pro Configuration Manager. Při použití této licence se ale v tomto SQL Server můžou spouštět jenom databáze pro Configuration Manager v předchozím seznamu. Pokud se SQL Server databáze pro další produkty společnosti Microsoft nebo třetí strany, musíte mít samostatnou licenci na tuto instanci SQL Server.
 <!-- sms500967 -->

### <a name="does-on-premises-mobile-device-management-mdm-require-an-intune-subscription"></a><a name="bkmk_opmdm"></a> Vyžaduje místní správa mobilních zařízení (MDM) předplatné Intune?

Pokud chcete začít používat místní správu mobilních zařízení (MDM) ve verzích 1806 a starší, potřebujete předplatné Microsoft Intune. Předplatné se vyžaduje jenom ke sledování licencí zařízení a nepoužívá se ke správě nebo ukládání informací o správě zařízení. Všechna data správy se ukládají ve vaší organizaci pomocí místní infrastruktury Configuration Manager.  

Počínaje verzí 1810 se připojení Intune už nevyžaduje pro nová místní nasazení MDM.<!--3607730, fka 1359124--> Vaše organizace pořád vyžaduje licence Intune, aby mohli tuto funkci používat. Další informace najdete v příspěvku na [blogu podpory Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).