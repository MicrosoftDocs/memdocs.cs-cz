---
title: Správa hromadně zakoupených aplikací Apple
titleSuffix: Microsoft Intune
description: Přečtěte si, jak synchronizovat aplikace zakoupené v rámci multilicenčního programu z obchodu iOS/iPadOS a macOS App Storu do Microsoft Intune a pak můžete spravovat a sledovat jejich používání.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 51d45ce2-d81b-4584-8bc4-568c8c62653d
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 750bc9411e93ac09f857518a1e794f8d69d8575c
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746608"
---
# <a name="how-to-manage-ios-and-macos-apps-purchased-through-apple-volume-purchase-program-with-microsoft-intune"></a>Jak spravovat aplikace pro iOS a macOS zakoupené prostřednictvím Apple Volume Purchase Program s využitím Microsoft Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Apple vám umožní koupit více licencí pro aplikaci, kterou chcete ve vaší organizaci použít v zařízeních s iOS/iPadOS a macOS pomocí [Apple Business Manageru](https://business.apple.com/) nebo [Apple School Manageru](https://school.apple.com/). Potom je možné synchronizovat informace o hromadném nákupu s Intune a sledovat využití aplikací, které jste tímto způsobem koupili. Nákup licencí aplikací vám pomůže efektivně spravovat aplikace v rámci vaší společnosti a uchovávat vlastnictví a kontrolu nad zakoupenými aplikacemi. 

Microsoft Intune vám pomůže spravovat aplikace zakoupené prostřednictvím tohoto programu:

- Synchronizují se tokeny umístění, které stáhnete z Apple Business Manageru.
- Sledování, kolik licencí je dostupných a které se používaly pro zakoupené aplikace.
- Pomůže vám nainstalovat aplikace až do počtu licencí, které vlastníte.

Kromě toho můžete pomocí Intune synchronizovat, spravovat a přiřazovat knihy, které jste zakoupili v Apple Business Manageru, a to pro zařízení s iOS/iPadOS. Další informace najdete v tématu [Správa e-knih pro iOS/iPadOS zakoupených prostřednictvím programu hromadného nákupu](vpp-ebooks-ios.md).

## <a name="what-are-location-tokens"></a>Co jsou tokeny umístění?
Tokeny umístění jsou známé také jako tokeny programu Volume purchase program (VPP). Tyto tokeny se používají pro přiřazení a správu licencí zakoupených pomocí nástroje Apple Business Manager. Správci obsahu můžou zakoupit a přidružit licence k tokenům umístění, ke kterým mají oprávnění v Apple Business Manageru. Tyto tokeny umístění se pak stáhnou z Apple Business Manageru a nahrají se v Microsoft Intune. Microsoft Intune podporuje nahrávání více tokenů umístění na tenanta. Tokeny mají platnost jeden rok.

## <a name="how-are-purchased-apps-licensed"></a>Jak se aplikace koupily jako licencované?
Zakoupené aplikace je možné přiřadit ke skupinám pomocí dvou typů licencí, které Apple nabízí pro zařízení s iOS/iPadOS a macOS.

