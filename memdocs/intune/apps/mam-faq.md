---
title: Časté otázky ke správě mobilních aplikací (MAM) a ochraně aplikací
description: Tento článek poskytuje odpovědi na některé časté otázky ke správě mobilních aplikací (MAM) Intune a ochraně aplikací Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 149def73-9d08-494b-97b7-4ba1572f0623
ms.reviewer: erikre
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59ec9f899991e63b9a652e55e3253a07dee0cc15
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79332131"
---
# <a name="frequently-asked-questions-about-mam-and-app-protection"></a>Časté otázky ke správě mobilních aplikací (MAM) a ochraně aplikací

Tento článek poskytuje odpovědi na některé časté otázky ke správě mobilních aplikací (MAM) Intune a ochraně aplikací Intune.

## <a name="mam-basics"></a>Základní informace o MAM

**Co je MAM?**<br></br>
[Správa mobilních aplikací (MAM) Intune](app-lifecycle.md) představuje sadu funkcí Intune pro správu, s kterými můžete publikovat, doručovat, konfigurovat, zabezpečovat, monitorovat a aktualizovat mobilní aplikace pro uživatele.

**Jaké jsou výhody ochrany aplikací pomocí MAM?**<br></br>
MAM chrání data organizace v rámci aplikace. Díky funkci MAM bez registrace zařízení (MAM-WE) jde pracovní nebo školní aplikaci, která obsahuje citlivá data, spravovat prakticky na jakémkoliv zařízení, včetně osobních zařízení, která uživatelé používají pracovně (BYOD, bring-your-own-device). Mnoho kancelářských aplikací, například aplikace Microsoft Office, lze spravovat přes Intune MAM. Podívejte se do oficiálního seznamu [aplikací spravovaných přes Intune](https://www.microsoft.com/cloud-platform/microsoft-intune-apps), který je veřejně přístupný.

**Jaké konfigurace zařízení MAM podporuje?**<br></br>
Intune MAM podporuje dvě konfigurace:
- **MDM+MAM Intune**: Správci IT můžou spravovat aplikace pomocí MAM a zásad ochrany aplikací jenom na zařízeních, která jsou zaregistrovaná ve správě mobilních zařízení (MDM) Intune. Pokud zákazníci chtějí spravovat aplikace pomocí MDM + MAM, měli by používat konzolu Intune na portálu Azure Portal na https://portal.azure.com.

- **MAM bez registrace zařízení:** MAM bez registrace zařízení, neboli MAM-WE, umožňuje správcům IT spravovat aplikace pomocí MAM a zásad ochrany aplikací na zařízeních, která nejsou zaregistrovaná ve správě mobilních zařízení Intune. To znamená, že aplikace je možné spravovat pomocí Intune na zařízeních, která jsou zaregistrovaná u jiných poskytovatelů EMM. Pokud chcete spravovat aplikace pomocí MAM-WE, zákazníci by měli používat konzolu Intune v Azure Portal v [https://portal.azure.com](https://portal.azure.com). Aplikace je také možné spravovat pomocí Intune na zařízeních zaregistrovaných pomocí jiných poskytovatelů správy firemních mobilních zařízení (Enterprise Mobility Management (EMM)) nebo na zařízeních vůbec v MDM nezaregistrovaných.


## <a name="app-protection-policies"></a>Zásady ochrany aplikace

**Co jsou zásady ochrany aplikací?**<br></br>
Zásady ochrany aplikací jsou pravidla, která zajistí, že data organizace budou zabezpečená nebo vázaná ve spravované aplikaci. Zásada může být pravidlo, které je vynuceno, když se uživatel pokusí pracovat s firemními daty nebo je přesunout, nebo sada akcí, které jsou zakázané nebo monitorované, pokud je uživatel uvnitř aplikace.

**Jaké jsou příklady zásad ochrany aplikací?**<br></br>
Podrobné informace o jednotlivých nastaveních zásad ochrany aplikací najdete v tématu nastavení [zásad ochrany aplikací pro Android](app-protection-policy-settings-android.md) a [nastavení zásad ochrany aplikací pro iOS/iPadOS](app-protection-policy-settings-ios.md) .

**Je možné pro stejné uživatele současně použít zásady MDM i MAM pro různá zařízení? Například pokud by uživatel mohl získat přístup ke svým pracovním prostředkům ze svého vlastního počítače s podporou MAM, ale také přichází k práci a používání zařízení spravovaného přes MDM v Intune. Existují nějaká upozornění k této myšlence?**<br></br>
Pokud pro uživatele použijete zásadu MAM bez nastavení stavu zařízení, uživatel získá zásadu MAM na zařízení BYOD i na zařízení spravovaném přes Intune. Můžete také použít zásadu MAM založenou na spravovaném stavu. Takže když vytvoříte zásady ochrany aplikací, zobrazí se vedle cíle u všech typů aplikací možnost Ne. Pak proveďte některou z následujících akcí:
- Použijte pro zařízení spravovaná přes Intune méně přísné zásady MAM a použijte pro zařízení zaregistrovaná v MDM více omezující zásadu MAM.
- Použije zásady MAM jenom pro odregistrovaná zařízení.

Další informace najdete v tématu [jak monitorovat zásady ochrany aplikací](app-protection-policies-monitor.md).

## <a name="apps-you-can-manage-with-app-protection-policies"></a>Aplikace, které se dají spravovat pomocí zásad ochrany aplikací

**Které aplikace se dají spravovat pomocí zásad ochrany aplikací?**<br></br>
Zásadami ochrany aplikací Intune se dá spravovat každá aplikace integrovaná sadou [Intune App SDK](../developer/app-sdk.md) nebo zabalená nástrojem [Intune App Wrapping](../developer/apps-prepare-mobile-application-management.md). Podívejte se do oficiálního seznamu [aplikací spravovaných přes Intune](https://www.microsoft.com/cloud-platform/microsoft-intune-apps), který je veřejně přístupný.

**Jaké jsou základní požadavky na používání zásad ochrany aplikací v aplikaci spravované přes Intune?**

- Koncový uživatel musí mít účet Azure Active Directory (AAD). Pokud se chcete dozvědět, jak se vytvářejí uživatelé Intune v Azure Active Directory, přečtěte si [Přidání uživatelů a udělení oprávnění pro správu v Intune](../fundamentals/users-add.md).

- Koncový uživatel musí mít ke svému účtu Azure Active Directory přiřazenou licenci pro Microsoft Intune. Informace o tom, jak se přiřazují licence Intune koncovým uživatelům, najdete v článku [Správa licencí Intune](../fundamentals/licenses-assign.md).

- Koncový uživatel musí patřit do skupiny zabezpečení, která je cílem zásady ochrany aplikace. Stejná zásada ochrany aplikace musí mít za cíl konkrétní používanou aplikaci. Zásady ochrany aplikací se dají vytvářet a nasazovat v konzole Intune na [portálu Azure](https://portal.azure.com). Skupiny zabezpečení se teď dají vytvořit v [centru pro správu Microsoft 365](https://admin.microsoft.com).

- Koncový uživatel se musí do aplikace přihlásit pomocí svého účtu AAD.

**Co když chci povolit aplikaci s Intune App Protection, ale nepoužíváte podporovanou platformu pro vývoj aplikací?**

Vývojový tým sady Intune SDK aktivně testuje a udržuje podporu pro aplikace vytvořené s nativními platformami Android, iOS/iPadOS (obj-C, SWIFT), Xamarin, Xamarin. Forms a Cordova. I když se někteří zákazníci dokončí s integrací sady Intune SDK s jinými platformami, jako je například reakce nativních a NativeScript, neposkytujeme explicitní pokyny ani moduly plug-in pro vývojáře aplikací, kteří používají jinou než naše podporované platformy.

**Podporuje sada Intune App SDK knihovnu MSAL (Microsoft Authentication Library) nebo účty sociálních sítí?**<br></br>
Sada Intune App SDK používá některé pokročilé možnosti ADAL (Active Directory Authentication Library) pro výchozí verze sady SDK i pro verze třetích stran. Proto knihovna MSAL příliš dobře nespolupracuje s mnoha našimi hlavními scénáři, jako je ověřování ve službě Intune App Protection nebo podmíněné spuštění. Vzhledem k tomu, že celkový návod od týmu identity společnosti Microsoft je přepnout na MSAL pro všechny systém Microsoft Office aplikace, Intune SDK bude nakonec potřebovat podporu, ale ještě neexistují žádné plány.

**Jaké jsou další požadavky na používání [mobilní aplikace Outlook](https://products.office.com/outlook)?**

- Koncový uživatel musí mít v zařízení nainstalovanou mobilní aplikaci Outlook.

- Koncový uživatel musí mít poštovní schránku [Office 365 Exchange Online](https://products.office.com/exchange/exchange-online) a licenci propojenou se svým účtem Azure Active Directory.

  >[!NOTE]
  > Mobilní aplikace Outlook aktuálně podporuje pouze Intune App Protection pro Microsoft Exchange Online a [Exchange Server s hybridním moderním ověřováním](https://technet.microsoft.com/library/mt846639(v=exchg.160).aspx) a nepodporuje Exchange v Office 365 Dedicated.

**Jaké jsou další požadavky na používání aplikací [Word, Excel a PowerPoint](https://products.office.com/business/office)?**

- Koncový uživatel musí mít licenci pro [Office 365 Business nebo Enterprise](https://products.office.com/business/compare-more-office-365-for-business-plans) propojenou se svým účtem Azure Active Directory. Předplatné musí obsahovat aplikace Office na mobilních zařízeních a může obsahovat účet pro ukládání do cloudu přes [OneDrive pro firmy](https://onedrive.live.com/about/business/). Licence na Office 365 se dají přiřadit v [centru pro správu Microsoft 365](https://admin.microsoft.com) podle těchto [pokynů](https://support.office.com/article/Assign-or-remove-licenses-for-Office-365-for-business-997596b5-4173-4627-b915-36abac6786dc).

- Koncový uživatel musí mít spravované umístění nakonfigurované pomocí podrobné funkce Uložit jako v nastavení zásad ochrany aplikací Uložit kopie org data. Pokud je spravovaným umístěním třeba OneDrive, musí být v aplikaci Word, Excel nebo PowerPoint koncového uživatele nakonfigurovaná aplikace [OneDrive](https://onedrive.live.com/about/).

- Pokud je spravovaným umístěním OneDrive, musí být aplikace cílem pro zásadu ochrany aplikace nasazenou pro koncového uživatele.

  >[!NOTE]
  > Mobilní aplikace Office aktuálně podporují jenom SharePoint Online a ne místní SharePoint.

**Proč je pro Office potřeba spravované umístění (jako OneDrive)?**<br></br>
Intune označuje veškerá data v aplikaci jako podniková (firemní) nebo osobní. Data se považují za podniková, když pocházejí z firemního umístění. U aplikací Office považuje Intune za firemní následující umístění: e-mail (Exchange) nebo cloudové úložiště (aplikace OneDrive s účtem OneDrive pro firmy).

**Jaké jsou další požadavky na používání Skypu pro firmy?**<br></br>
Viz licenční požadavky [Skypu pro firmy](https://products.office.com/skype-for-business/it-pros). Informace o hybridních a místních konfiguracích Skypu pro firmy najdete v článcích [Hybridní moderní ověřování pro Skype pro firmy a Exchange bude všeobecně dostupné](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Hybrid-Modern-Auth-for-SfB-and-Exchange-goes-GA/ba-p/134756) a [Moderní ověřování pro Skype pro firmy v místním prostředí s AAD](https://techcommunity.microsoft.com/t5/Skype-for-Business-Blog/Modern-Auth-for-SfB-OnPrem-with-AAD/ba-p/180910).

## <a name="app-protection-features"></a>Funkce ochrany aplikací

**Co je podpora více identit?**<br></br>
Podpora více identit je schopnost sady Intune App SDK použít zásady ochrany aplikací jenom na pracovní nebo školní účet přihlášený k aplikaci. Pokud se k aplikaci přihlásí osobní účet, zůstanou data nedotčená.

**Co je účelem podpory více identit?**<br></br>
Podpora více identit umožňuje, aby se aplikace pro podnikové i běžné zákazníky (tj. aplikace Office) vydávaly veřejně s funkcemi ochrany aplikací Intune pro podnikové účty.

**Jak je na tom aplikace Outlook s více identitami?**<br></br>
Outlook má kombinované zobrazení osobních a podnikových e-mailů, proto při spuštění zobrazí výzvu k zadání PINu Intune.

**Co je PIN aplikace Intune?**<br></br>
Osobní identifikační číslo (PIN) je heslo, kterým se ověřuje, že s daty organizace pracuje v aplikaci správný uživatel.

- **Když je uživatel vyzván k zadání PINu?**<br></br> Intune vyzve uživatele k zadání PINu aplikace, když se uživatel chystá pracovat s podnikovými daty. V aplikacích s více identitami, jako Word, Excel a PowerPoint, bude uživatel vyzván k zadání PINu při pokusu o otevření podnikového souboru nebo dokumentu. V aplikacích s jednou identitou, například obchodní aplikace spravované přes nástroj Intune App Wrapping, se PIN vyžaduje při spuštění, protože sada Intune App SDK ví, že prostředí uživatele v aplikaci bude vždy podnikové.

- **Jak často se uživateli zobrazí výzva k zadání kódu PIN Intune?**<br></br> Správce IT může v konzole pro správu Intune definovat nastavení zásad ochrany aplikací Překontrolovat požadavky na přístup za (minuty). Toto nastavení určuje dobu, než se v zařízení zkontrolují požadavky na přístup a znovu se zobrazí obrazovka pro kód PIN aplikace. Četnost, s jakou se budou uživateli zobrazovat výzvy, ale ovlivňují důležité detaily týkající se kódu PIN: 

  - **PIN kód se sdílí mezi aplikacemi stejného vydavatele, aby se zlepšila použitelnost:** V systému iOS/iPadOS je jeden PIN aplikace sdílený mezi všemi aplikacemi **stejného vydavatele aplikace**. V Androidu se kód PIN jedné aplikace sdílí mezi všemi aplikacemi.
  - **Chování „Překontrolovat požadavky na přístup za (minuty)“ po restartu zařízení:** „Časovač kódu PIN“ sleduje počet minut nečinnosti, které určí, kdy znovu zobrazit PIN aplikace Intune. V systému iOS/iPadOS je časovač PIN neovlivněný restartováním zařízení. Proto nebude restart zařízení nijak ovlivněný počtem minut, po který byl uživatel neaktivní z aplikace pro iOS/iPadOS pomocí zásad PIN kódu Intune. V systému Android restartování zařízení časovač kódu PIN vynuluje. Proto aplikace pro Android se zásadou pro PIN budou pravděpodobně **po restartu zařízení** vyžadovat PIN aplikace bez ohledu na hodnotu nastavení „Překontrolovat požadavky na přístup za (minuty)“.  
  - **Kolísavost časovače přidruženého ke kódu PIN:** Když po zadání kódu PIN pro přístup k nějaké aplikaci (aplikace A) se tato aplikace v zařízení přestane zobrazovat na popředí (hlavní fokus), vynuluje se časovač tohoto kódu PIN. Jakákoli aplikace (aplikace B), která tento kód PIN sdílí, nevyzve uživatele k jeho zadání, protože časovač se vynuloval. Tato výzva se zobrazí znovu, jakmile je opět splněna hodnota nastavení Překontrolovat požadavky na přístup za (minuty).

V případě zařízení se systémem iOS/iPadOS, i když je kód PIN sdílen mezi aplikacemi od různých vydavatelů, se výzva zobrazí znovu po opětovném **zjištění hodnoty požadavků na přístup po (minuty)** pro aplikaci, která není hlavním vstupním fokusem. Představte si například, že má uživatel aplikaci _A_ od vydavatele _X_ a aplikaci _B_ od vydavatele _Y_ a na obou se používá stejný PIN. Uživatel se zaměřuje na aplikaci _A_ (popředí), aplikace _B_ se minimalizuje. Když se splní hodnota **Znovu zkontrolovat požadavky na přístup po (minuty)** a uživatel přepne na aplikaci _B_, bude vyžadován PIN.

  >[!NOTE] 
  > Kvůli častějšímu ověřování požadavků na přístup uživatele (například výzvy k zadání PINu) doporučujeme zmenšit hodnotu nastavení Překontrolovat požadavky na přístup za (minuty), a to především u často používaných aplikací. 
      
- **Jak PIN kód Intune funguje s integrovanými PIN kódy aplikace pro Outlook a OneDrive?**<br></br>
PIN kód Intune funguje na základě časovače založeného na nečinnosti (hodnota "znovu kontrolovat požadavky na přístup za (minuty)"). Proto se výzvy PIN kódu Intune zobrazují nezávisle na výzvách integrovaných PIN kódů aplikace pro Outlook a OneDrive, které jsou většinou ve výchozím nastavení svázané se spuštěním aplikace. Pokud se uživateli zobrazí obě výzvy PIN kódu najednou, měl by mít přednost PIN kód Intune. 

- **Je PIN bezpečný?**<br></br> PIN slouží k tomu, aby v aplikaci povolil pracovat s daty organizace jenom správnému uživateli. Proto se koncový uživatel musí přihlásit s pracovním nebo školním účtem, aby si mohl nastavit nebo resetovat PIN pro aplikaci Intune. Toto ověření zpracovává Azure Active Directory prostřednictvím zabezpečené výměny tokenu a sada Intune App SDK do procesu nevidí. Z hlediska zabezpečení je nejlepší ochranou pracovních nebo školních dat jejich šifrování. Šifrování nesouvisí s PINem aplikace, ale jde o vlastní zásadu ochrany aplikace.

- **Jak Intune chrání PIN před útoky hrubou silou?**<br></br> Jako součást zásady pro PIN aplikace může správce IT nastavit maximální počet pokusů, které uživatel má k ověření PINu před uzamčením aplikace. Po vyčerpání pokusů může sada Intune App SDK vymazat podniková data v aplikaci.
  
- **Proč musím v aplikacích od stejného vydavatele dvakrát zadávat PIN?**<br></br> MAM (v iOS/iPadOS) v současné době povoluje PIN kód na úrovni aplikace s alfanumerickými a speciálními znaky (označované jako "heslo"), které vyžadují zapojení aplikací (například WXP, Outlook, Managed Browser, Yammer) pro integraci sady Intune APP SDK pro iOS/iPadOS. Bez toho se nastavení hesla pro cílové aplikace správně nevynutí. Tato funkce byla vydaná v Intune SDK pro iOS/iPadOS v. 7.1.12. <br><br> Aby se tato funkce podporovala a zajistila zpětná kompatibilita s předchozími verzemi sady Intune SDK pro iOS/iPadOS, jsou všechny PIN kódy v 7.1.12 + zpracovávány odděleně od číselného kódu PIN v předchozích verzích sady SDK. Proto pokud má zařízení aplikace se sadou Intune SDK pro verze iOS/iPadOS před 7.1.12 a po 7.1.12 od stejného vydavatele, budou muset nastavit dvě PIN kódy. <br><br> Tyto dva kódy PIN (pro každou aplikaci jeden) spolu nijak nesouvisejí, tzn. že musejí vyhovovat zásadám ochrany aplikace platným pro danou aplikaci. Uživatel smí nastavit stejný PIN dvakrát *jen tehdy*, když aplikace A a B používají stejné zásady (platné pro PIN). <br><br> Toto chování je specifické pro PIN aplikací pro iOS/iPadOS, které jsou povolené pomocí správy mobilních aplikací Intune. Když aplikace v průběhu času přijímají novější verze sady Intune SDK pro iOS/iPadOS, je nutné nastavit kód PIN dvakrát u aplikací od stejného vydavatele na menší problém. V následující poznámce uvádíme příklad.

  >[!NOTE]
  > Například pokud je aplikace A sestavena s verzí starší než 7.1.12 a aplikace B je sestavena s verzí větší nebo rovnou 7.1.12 od stejného vydavatele, bude muset koncový uživatel nastavit PIN kódy samostatně pro a a B, pokud jsou obě nainstalovány na zařízení iOS/iPadOS. <br><br> Pokud na toto zařízení nainstalujete aplikaci C se sadou SDK 7.1.9, bude mít stejný PIN jako aplikace A. <br><br> Aplikace D vytvořená s použitím verze 7.1.14 bude mít stejný PIN jako aplikace B. <br><br> Pokud na zařízení nainstalujete jenom aplikace A a C, stačí nastavit jenom jeden PIN. To samé platí, i pokud jsou na zařízení nainstalované aplikace B a D.

**A co šifrování?**<br></br>
Správci IT můžou nasadit zásadu ochrany aplikace, která vyžaduje šifrování dat aplikace. Jako součást této zásady může správce IT také určit, kdy se obsah bude šifrovat.

- **Jak Intune šifruje data?**<br></br> Podrobné informace o nastavení zásad ochrany aplikací pro šifrování najdete v tématu Nastavení zásad [ochrany aplikací pro Android](app-protection-policy-settings-android.md) a [nastavení zásad ochrany aplikací pro iOS/iPadOS](app-protection-policy-settings-ios.md) .

- **Co se šifruje?**<br></br> Šifrují se jenom data označená jako podniková, a to podle zásady ochrany aplikace správce IT. Data se považují za podniková, když pocházejí z firemního umístění. U aplikací Office považuje Intune za firemní následující umístění: e-mail (Exchange) nebo cloudové úložiště (aplikace OneDrive s účtem OneDrive pro firmy). U obchodních aplikací spravovaných nástrojem Intune App Wrapping se za podniková považují všechna data aplikace.

**Jak může Intune vzdáleně smazat data?**<br></br>
Intune může data aplikace smazat třemi způsoby: úplným vymazáním zařízení, selektivním vymazáním pro MDM nebo selektivním vymazáním pro MAM. Další informace o vzdáleném vymazání pro správu mobilních zařízení (MDM) najdete v článku věnovaném [odebrání zařízení pomocí vymazání nebo vyřazení](../remote-actions/devices-wipe.md). Další informace o selektivním vymazání pomocí MAM najdete v části [Vyřazení](../remote-actions/devices-wipe.md#retire) a v článku [Jak z aplikací vymazat jenom firemní data](apps-selective-wipe.md).

- **Co je vymazání?**<br></br> [Vymazání](../remote-actions/devices-wipe.md) odebere veškerá uživatelská data a nastavení ze **zařízení** obnovením jeho výchozího továrního nastavení. Zařízení se odebere ze služby Intune.
  >[!NOTE]
  > Vymazání jde dosáhnout jen na zařízeních zaregistrovaných ve správě mobilních zařízení (MDM) Intune.

- **Co je selektivní vymazání pro MDM?**<br></br> V článku [Odebrání zařízení – část Vyřazení](../remote-actions/devices-wipe.md#retire) najdete informace o odebírání firemních dat.

- **Co je selektivní vymazání pro MAM?**<br></br> Selektivní vymazání pro MAM jednoduše odebere data aplikace společnosti z aplikace. Žádost se inicializuje pomocí portálu Intune Azure Portal. Informace o zahájení žádosti o vymazání najdete v článku [Jak z aplikací vymazat jenom firemní data](apps-selective-wipe.md).

- **Jak rychle selektivní vymazání pro MAM proběhne?**<br></br> Pokud uživatel používá aplikaci, když je zahájeno selektivní vymazání, sada Intune App SDK kontroluje každých 30 minut žádost o selektivní vymazání ze služby Intune MAM. Selektivní vymazání také kontroluje tehdy, když uživatel spustí aplikaci poprvé a přihlásí se pomocí pracovního nebo školního účtu.

**Proč místní služby nepracují s aplikacemi chráněnými službou Intune?**<br></br>
Ochrana aplikací Intune závisí na identitě uživatele, aby byla konzistentní mezi aplikací a sadou Intune App SDK. Jediná cesta, která to může zaručit, je moderní ověřování. Jsou situace, kdy aplikace můžou fungovat s místní konfigurací, ale nejsou konzistentní ani nic nezaručují.

**Existuje bezpečný způsob, jak otevírat webové odkazy ze spravovaných aplikací?**<br></br>
Ano! Správce IT může nasadit a nastavit zásadu ochrany aplikace pro [aplikaci Intune Managed Browser](../apps/app-configuration-managed-browser.md), což je webový prohlížeč vyvinutý týmem Microsoft Intune, který se dá snadno spravovat přes Intune. Správce IT může vyžadovat, aby se všechny webové odkazy v aplikacích spravovaných přes Intune otvíraly v aplikaci Managed Browser.

## <a name="app-experience-on-android"></a>Prostředí aplikací na Androidu

**Proč je potřeba aplikace Portál společnosti, aby ochrana aplikací Intune fungovala na zařízeních s Androidem?**<br></br>
Většina funkcí ochrany aplikací je integrovaná do aplikace Portál společnosti. I když aplikace Portál společnosti se vždycky vyžaduje, registrace zařízení se _nevyžaduje_. U správy mobilních aplikací bez registrace (MAM-WE) je jenom nutné, aby měl koncový uživatel aplikaci Portál společnosti na zařízení nainstalovanou.

**Jak na Androidu funguje více nastavení přístupu k ochraně aplikací Intune, která jsou nakonfigurovaná na stejnou sadu aplikací a uživatelů?**<br></br>
Zásady ochrany aplikací Intune pro přístup se na zařízení koncových uživatelů, která se pokusí o přístup k cílové aplikaci z firemního účtu, použijí v konkrétním pořadí. Obecně má přednost blokování, pak upozornění, které se dá zavřít. Například pokud se aplikuje na konkrétního uživatele nebo aplikaci, nastavení minimální verze opravy Androidu, které uživatele upozorňuje, aby provedl upgrade opravy, se použije po nastavení minimální verze opravy Androidu, které uživateli zablokuje přístup. Proto ve scénáři, kde správce IT nakonfiguruje minimální verzi opravy Androidu na 2018-03-01 a minimální verzi opravy Androidu (pouze upozornění) na 2018-02-01, zatímco zařízení pokoušející se o přístup k aplikaci má verzi opravy 2018-01-01, by byl koncový uživatel zablokován na základě přísnějšího nastavení pro minimální verzi opravy Androidu, která vede k zablokování přístupu. 

Při zpracování různých typů nastavení by měl přednost požadavek na verzi aplikace. Následoval by požadavek na verzi operačního systému Android a pak požadavek na verzi opravy Androidu. Pak se ve stejném pořadí kontrolují všechna upozornění pro všechny typy nastavení.

**Zásady Intune App Protection poskytují správcům možnost vyžadovat, aby zařízení koncových uživatelů prošla ověřením identity SafetyNet Google pro zařízení s Androidem. Jak často je do služby odeslán nový výsledek ověření identity SafetyNet?** <br><br> Správce IT bude hlásit nové Google Play služby v intervalu určeném službou Intune. Četnost volání služby je způsobena omezením zatížení, takže tato hodnota je udržována interně a nelze ji konfigurovat. Veškerá akce nakonfigurovaná správcem IT pro nastavení ověřování Google SafetyNet se provede na základě posledního hlášeného výsledku služby Intune v době podmíněného spuštění. Pokud nejsou k dispozici žádná data, bude přístup povolen v závislosti na neúspěšných kontrolách nepodmíněných spuštění a Google Play služby zpětného vyhledávání pro určení výsledků ověření identity začne v back-endu a uživatel se vyzve k asynchronnímu přihlášení, pokud se zařízení nezdařilo. Pokud jsou k dispozici zastaralá data, přístup se zablokuje nebo povolí v závislosti na posledním zaznamenaném výsledku, a podobně Google Play služby zpětného dotazování pro určení výsledků ověření identity zahájí a uživatele se vyzve k asynchronnímu přihlášení, pokud se zařízení nezdařilo.

**Zásady Intune App Protection poskytují správcům možnost vyžadovat, aby zařízení koncových uživatelů odesílala signály přes rozhraní API pro zařízení s Androidem prostřednictvím rozhraní Google pro ověřování aplikací. Jak může koncový uživatel zapnout kontrolu aplikací, aby k nim neblokoval přístup z tohoto důvodu?**<br><br> Pokyny k tomu, jak to udělat, se mírně liší podle zařízení. Obecný proces zahrnuje Obchod Google Play a pak kliknutí na **Moje aplikace & hry**. Kliknutím na výsledek poslední kontroly aplikace přejdete do nabídky Play Protect. Zajistěte, aby byl přepínač pro **kontrolu zařízení pro bezpečnostní hrozby** přepnut na zapnuto.

**Co rozhraní API pro ověření identity Google SafetyNet skutečně kontroluje na zařízeních s Androidem? Jaký je rozdíl mezi konfigurovatelnými hodnotami ' Kontrola základní integrity ' a ' Kontrola základní integrity & certifikovanými zařízeními '?** <br><br>
Intune využívá Google Play ochraně rozhraní API pro SafetyNet, aby se přidaly k existujícím kontrolám zjišťování kořenu pro nezaregistrovaná zařízení. Google vyvinula a zachovala tuto sadu rozhraní API pro aplikace pro Android, aby se mohla přijmout, pokud nechtějí spouštět jejich aplikace na zařízení root. Aplikace pro platby v Androidu tento příklad zahrnula. I když Google nesdílí veřejně celou řadu kontrol kořenového zjišťování, ke kterým dojde, očekáváme, že tato rozhraní API zjišťují uživatele, kteří mají svá zařízení root. Tito uživatelé jim pak můžou zablokovat přístup nebo se jejich firemní účty vymažou z aplikací s povolenými zásadami. "Kontrola základní integrity" obsahuje informace o obecné integritě zařízení. Zařízení s rootem, emulátory, virtuální zařízení a zařízení se znaménkem neoprávněného selhání základní integrity. ' Kontrola základní integrity & certifikovaných zařízeních ' obsahuje informace o kompatibilitě zařízení s službami Google. Tuto kontrolu můžou předat jenom nezměněná zařízení, která získala certifikace od společnosti Google. Zařízení, která selžou, budou zahrnovat následující:

- Zařízení, která nevyhověla základní integritě
- Zařízení s odemčeným nástrojem pro spouštění
- Zařízení s vlastní bitovou kopií systému/ROM
- Zařízení, u kterých výrobce nepoužil, nebo předávat certifikát Google 
- Zařízení s bitovou kopií systému vytvořenou přímo ze zdrojových souborů programu Open Source v Androidu
- Zařízení se systémovou imagí beta/vývojář verze Preview

Technické podrobnosti najdete v [dokumentaci Google na SafetyNet Attestation](https://developer.android.com/training/safetynet/attestation) .

**Při vytváření zásad Intune App Protection pro zařízení s Androidem se v oddílu podmíněného spuštění nacházejí dvě podobné kontroly. Mám vyžadovat nastavení "ověření zařízení SafetyNet" nebo "zařízení s jailbreakem/rootem"?** <br><br>
Google Play chránit SafetyNet rozhraní API vyžaduje, aby koncový uživatel byl online, a to alespoň po dobu, kdy se spustí "zpětný" čas pro určení výsledků ověření identity. Pokud je koncový uživatel offline, může správce IT stále očekávat, že se výsledek vynutil z nastavení zařízení s jailbreakem/rootem. V případě, že je koncový uživatel příliš dlouhý offline, je hodnota "období odkladu v režimu offline" převedena do hry a veškerý přístup k pracovním nebo školním datům je po dosažení hodnoty časovače zablokován, dokud nebude k dispozici přístup k síti. Zapnutím obou nastavení umožníte vrstveným přístupům v dobrém stavu zařízení koncových uživatelů, což je důležité, když koncoví uživatelé přistupují k pracovním nebo školním datům na mobilních zařízeních. 

**Nastavení zásad ochrany aplikací, které využívají Google Play chránit rozhraní API, vyžaduje Služby Google Play funkce. Co když Služby Google Play nejsou povoleny v umístění, kde může být koncový uživatel?**<br><br>
Pro správné fungování Služby Google Play vyžaduje, aby nastavení ověřování zařízení SafetyNet a kontrola hrozeb u aplikací fungovala ve verzi Google. Vzhledem k tomu, že se jedná o nastavení, která spadají do oblasti zabezpečení, bude koncový uživatel zablokován, pokud je s těmito nastaveními cílen a nesplňuje příslušnou verzi Služby Google Play nebo nemá přístup k Služby Google Play. 

## <a name="app-experience-on-ios"></a>Prostředí aplikací v iOS
**Co se stane, když v zařízení přidám nebo odeberu otisk prstu nebo tvář?**<br></br>
Zásady ochrany aplikací Intune umožňují řídit přístup k aplikacím jen uživatelům s licencí na Intune. Jedním ze způsobů, jak řídit přístup k aplikacím, je vyžadovat na podporovaných zařízeních Touch ID nebo Face ID od Applu. Intune se chová tak, že když se v zařízení změní databáze biometrických údajů, vyzve uživatele k zadání kódu PIN, pokud je splněna hodnota časového limitu nečinnosti. Ke změnám biometrických údajů patří přidání nebo odebrání otisku prstu nebo tváře. Pokud uživatel Intune nemá nastavený kód PIN, je nasměrován na nastavení kódu PIN pro Intune.

Záměrem tohoto chování je nadále udržovat data organizace v aplikaci zabezpečená a chráněná na úrovni aplikace. Tato funkce je dostupná jenom pro iOS/iPadOS a vyžaduje zapojení aplikací, které integrují sadu Intune APP SDK pro iOS/iPadOS, verze 9.0.1 nebo novější. Integrace této sady SDK je nezbytná kvůli vynucení tohoto chování u cílových aplikací. K této integraci dochází průběžně a závisí na týmech konkrétních aplikací. Mezi zapojené aplikace patří například WXP, Outlook, Managed Browser a Yammer.
  
**Můžu pomocí rozšíření pro sdílení pro iOS otevřít pracovní nebo školní data v nespravovaných aplikacích, a to i v případě, že se zásady přenosu dat nastavily jenom na spravované aplikace nebo žádné aplikace. Nejedná se o nevrácená data?**<br></br>
Zásady ochrany aplikací pro Intune nemůžou ovládat rozšíření pro sdílení v iOS, když dané zařízení nespravují. Proto Intune _**podniková data před jejich sdílením mimo příslušnou aplikaci zašifruje**_ . Můžete si to ověřit tak, že si zkusíte otevřít podnikový soubor mimo spravovanou aplikaci. Soubor by měl být zašifrovaný a mimo spravovanou aplikaci by ho nemělo být možné otevřít.

**Jak v iOSu funguje více nastavení přístupu k ochraně aplikací Intune, která jsou nakonfigurovaná na stejnou sadu aplikací a uživatelů?**<br></br>
Zásady ochrany aplikací Intune pro přístup se na zařízení koncových uživatelů, která se pokusí o přístup k cílové aplikaci z firemního účtu, použijí v konkrétním pořadí. Obecně má přednost vymazání, pak blokování, a pak upozornění, které se dá zavřít. Například pokud se vztahuje na konkrétního uživatele nebo aplikaci, nastavení minimálního operačního systému iOS/iPadOS, které uživatele upozorní na aktualizaci verze iOS/iPadOS, se použije po nastavení minimálního operačního systému iOS/iPadOS, které uživateli zablokuje přístup. Proto ve scénáři, kde správce IT nakonfiguruje minimální operační systém iOS/iPadOS na 11.0.0.0 a minimální operační systém iOS/iPadOS (pouze upozornění) na 11.1.0.0, zatímco zařízení pokoušející se o přístup k aplikaci bylo v iOS/iPadOS 10, bude koncový uživatel zablokován na základě přísnějšího nastavení pro minimální verzi operačního systému iOS/iPadOS, která vede k zablokování přístupu.

Při zpracování různých typů nastavení by měl přednost požadavek verze sady Intune App SDK a pak požadavek na verzi aplikace následovaný požadavkem na verzi operačního systému iOS/iPadOS. Pak se ve stejném pořadí kontrolují všechna upozornění pro všechny typy nastavení. Doporučujeme nakonfigurovat verzi Intune App SDK jenom po pokynu od produktového týmu Intune pro základní scénáře blokování.


## <a name="see-also"></a>Viz také
- [Implementace plánu Intune](../fundamentals/planning-guide-onboarding.md)
- [Testování a ověřování Intune](../fundamentals/planning-guide-test-validation.md)
- [Nastavení zásad správy mobilních aplikací pro Android v Microsoft Intune](../apps/app-protection-policy-settings-android.md)
- [nastavení zásad správy mobilních aplikací pro iOS/iPadOS](../apps/app-protection-policy-settings-ios.md)
- [Aktualizace zásad ochrany aplikací](../apps/app-protection-policy-delivery.md)
- [Ověření zásad ochrany aplikací](../apps/app-protection-policy-delivery.md)
- [Přidání zásad konfigurace aplikací pro spravované aplikace bez registrace zařízení](../apps/app-configuration-policies-managed-app.md)
- [Jak získat podporu pro Microsoft Intune](../fundamentals/get-support.md)
