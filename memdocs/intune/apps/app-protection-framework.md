---
title: Architektura ochrany dat pomocí zásad APP (App Protection Policies)
titleSuffix: Microsoft Intune
description: Přečtěte si, jak zásady ochrany aplikací (aplikace) zajišťují, že data organizace zůstávají v bezpečí nebo jsou obsažená ve spravované aplikaci bez ohledu na to, jestli je zařízení zaregistrované.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/19/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91683280a2e48d82fd145bf19228c33b432b6b49
ms.sourcegitcommit: a1da477542fb0ff360685d6eb58ef43e37ac3950
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/26/2020
ms.locfileid: "83853566"
---
# <a name="data-protection-framework-using-app-protection-policies"></a>Architektura ochrany dat pomocí zásad APP (App Protection Policies) 

Protože víc organizací implementuje strategie mobilních zařízení pro přístup k pracovním nebo školním datům, je ochrana před únikem dat zcela nejdůležitější. Řešení správy mobilních aplikací v Intune pro ochranu před únikem dat je zásady ochrany aplikací (aplikace). APLIKACE jsou pravidla, která zajistí, aby data organizace zůstala bezpečná nebo obsažená ve spravované aplikaci bez ohledu na to, jestli je zařízení zaregistrované. Další informace najdete v tématu [Přehled zásad ochrany aplikací](app-protection-policy.md).