|  | Licencování zařízení | Licencování uživatelů |
|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Přihlášení do App Storu | Nepožadováno. | Každý koncový uživatel musí při zobrazení výzvy k přihlášení do App Storu použít jedinečné Apple ID. |
| Konfigurace zařízení blokující přístup k obchodu s aplikacemi | Aplikace se dají nainstalovat a aktualizovat pomocí Portál společnosti. | Pozvánka k připojení k programu Apple VPP vyžaduje přístup k App Storu. Pokud jste nastavili zásadu pro zakázání App Storu, Licencování uživatelů pro aplikace VPP nebude fungovat. |
| Automatická aktualizace aplikace | Jak je nakonfiguroval správce Intune v nastavení tokenu Apple VPP.<p>Pokud je typ přiřazení dostupný pro zaregistrovaná zařízení, můžete z Portál společnosti nainstalovat taky dostupné aktualizace aplikací, a to tak, že na stránce podrobností aplikace vyberete akci **aktualizovat** . | Jak je nakonfigurované koncovým uživatelem v nastavení osobního obchodu s aplikacemi. Tuto funkci nemůže spravovat správce Intune. |
| Zápis uživatele | Není podporováno. | Podporováno pomocí spravovaných Apple ID. |
| Knihy | Není podporováno. | Podporuje se. |
| Používané licence | 1 licence na zařízení Licence je přidružená k zařízení. | 1 licence pro až 5 zařízení, která používají stejné osobní Apple ID. Licence je přidružena k uživateli.<p>Koncový uživatel přidružený k osobnímu Apple ID a spravovanému Apple ID v Intune spotřebovává 2 licence aplikací. |
| Migrace licencí | Aplikace se můžou v tichém režimu migrovat z licencí uživatelů na zařízení. | Aplikace nemůžou migrovat ze zařízení na uživatelské licence. |

> [!NOTE]  
> Portál společnosti nezobrazuje aplikace licencované pro zařízení v zařízeních pro registraci uživatelů, protože na zařízeních pro zápis uživatelů je možné nainstalovat jenom aplikace licencované pro uživatele.

## <a name="what-app-types-are-supported"></a>Jaké typy aplikací jsou podporované?
Můžete zakoupit a distribuovat veřejné i soukromé aplikace pomocí nástroje Apple Business Manager.
- **Aplikace pro Store:** Pomocí Apple Business Manageru můžou správci obsahu koupit bezplatné i placené aplikace, které jsou k dispozici v obchodě s aplikacemi.
- **Vlastní aplikace:** Pomocí Apple Business Manageru můžou správci obsahu taky koupit vlastní aplikace, které jsou pro vaši organizaci k dispozici soukromě. Tyto aplikace jsou přizpůsobené konkrétním potřebám vaší organizace vývojářům, se kterými přímo pracujete. Přečtěte si další informace o [tom, jak distribuovat vlastní aplikace](https://developer.apple.com/business/custom-apps/).

## <a name="prerequisites"></a>Požadavky
- Účet [Apple Business Manager](https://business.apple.com/) nebo [Apple School Manager](https://school.apple.com/) pro vaši organizaci. 
- Zakoupené licence aplikace přiřazené k jedné nebo více tokenům umístění. 
- Byly staženy tokeny umístění. 

> [!IMPORTANT]
> - Token umístění se dá v jednu chvíli použít jenom s jedním řešením správy zařízení. Než začnete používat zakoupené aplikace s Intune, odvoláte a odeberete všechny existující tokeny umístění používané s jiným dodavatelem správy mobilních zařízení (MDM). 
> - Token umístění se podporuje jenom pro použití v jednom klientovi Intune. Nepoužívejte znovu stejný token pro více tenantů Intune.
> - Ve výchozím nastavení Intune synchronizuje tokeny umístění s Apple dvakrát denně. Ruční synchronizaci můžete kdykoli iniciovat v Intune.
> - Po naimportování tokenu umístění do Intune neimportujte stejný token do žádného jiného řešení správy zařízení. Pokud byste to udělali, mohli byste ztratit přiřazení licence a uživatelských záznamů.

## <a name="migrate-from-volume-purchase-program-vpp-to-apps-and-books"></a>Migrace z programu Volume purchase program (VPP) do aplikací a knih
Pokud se ještě nemigruje na Apple Business Manager nebo Apple School Manager, přečtěte si [pokyny společnosti Apple o migraci na aplikace a knihy](https://support.apple.com/HT208257) před tím, než budete pokračovat v správě zakoupených aplikací v Intune.

> [!IMPORTANT]
> - Pro dosažení optimálního prostředí migrace proveďte migraci pouze jednoho nákupčího VPP na jedno místo. Pokud se každý nákupčí migruje do jedinečného umístění, přesunou se do aplikací a knih všechny licence (přiřazené a nepřiřazené).
> - Neodstraňujte stávající starší tokeny VPP v Intune nebo aplikace a přiřazení přidružená k existujícímu staršímu tokenu VPP v Intune. Tyto akce budou vyžadovat, aby se všechna přiřazení aplikací znovu vytvořila v Intune.

Migrujte existující koupený obsah a tokeny VPP do aplikací a knih v Apple Business Manageru nebo Apple School Manageru následujícím způsobem:

1. Vyzvěte nákupčí VPP, aby se připojili k vaší organizaci, a nasměrujte jednotlivé uživatele na výběr jedinečného umístění. 
2. Než budete pokračovat, ujistěte se, že všichni odběratelé VPP v rámci vaší organizace dokončili krok 1.
3. Ověřte, že se všechny koupené aplikace a licence migrovali do aplikací a knih v Apple Business Manageru nebo Apple School Manageru.
4. Stáhněte si nový token umístění, a to tak, že v aplikaci **Apple Business (nebo School) Manager**  >  **Nastavení**  >  **aplikace a**  >  **Moje tokeny na serverech**.
5. Aktualizujte token umístění v centru pro správu Microsoft Endpoint Manageru tak, že v části provedete konektory **pro správu tenanta**  >  **a**tokeny  >  **Apple VPP** a ručně nahrajete token.

## <a name="upload-an-apple-vpp-or-location-token"></a>Nahrání tokenu Apple VPP nebo umístění

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte možnost konektory **správy tenanta**  >  **a tokeny**programu  >  **Apple VPP**.
3. V podokně s tokeny VPP vyberte **Vytvořit**.
4. V podokně **Vytvořit token VPP** zadejte následující informace:
    - **Soubor tokenu VPP** – Pokud jste to ještě neudělali, zaregistrujte se do Apple Business Manageru nebo Apple School Manager. Po zaregistrování si stáhněte token Apple VPP pro svůj účet a vyberte ho tady.
    - **Apple ID** – zadejte spravované Apple ID účtu přidruženého k odeslanému tokenu.
    - **Převzít kontrolu nad tokenem z jiné MDM** – nastavením této možnosti na **Ano** umožníte, aby se token přiřadil do Intune z jiného řešení MDM.
    - **Název tokenu** – pole pro správu pro nastavení názvu tokenu.
    - **Země/oblast** – vyberte úložiště VPP země/oblast.  Intune synchronizuje aplikace VPP pro všechna národní prostředí ze zadaného úložiště v zemi nebo oblasti VPP.
        > [!WARNING]  
        > Když se změní země nebo oblast, aktualizují se metadata aplikace a adresa URL obchodu s aplikacemi při příští synchronizaci se službou Apple pro aplikace vytvořené pomocí tohoto tokenu. Aplikace nebude aktualizována, pokud neexistuje v úložišti nové země/oblast.

    - **Typ účtu VPP** – zvolte jednu z možností: **Obchodní** nebo **Vzdělávání**.
    - **Automatické aktualizace aplikací** – zvolte **Zapnuto** nebo **Vypnuto** podle toho, jestli chcete automatické aktualizace povolit nebo zakázat. Když je tato možnost povolená, Intune zjistí aktualizace aplikací VPP v App Storu a automaticky je odešle do zařízení, jakmile se ohlásí.

        > [!NOTE]
        > Automatické aktualizace aplikací pro aplikace Apple VPP se automaticky aktualizují pro **požadované** i **dostupné** instalační záměry. U aplikací nasazených s **dostupným** záměrem instalace vygeneruje Automatická aktualizace stavovou zprávu pro správce IT, která informuje o tom, že je k dispozici nová verze aplikace. Tato stavová zpráva se zobrazí tak, že se vybere aplikace, vyberete stav instalace zařízení a zkontrolujete podrobnosti o stavu.  

    - **Udělujem Microsoftu oprávnění odesílat informace o uživatelích i zařízeních do společnosti Apple.** – **Chcete-li pokračovat** , je nutné vybrat souhlasím. Informace o tom, jaká data Microsoft posílá společnosti Apple, najdete v tématu [data Intune odesílají společnosti Apple](../protect/data-intune-sends-to-apple.md).
5. Po dokončení vyberte **Vytvořit**. Token se zobrazí v podokně se seznamem tokenů.

## <a name="synchronize-a-vpp-token"></a>Synchronizace tokenu VPP

Můžete synchronizovat názvy aplikací, metadata a informace o licencích pro vaše zakoupené aplikace v Intune výběrem možnosti **synchronizovat** pro vybraný token.

## <a name="assign-a-volume-purchased-app"></a>Přiřazení hromadně koupené aplikace

1. Vyberte **aplikace**  >  **všechny aplikace**.
2. V podokně se seznamem aplikací zvolte aplikaci, kterou chcete přiřadit, a pak zvolte **Přiřazení**.
3. V podokně **přiřazení názvu aplikace**  -  **Assignments** zvolte **Přidat skupinu** a pak v podokně **Přidat skupinu** vyberte **Typ přiřazení** a skupiny uživatelů nebo zařízení Azure AD, ke kterým chcete aplikaci přiřadit.
5. Pro každou zvolenou skupinu vyberte následující nastavení:
    - **Typ** – vyberte, jestli bude aplikace **k dispozici** (koncoví uživatelé můžou aplikaci nainstalovat z Portálu společnosti), nebo **povinná** (aplikace se na zařízení koncových uživatelů nainstaluje automaticky).
    - **Typ licence** – vyberte **Licencování uživatelů** nebo **Licencování zařízení**.
6. Až to budete mít, zvolte **Uložit**.


>[!NOTE]
>Dostupný záměr nasazení není pro skupiny zařízení podporován, jsou podporovány pouze skupiny uživatelů. V seznamu zobrazené aplikace jsou přidružené k tokenu. Pokud máte aplikaci, která je spojená s více tokeny VPP, zobrazí se stejná aplikace několikrát – jednou u každého tokenu.

> [!NOTE]  
> Intune (nebo jakákoli jiná MDM) pro tuto skutečnost neinstaluje aplikace VPP. Místo toho se Intune připojí k účtu VPP a sdělí Apple, které licence k aplikacím přiřadí k těmto zařízením. Odtud se veškerá vlastní instalace zpracuje mezi společností Apple a zařízením.
> 

## <a name="end-user-prompts-for-vpp"></a>Výzvy k VPP pro koncové uživatele

Koncový uživatel obdrží výzvu k instalaci aplikace v rámci VPP v řadě scénářů. Jednotlivé podmínky jsou vysvětlené v tabulce:

| # | Scénář                                | Pozvánka do programu Apple VPP                              | Výzva při instalaci aplikace | Výzva k zadání Apple ID |
|---|--------------------------------------------------|-------------------------------------------------------------------------------------------------|---------------------------------------------|-----------------------------------|
| 1 | BYOD – uživatel licencovaný (nejedná se o zařízení pro zápis uživatelů)                             | Ano                                                                                               | Ano                                           | Ano                                 |
| 2 | Zařízení společnosti – licencovaný uživatel (zařízení není pod dohledem)     | Ano                                                                                               | Ano                                           | Ano                                 |
| 3 | Zařízení společnosti – licencovaný uživatel (zařízení pod dohledem)         | Ano                                                                                               | N                                           | Ano                                 |
| 4 | Vlastní zařízení – licencované zařízení                           | N                                                                                               | Ano                                           | N                                 |
| 5 | Zařízení společnosti – licencované zařízení (zařízení není pod dohledem)                           | N                                                                                               | Ano                                           | N                                 |
| 6 | Zařízení společnosti – licencované zařízení (zařízení pod dohledem)                           | N                                                                                               | N                                           | N                                 |
| 7 | Beznabídkový režim (zařízení pod dohledem) – licencované zařízení | N                                                                                               | N                                           | N                                 |
| 8 | Beznabídkový režim (zařízení pod dohledem) – licencovaný uživatel   | --- | ---                                          | ---                                |

> [!Note]  
> Nedoporučujeme přiřazovat aplikace VPP do zařízení v celoobrazovkovém režimu pomocí Licencování uživatelů.

## <a name="revoking-app-licenses"></a>Odvolávání licencí aplikací

Můžete odvolat všechny přidružené licence aplikací pro iOS/iPadOS nebo macOS programu Volume purchase program (VPP) na základě daného zařízení, uživatele nebo aplikace.  Existují však určité rozdíly mezi platformami iOS/iPadOS a macOS. 

|  | iOS/iPadOS | macOS |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Odebrat přiřazení aplikace | Když odeberete aplikaci, která byla přiřazena uživateli, Intune znovu vyřadí licenci uživatele nebo zařízení a odinstaluje aplikaci ze zařízení. | Když odeberete aplikaci, která byla přiřazena uživateli, Intune znovu získá licenci uživatele nebo zařízení. Aplikace se ze zařízení neodinstaluje. |
| Odvolat licenci aplikace | Odvolání licence aplikace znovu získá licenci aplikace od uživatele nebo zařízení. Aby bylo možné aplikaci odebrat ze zařízení, je nutné změnit přiřazení pro **odinstalaci** . | Odvolání licence aplikace znovu získá licenci aplikace od uživatele nebo zařízení. Aplikace macOS s odvolanými licencemi zůstává v zařízení použitelná, ale nedá se aktualizovat, dokud uživatel nebo zařízení nepřidá licenci. Podle Applu se takové aplikace po uplynutí 30denní lhůty odeberou. Společnost Apple ale neposkytuje způsob, jak Intune aplikaci odebrat, a to pomocí akce odinstalovat přiřazení. |

>[!NOTE]
> - Pokud zaměstnanec odejde z firmy a už není součástí skupin AAD, Intune uvolní licence k aplikacím.
> - Když přiřadíte zakoupenou aplikaci s záměrem **odinstalace** , Intune obě licence znovu vyřadí a aplikace odinstaluje.
> - Licence aplikací se při odebrání zařízení ze správy Intune neuvolní. 

## <a name="deleting-vpp-tokens"></a>Odstraňují se tokeny VPP.
<!-- 820879 -->  
Pomocí konzoly nástroje můžete odstranit token programu Apple Volume purchase program (VPP). To může být nutné v případě, že máte duplicitní instance tokenu VPP. Odstraněním tokenu se odstraní také všechny přidružené aplikace a přiřazení. Odstraněním tokenu se ale licence aplikací neodvolají ani aplikace neodinstalují. 

>[!NOTE]
>Po odstranění tokenu nemůže Intune odvolat licence aplikací. 

<!-- 820870 -->  
K odvolání licencí všech aplikací VPP pro daný token VPP je nutné nejprve odvolat všechny licence aplikací, které jsou k tomuto tokenu přidružené, a potom daný token odstranit.

## <a name="renewing-app-licenses"></a>Obnovení licencí aplikací

Token Apple VPP si můžete prodloužit stažením nového tokenu z [Apple Business Manageru](https://business.apple.com/) nebo [Apple School Manageru](https://school.apple.com/) a aktualizací existujícího tokenu v Intune. 

K obnovení tokenu Apple VPP použijte následující postup:

1. Přejděte na [Apple Business Manager](https://business.apple.com/) nebo [Apple School Manager](https://school.apple.com/).
2. Stáhněte si nový token ve **Správci Apple Business (nebo School)**, a to tak, že vyberete **Nastavení**  >  **aplikace a kniha**  >  **Moje tokeny serveru**.
3. Aktualizujte token v [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) tak, že vyberete možnost konektory **pro správu tenanta**  >  **a tokeny**  >  **Apple VPP**. Pak ručně nahrajte token.

>[!NOTE]
>Pokud chcete, aby uživatel, který nastavil token v Apple Business Manageru, změnil heslo nebo uživatel zůstane v organizaci Apple Business Manageru, musíte si z Apple Business Manageru stáhnout nový token pro Apple VPP nebo location a aktualizovat existující token v Intune. Tokeny, které se neobnovily, zobrazí v Intune stav "neplatný".

## <a name="deleting-a-vpp-app"></a>Odstranění aplikace VPP

V současné době nemůžete z Microsoft Intune odstranit aplikaci VPP pro iOS/iPadOS.

## <a name="assigning-custom-role-permissions-for-vpp"></a>Přiřazují se oprávnění vlastní role pro VPP

Přístup k tokenům Apple VPP a aplikacím VPP se dá řídit nezávisle pomocí oprávnění přiřazených k vlastním rolím Správce v Intune.

* Pokud chcete, aby vlastní role Intune spravovala tokeny programu Apple VPP, vyberte v centru pro správu Microsoft Endpoint Manageru možnost konektory **pro správu tenanta**  >  **a tokeny**  >  **Apple VPP**, přiřaďte oprávnění pro **spravované aplikace**.
* Aby mohla vlastní role Intune spravovat aplikace zakoupené pomocí tokenů VPP pro iOS/iPadOS v části **aplikace**  >  **všechny aplikace**, přiřaďte oprávnění pro **mobilní aplikace**. 

## <a name="additional-information"></a>Další informace

Při vytváření a obnovování tokenů VPP můžete využít přímou podporu od společnosti Apple. Podrobnosti najdete v článku [Distribuce obsahu vašim uživatelům v rámci programu hromadných nákupů (VPP)](https://go.microsoft.com/fwlink/?linkid=2014661) v dokumentaci Apple. 

Pokud se na portálu Intune uvádí **Přiřazeno k externí správě MDM**, můžete v Intune použít token VPP až poté, co jste ho (vy jako správce) odebrali ze správy MDM třetí strany.

## <a name="frequently-asked-questions"></a>Nejčastější dotazy

### <a name="how-many-tokens-can-i-upload"></a>Kolik tokenů můžu nahrát?

Do Intune můžete nahrát až 3 000 tokenů.

### <a name="how-long-does-the-portal-take-to-update-the-license-count-once-an-app-is-installed-or-removed-from-the-device"></a>Jak dlouho trvá, než portál po instalaci aplikace nebo jejím odebrání ze zařízení aktualizuje počet licencí?

Licence by se měly aktualizovat do několika hodin od instalace nebo odinstalace aplikace. Je třeba mít na paměti, že pokud koncový uživatel odebere aplikaci ze zařízení, zůstává licence danému uživateli nebo zařízení stále přiřazená.

### <a name="is-it-possible-to-oversubscribe-an-app-and-if-so-in-what-circumstance"></a>Je možné přidělit aplikaci nadměrnému počtu subjektů? A pokud ano, za jakých okolností?

Ano. Správce Intune může aplikaci přidělit nadměrnému počtu uživatelů nebo zařízení. A to například tehdy, když zakoupí sto licencí k aplikaci XYZ a potom ji zacílí na skupinu s pěti sty členy. Prvnímu stu členů (uživatelům nebo zařízením) se licence přiřadí a u zbylých členů se přiřazení licence nezdaří.

## <a name="next-steps"></a>Další kroky

Informace, s kterými budete moct lépe sledovat přiřazování aplikací, najdete v článku [Jak sledovat přiřazení aplikací](apps-monitor.md).

Informace o řešení problémů souvisejících s aplikacemi najdete v tématu řešení [potíží s aplikacemi](troubleshoot-app-install.md) .