Když konfigurujete zásady ochrany aplikací, počet různých nastavení a možností umožňuje organizacím přizpůsobit ochranu jejich konkrétním potřebám. Z důvodu této flexibility nemusí být zřejmé, že je nutné provést permutaci nastavení zásad pro implementaci kompletního scénáře. Za účelem pomáhat organizacím upřednostnit budoucna koncového bodu klienta, společnost Microsoft zavedla novou taxonomii pro [Konfigurace zabezpečení ve Windows 10](https://aka.ms/secconframework)a Intune využívá podobnou taxonomii pro své rozhraní ochrany dat aplikací pro správu mobilních aplikací.  

Konfigurační rozhraní ochrany dat aplikace je rozdělené do tří různých scénářů konfigurace:

- Úroveň 1 Enterprise Basic Data Protection – Microsoft doporučuje tuto konfiguraci jako minimální konfiguraci ochrany dat pro podnikové zařízení.

- Level 2 Enterprise Enhanced Data Protection – Microsoft doporučuje tuto konfiguraci pro zařízení, kde uživatelé přistupují k citlivým nebo důvěrným informacím. Tato konfigurace platí pro většinu mobilních uživatelů, kteří přistupují k pracovním nebo školním datům. Některé ovládací prvky mohou ovlivnit činnost koncového uživatele.

- Level 3 Enterprise high data Protection – Microsoft doporučuje tuto konfiguraci pro zařízení spuštěná v organizaci s větším nebo výkonnějším bezpečnostním týmem nebo pro konkrétní uživatele nebo skupiny, které mají jednoznačně vysoké riziko (uživatelé, kteří zpracovávají vysoce citlivá data, pokud neoprávněná vyzrazení způsobuje značnou materiální ztrátu v organizaci). Organizace, která bude pravděpodobně cílena prostřednictvím dobře financované a sofistikované nežádoucí osoby, by měla snažíme na tuto konfiguraci.

## <a name="app-data-protection-framework-deployment-methodology"></a>Metodologie nasazení architektury APP data Protection

Stejně jako u jakéhokoli nasazení nového softwaru, funkcí nebo nastavení doporučuje společnost Microsoft investovat v rámci kruhové metodologie pro testování ověřování před nasazením architektury aplikace Data Protection. Definování okruhů nasazení je obecně jednorázová událost (nebo nejméně zřídka), ale měla by tyto skupiny znovu navštívit, aby bylo zajištěno, že pořadí je stále správné.

Společnost Microsoft doporučuje pro architekturu ochrany dat aplikací následující aktualizační přístup k nasazení:

| Aktualizační kanál nasazení  | Tenant  | Týmy posouzení  | Výstup  | Časová osa  |
|--------------------|------------------------|-------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| Kontrola kvality  | Předprodukční tenant  | Vlastníci funkce, zabezpečení, posouzení rizik, soukromí, uživatelské rozhraní  | Ověřování funkčních scénářů, koncept dokumentace  | 0-30 dní  |
| Preview  | Provozní tenant  | Vlastníci mobilních funkcí, UX  | Ověření scénáře koncového uživatele, dokumentace k uživateli  | 7-14 dní, vyúčtování kvality  |
| Produkce  | Provozní tenant  | Vlastníci na mobilní funkce, IT oddělení technické podpory  | –  | 7 dní do několika týdnů, po verzi Preview  |

Jak uvádí výše uvedená tabulka, všechny změny zásad ochrany aplikací by se měly nejdřív provést v předprodukčním prostředí, aby se porozumělo nastavení zásad. Po dokončení testování je možné změny přesunout do produkčního prostředí a použít na podmnožinu produkčních uživatelů, obecně, IT oddělení a dalších příslušných skupin. A nakonec můžete zavedení dokončit pro ostatní uživatele mobilní komunity. Zavedení do produkčního prostředí může trvat delší dobu v závislosti na rozsahu dopadu na změnu. Pokud nedochází k žádnému dopadu na uživatele, změna by se měla rychle vymezit, zatímco pokud změna vznikne vlivem na uživatele, může být potřeba, aby se povedlo zpomalit, protože je potřeba sdělit změny naplnění uživatele.

Při testování změn v aplikaci mějte na paměti [časování doručování](app-protection-policy-delivery.md). Stav doručování aplikace pro daného uživatele může být monitorován. Další informace najdete v tématu [jak monitorovat zásady ochrany aplikací](app-protection-policies-monitor.md).

Jednotlivá nastavení aplikací pro každou aplikaci je možné ověřit na zařízeních pomocí Edge a adresy URL *o: Intunehelp*. Další informace najdete v tématech [Kontrola protokolů ochrany klientských aplikací](app-protection-policy-settings-log.md) a [používání hraničních zařízení pro iOS a Android pro přístup k protokolům spravovaných aplikací](manage-microsoft-edge.md#use-edge-for-ios-and-android-to-access-managed-app-logs).

## <a name="app-data-protection-framework-settings"></a>Nastavení architektury aplikace Data Protection

Tato nastavení zásad ochrany aplikací by měla být povolená pro příslušné aplikace a přiřazená všem mobilním uživatelům. Další informace o jednotlivých nastaveních zásad najdete v tématu nastavení [zásad ochrany aplikací pro iOS](app-protection-policy-settings-ios.md) a [nastavení zásad ochrany aplikací pro Android](app-protection-policy-settings-android.md).

Společnost Microsoft doporučuje kontrolu a kategorizaci scénářů používání a následně konfiguraci uživatelů pomocí doporučených pokynů pro danou úroveň. Stejně jako u všech platforem může být potřeba upravit nastavení v odpovídající úrovni v závislosti na potřebách organizace, protože ochrana dat musí vyhodnocovat hrozby, později rizika a dopad na použitelnost.  

### <a name="conditional-access-policies"></a>Zásady podmíněného přístupu
Aby se zajistilo, že pouze aplikace, které podporují zásady ochrany aplikací Azure Active Directory, mají přístup k datům v pracovním nebo školním účtu, jsou vyžadovány zásady podmíněného přístupu Viz **scénář 1: aplikace Office 365 vyžadují schválené aplikace se zásadami ochrany aplikací** v tématu [vyžadování zásad ochrany aplikací pro cloudovou aplikaci přístup pomocí podmíněného přístupu](https://docs.microsoft.com/azure/active-directory/conditional-access/app-protection-based-conditional-access) pro kroky pro implementaci konkrétních zásad.

### <a name="apps-to-include-in-the-app-protection-policies"></a>Aplikace, které se mají zahrnout do zásad ochrany aplikací  

Pro každou zásadu ochrany aplikací by měly být zahrnuté následující základní aplikace Microsoftu:

- Edge
- Excel
- Office
- OneDrive
- OneNote
- Outlook
- PowerPoint
- Microsoft Teams
- Microsoft To-Do
- Word
- Microsoft SharePoint

Zásady by měly zahrnovat další aplikace Microsoftu založené na obchodních potřebách, další veřejné aplikace třetích stran, které mají integrovanou sadu Intune SDK použitou v rámci organizace, a také obchodní aplikace, které mají integrovanou [sadu Intune SDK](../developer/app-sdk.md) (nebo byly zabaleny).

### <a name="level-1-enterprise-basic-data-protection"></a>Úroveň 1 podniková ochrana dat úrovně Basic

Úroveň 1 je minimální konfigurace ochrany dat pro podnikové mobilní zařízení. Tato konfigurace nahrazuje potřebu základních zásad přístupu k zařízením Exchange Online tím, že vyžaduje PIN pro přístup k pracovním nebo školním datům, šifrování pracovních nebo školních účtů a poskytuje možnost selektivně vymazat školní nebo pracovní data. Na rozdíl od zásad přístupu k zařízení Exchange Online platí, že níže uvedená nastavení zásad ochrany aplikací se vztahují na všechny aplikace vybrané v zásadách. tím se zajistí Ochrana přístupu k datům mimo scénáře mobilního zasílání zpráv.

Zásady na úrovni 1 vynutily rozumnou úroveň přístupu k datům a současně minimalizují dopad na uživatele a při vytváření zásad ochrany aplikací v rámci služby Microsoft Endpoint Manager se zrcadlí výchozí nastavení ochrany dat a požadavků na přístup.  

#### <a name="data-protection"></a>Ochrana dat

| Nastavení | Popis nastavení |             Hodnota  |             Platforma        |
|-----------------|--------------------------------------------------------|-----------------------|----------------------------------------|
| Přenos dat |             Zálohovat organizační data do...  |             Povolit  |             iOS/iPadOS, Android        |
| Přenos dat |       Posílání organizačních dat do jiných aplikací  |             Všechny aplikace  |             iOS/iPadOS, Android        |
| Přenos dat |       Příjem dat z jiných aplikací  |             Všechny aplikace  |             iOS/iPadOS, Android        |
| Přenos dat |       Omezit vyjmutí, kopírování a vložení mezi aplikacemi  |             Libovolná aplikace  |             iOS/iPadOS, Android        |
| Přenos dat |       Klávesnice třetích stran  |             Povolit  |             iOS/iPadOS        |
| Přenos dat |       Schválené klávesnice  |             Není požadováno  |             Android        |
| Přenos dat |       Snímek obrazovky a pomocník Google  |             Povolit  |             Android        |
| Šifrování |             Šifrování dat organizace  |             Vyžadovat  |             iOS/iPadOS, Android        |
| Šifrování |       Šifrování dat organizace v zaregistrovaných zařízeních  |             Vyžadovat  |             Android        |
| Funkce  |             Synchronizace aplikace s nativní aplikací kontaktů  |             Povolit  |             iOS/iPadOS, Android        |
| Funkce  |       Tisk organizačních dat  |             Povolit  |             iOS/iPadOS, Android        |
| Funkce  |       Omezení přenosu webového obsahu u jiných aplikací  |             Libovolná aplikace  |             iOS/iPadOS, Android        |
| Funkce  |       Oznámení o datech organizace  |             Povolit  |             iOS/iPadOS, Android        |

#### <a name="access-requirements"></a>Požadavky na přístup 

| Nastavení  | Hodnota  | Platforma  | Poznámky  |
|----------------------------------------------------------------|---------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Připnout pro přístup  | Vyžadovat  | iOS/iPadOS, Android  |   |
| Typ kódu PIN  | Numeric  | iOS/iPadOS, Android  |   |
| Jednoduchý PIN kód  | Povolit  | iOS/iPadOS, Android  |   |
| Vyberte minimální délku PIN kódu.  | 4  | iOS/iPadOS, Android  |   |
| Biometrika místo kódu PIN pro přístup  | Povolit  | iOS/iPadOS, Android  |   |
| Přepsat biometriku místo kódu PIN pro přístup  | Vyžadovat  | iOS/iPadOS, Android  |   |
| Časový limit (minuty aktivity)  | 720  | iOS/iPadOS, Android  |   |
| ID obličeje místo kódu PIN pro přístup  | Povolit  | iOS/iPadOS  |   |
| Resetovat PIN kód po počtu dní  | Ne  | iOS/iPadOS, Android  |   |
| PIN kód aplikace, když je nastavený PIN kód zařízení  | Vyžadovat  | iOS/iPadOS, Android  | Pokud je zařízení zaregistrované v Intune, můžou správci zvážit nastavení "Nepožadováno", pokud vynucuje silný PIN kód zařízení pomocí zásad dodržování předpisů zařízením.  |
| Přihlašovací údaje k pracovnímu nebo školnímu účtu pro přístup  | Není požadováno  | iOS/iPadOS, Android  |   |
| Znovu ověřit požadavky na přístup po (minuty neaktivity)  | 30  | iOS/iPadOS, Android  |   |

#### <a name="conditional-launch"></a>Podmíněné spouštění 

| Nastavení | Popis nastavení |          Hodnota/akce  |          Platforma        | Poznámky |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Podmínky aplikace |       Maximální počet pokusů o zadání PIN kódu  |          5/obnovit PIN kód  |          iOS/iPadOS, Android  |                  |
| Podmínky aplikace |       Období odkladu pro offline režim  |          720/blokovat přístup (minuty)  |          iOS/iPadOS, Android  |                  |
| Podmínky aplikace |       Období odkladu pro offline režim  |          90/vymazat data (dny)  |          iOS/iPadOS, Android  |                  |
| Podmínky zařízení  |       Zařízení s jailbreakem/rootem  |        Není k dispozici/blokovat přístup  |          iOS/iPadOS, Android  |                  |
| Podmínky zařízení  |       Ověření zařízení SafetyNet  |          Základní integrita a certifikovaná zařízení/blokovat přístup  |          Android  |          <p>Toto nastavení konfiguruje ověřování SafetyNet Google na zařízeních koncových uživatelů. Základní integrita ověřuje integritu zařízení. Zařízení s rootem, emulátory, virtuální zařízení a zařízení se znaménkem neoprávněného selhání základní integrity. </p><p> Základní integrita a certifikovaná zařízení ověřují kompatibilitu zařízení se službami Google. Tuto kontrolu můžou předat jenom nezměněná zařízení, která získala certifikace od společnosti Google.</p>  |
| Podmínky zařízení  |       Vyžadovat kontrolu hrozeb u aplikací  |        Není k dispozici/blokovat přístup  |          Android  |          Toto nastavení zajistí, aby byla pro zařízení koncových uživatelů zapnutá kontrola aplikací pro ověřování Google. V případě konfigurace bude koncový uživatel zablokován přístup, dokud nezapnete kontrolu aplikací Google na svém zařízení s Androidem.        |

#### <a name="level-2-enterprise-enhanced-data-protection"></a>Úroveň 2 Enterprise Rozšířená ochrana dat

Úroveň 2 je konfigurace ochrany dat doporučená jako standard pro zařízení, kde uživatelé přistupují k citlivým informacím. Tato zařízení jsou v podnicích v současnosti přirozeného cíle. Tato doporučení nepředpokládají velký personál zkušených specialistů na zabezpečení, a proto by měla být přístupná většině podnikových organizací. Tato konfigurace se rozšíří na konfiguraci na úrovni 1 tím, že omezí scénáře přenosu dat a vyžaduje minimální verzi operačního systému.

Nastavení zásad vyžadované v úrovni 2 zahrnuje všechna nastavení zásad doporučená pro úroveň 1, ale obsahuje jenom ta nastavení, která byla přidaná nebo změněná k implementaci více ovládacích prvků a pokročilejší konfigurace než úroveň 1. I když tato nastavení mohou mít mírně vyšší dopad na uživatele nebo na aplikace, vynutila úroveň ochrany dat lépe úměrná riziku uživatelů s přístupem k citlivým informacím na mobilních zařízeních.

#### <a name="data-protection"></a>Ochrana dat

| Nastavení | Popis nastavení |             Hodnota  |             Platforma        | Poznámky |
|---------------|----------------------------------------------------------|-----------------------------------------------|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Přenos dat |       Zálohovat organizační data do...  |          Blok  |          iOS/iPadOS, Android  |                  |
| Přenos dat |       Posílání organizačních dat do jiných aplikací  |          Aplikace spravované podle zásad  |          iOS/iPadOS, Android  |          <p>S iOS/iPadOS můžou správci nakonfigurovat tuto hodnotu jako "aplikace spravované zásadou", "aplikace spravované zásadou" s funkcí sdílení operačního systému "nebo" aplikace spravované podle zásad s filtrováním Open-in/sdílení ". </p><p>Aplikace spravované podle zásad se sdílením operačního systému jsou dostupné, pokud je zařízení také zaregistrované v Intune. Toto nastavení umožňuje přenos dat do jiných aplikací spravovaných zásadou a také přenos souborů do jiných aplikací spravovaných pomocí Intune. </p><p>Aplikace spravované podle zásad s filtrováním Open-in/sdílení vyfiltrují dialogová okna otevřít v operačním systému nebo sdílet, aby zobrazovala jenom aplikace spravované zásadami. </p><p> Další informace najdete v tématu [nastavení zásad ochrany aplikací pro iOS](app-protection-policy-settings-ios.md).</p> |
| Přenos dat |       Uložení kopií dat org  |          Blok  |          iOS/iPadOS, Android  |                  |
| Přenos dat |       Umožňuje uživatelům ukládat kopie do vybraných služeb.  |          OneDrive pro firmy, SharePoint Online |          iOS/iPadOS, Android  |                  |
| Přenos dat |       Omezit vyjmutí, kopírování a vložení mezi aplikacemi  |          Aplikace s vložením spravované podle zásad  |          iOS/iPadOS, Android  |                  |
| Přenos dat |       Snímek obrazovky a pomocník Google  |          Blok  |          Android  |                  |
| Funkce |       Omezení přenosu webového obsahu u jiných aplikací  |          Microsoft Edge  |          iOS/iPadOS, Android  |                  |
| Funkce |       Oznámení o datech organizace  |          Blokovat organizační data  |          iOS/iPadOS, Android  |          Seznam aplikací, které podporují toto nastavení, najdete v tématu nastavení [zásad ochrany aplikací pro iOS](app-protection-policy-settings-ios.md) a [nastavení zásad ochrany aplikací pro Android](app-protection-policy-settings-android.md).       |

#### <a name="conditional-launch"></a>Podmíněné spouštění

| Nastavení | Popis nastavení |          Hodnota/akce  |          Platforma        | Poznámky |
|--------------------|----------------------------|-----------------------------------------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Podmínky zařízení  |       Minimální verze operačního systému  |          *Formát: Hlavní_verze. podverze. sestavení <br> Příklad: 12.4.6* /Block Access |          iOS/iPadOS        | Microsoft doporučuje nakonfigurovat minimální hlavní verzi iOS tak, aby odpovídala podporovaným verzím iOS pro aplikace Microsoftu.   Aplikace Microsoftu podporují N-1 přístup, kde N je aktuální hlavní verze iOS. V případě hodnot menších verzí a verze sestavení doporučuje společnost Microsoft zajistit, aby byla zařízení v aktuálním stavu s příslušnými aktualizacemi zabezpečení. Seznamte se s [aktualizacemi zabezpečení Apple](https://support.apple.com/en-us/HT201222) pro nejnovější doporučení společnosti Apple. |
| Podmínky zařízení  |       Minimální verze operačního systému  |          *Formát: Hlavní_verze. podverze <br>   Příklad: 5,0* /blokovat přístup   |          Android        | Microsoft doporučuje nakonfigurovat minimální hlavní verzi Androidu tak, aby odpovídala podporovaným verzím Androidu pro aplikace Microsoftu. Výrobci OEM a zařízení, kteří dodržují doporučené požadavky na Android Enterprise, musí podporovat aktuální dodací verzi a jeden upgrade na jedno písmeno.   V současné době Android doporučuje Android 8,0 a novější pro pracovníky znalostní báze.   Nejnovější doporučení pro Android najdete v tématu [Doporučené požadavky pro Android Enterprise](https://www.android.com/enterprise/recommended/requirements/) |
| Podmínky zařízení  |       Minimální verze opravy  |          *Formát: rrrr-mm-dd <br> Příklad: 2020-01-01* /blokovat přístup  |          Android        | Zařízení s Androidem můžou přijímat měsíční opravy zabezpečení, ale tato verze závisí na výrobci OEM nebo nosiči. Organizace musí před implementací tohoto nastavení zajistit, aby nasazená zařízení s Androidem přijímala aktualizace zabezpečení. Nejnovější verze oprav najdete v [bulletinech zabezpečení pro Android](https://source.android.com/security/bulletin/) .  |

#### <a name="level-3-enterprise-high-data-protection"></a>Úroveň 3; podniková ochrana dat – vysoká 

Úroveň 3 je konfigurace ochrany dat doporučená jako standard pro organizace s velkými a sofistikovanými organizacemi zabezpečení nebo pro konkrétní uživatele a skupiny, které budou jedinečně cíleny na nežádoucí osoby. Tyto organizace jsou obvykle zaměřené na dobře financované a sofistikované nežádoucí osoby a jako taková jsou popsaná další omezení a ovládací prvky. Tato konfigurace se rozšíří na konfiguraci ve druhé úrovni tím, že omezí další scénáře přenosu dat, zvýší složitost konfigurace kódu PIN a přidá detekci mobilních hrozeb.  

Nastavení zásad vyžadované v úrovni 3 zahrnuje všechna nastavení zásad doporučená pro úroveň 2, ale obsahuje jenom ta nastavení, která jste přidali nebo změnili k implementaci více ovládacích prvků a pokročilejší konfiguraci než úroveň 2. Tato nastavení zásad můžou mít potenciálně významný dopad na uživatele nebo na aplikace, což vynucuje úroveň zabezpečení odpovídající cílovým organizacím, které čelí.  

#### <a name="data-protection"></a>Ochrana dat

| Nastavení | Popis nastavení |             Hodnota  |             Platforma        | Poznámky |
|---------------|---------------------------------------|----------------------------------------|--------------------------------------|---------------------------------------------------------------------------------------------------------|
| Přenos dat |       Příjem dat z jiných aplikací  |          Aplikace spravované podle zásad  |          iOS/iPadOS, Android         |  |
| Přenos dat |       Klávesnice třetích stran  |          Blok  |          iOS/iPadOS        | V systému iOS to blokuje fungování všech klávesnic třetích stran v rámci aplikace.  |
| Přenos dat |       Schválené klávesnice  |          Vyžadovat  |          Android        | V případě Androidu je třeba vybrat klávesnice, aby bylo možné je použít v závislosti na nasazených zařízeních s Androidem.  |
| Přenos dat |       Vybrat klávesnice ke schválení  |          *Přidat nebo odebrat klávesnice*  |          Android        | V případě Androidu je třeba vybrat klávesnice, aby bylo možné je použít v závislosti na nasazených zařízeních s Androidem.  |
| Funkce |       Tisk organizačních dat  |          Blok  |          iOS/iPadOS, Android         |  |

#### <a name="access-requirements"></a>Požadavky na přístup

|       Nastavení  |          Hodnota  |          Platforma  |
|-----------------------------------------------------------|--------------------|---------------------------------|
|       Jednoduchý PIN kód  |          Blok  |          iOS/iPadOS, Android  |
|       Vyberte minimální délku PIN kódu.  |          6  |          iOS/iPadOS, Android  |
|       Resetovat PIN kód po počtu dní  |          Ano  |          iOS/iPadOS, Android  |
|       Počet dní  |          365  |          iOS/iPadOS, Android  |

#### <a name="conditional-launch"></a>Podmíněné spouštění

| Nastavení | Popis nastavení |          Hodnota/akce  |          Platforma        | Poznámky |
|----------------------------|--------------------------------------|-------------------|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Podmínky zařízení  |       Minimální verze operačního systému  |          *Formát: Hlavní_verze. podverze <br>   Příklad: 8,0* /blokovat přístup   |          Android        | Microsoft doporučuje nakonfigurovat minimální hlavní verzi Androidu tak, aby odpovídala podporovaným verzím Androidu pro aplikace Microsoftu. Výrobci OEM a zařízení, kteří dodržují doporučené požadavky na Android Enterprise, musí podporovat aktuální dodací verzi a jeden upgrade na jedno písmeno.   V současné době Android doporučuje Android 8,0 a novější pro pracovníky znalostní báze.   Nejnovější doporučení pro Android najdete v tématu [Doporučené požadavky pro Android Enterprise](https://www.android.com/enterprise/recommended/requirements/) |
|       Podmínky zařízení  |          Zařízení s jailbreakem nebo rootem  |        Data není k dispozici a vymazání  |          iOS/iPadOS, Android        |  |
|       Podmínky zařízení  |          Maximální povolená úroveň hrozeb  |          Zabezpečený/blokovaný přístup  |          iOS/iPadOS, Android        | <p>U neregistrovaných zařízení je možné kontrolovat hrozby pomocí ochrany před mobilními hrozbami. Další informace najdete v tématu Ochrana před [mobilními hrozbami u neregistrovaných zařízení](https://aka.ms/mtdmamdocs).      </p><p>     Pokud je zařízení zaregistrované, toto nastavení se dá přeskočit při nasazení ochrany před mobilními hrozbami pro zaregistrovaná zařízení. Další informace najdete v tématu Ochrana před [mobilními hrozbami u zaregistrovaných zařízení](../protect/mtd-device-compliance-policy-create.md).</p> |

## <a name="next-steps"></a>Další kroky

Správci můžou začlenit výše uvedené úrovně konfigurace v rámci své metodiky nasazení do kroužku pro účely testování a produkčního použití importováním ukázkových [šablon JSON pro konfigurační Intune App Protection zásad pro Configuration Framework](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AppProtectionPolicies) pomocí [skriptů PowerShellu Intune](https://github.com/microsoftgraph/powershell-intune-samples).

## <a name="see-also"></a>Viz také

- [Jak vytvořit a nasadit zásady ochrany aplikací pomocí Microsoft Intune](app-protection-policies.md)
- [Dostupná nastavení zásad ochrany aplikací pro Android pomocí Microsoft Intune](app-protection-policy-settings-android.md)
- [Dostupná nastavení zásad ochrany aplikací pro iOS/iPadOS s Microsoft Intune](app-protection-policy-settings-ios.md)
- Aplikace jiných firem, například mobilní aplikace Salesforce, fungují s Intune specifickým způsobem, aby chránily podniková data. Další informace o tom, jak konkrétně aplikace Salesforce funguje s Intune (včetně nastavení konfigurace aplikace MDM), najdete v článku [Aplikace Salesforce a Microsoft Intune](https://gallery.technet.microsoft.com/Salesforce-App-and-Intune-c47d44ee/file/188000/1/Salesforce%20App%20and%20Intune%20for%20external.pdf).
