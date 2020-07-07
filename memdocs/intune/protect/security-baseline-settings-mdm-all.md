---
title: Nastavení standardních hodnot zabezpečení Intune pro Windows 10 MDM
titleSuffix: Microsoft Intune
description: Zkontrolujte výchozí a dostupná nastavení pro různé verze standardních hodnot zabezpečení Windows MDM, které můžete spravovat pomocí Microsoft Intune.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/06/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
zone_pivot_groups: windows-mdm-versions
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9cc2cf4531c2e2d7a2847ccdbce87c8b938a46d6
ms.sourcegitcommit: b90d51f7ce09750e024b97baf6950a87902a727c
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022224"
---
# <a name="windows-mdm-security-baseline-settings-for-intune"></a>Nastavení standardních hodnot zabezpečení Windows MDM pro Intune

Zobrazte nastavení základní hodnoty zabezpečení MDM, které Microsoft Intune podporuje pro zařízení se systémem Windows 10 nebo novějším. Výchozí hodnoty pro nastavení v tomto směrném plánu reprezentují doporučenou konfiguraci pro příslušná zařízení. Výchozí hodnoty pro jednu základnu se nemusí shodovat s výchozími hodnotami z jiných standardních hodnot zabezpečení nebo z jiných verzí tohoto směrného plánu.

- Další informace o použití standardních hodnot zabezpečení s Intune a postup upgradu základní verze v profilech standardních hodnot zabezpečení najdete v tématu [použití standardních hodnot zabezpečení](security-baselines.md).
- Nejnovější základní verze je základní hodnota **zabezpečení MDM pro květen 2019**

Chcete-li zjistit, co se změnilo v této verzi směrného plánu z předchozích verzí, použijte akci [Porovnat směrné plány](../protect/security-baselines.md#compare-baseline-versions) , která je k dispozici při prohlížení podokna *verze* pro tento směrný plán.

Nezapomeňte vybrat verzi směrného plánu, kterou chcete zobrazit.
<!-- Cookies might be required to enable some browsers to display the zone options -->

::: zone pivot="mdm-may-2019"

**Základní hodnota zabezpečení MDM pro květen 2019**:  
> [!NOTE]
> V červnu 2019 byla šablona *zabezpečení MDM pro květen 2019* vydaná jako obecně dostupná (není ve verzi Preview). Tato verze standardních hodnot zabezpečení nahrazuje předchozí standardní hodnoty *zabezpečení MDM pro 2018. října*.  Profily, které byly vytvořeny před dostupností směrného plánu květen 2019, se neaktualizují, aby odrážely nastavení a hodnoty, které jsou ve verzi květen 2019.  I když nemůžete vytvořit nové profily založené na šabloně Preview, můžete upravit a pokračovat v používání profilů, které jste vytvořili dříve, a to na základě šablony ve verzi Preview.

Informace o tom, co se změnilo v této verzi směrného plánu z předchozí verze, najdete v tématu [co se změnilo v nové šabloně](#whats-changed-in-the-new-template).

::: zone-end
::: zone pivot="mdm-preview"

**Preview – směrný plán zabezpečení MDM pro říjen 2018**:  
> [!NOTE]
> Toto je verze Preview směrného plánu zabezpečení MDM vydaná v říjnu od 2018. Tato verze Preview byla v červnu 2019 nahrazena vydáním *směrného plánu zabezpečení MDM pro šablonu květen 2019* , která je všeobecně dostupná (není ve verzi Preview). Profily, které byly vytvořeny před dostupností *směrného plánu zabezpečení MDM pro květen 2019* , se nebudou aktualizovat tak, aby odrážely nastavení a hodnoty, které jsou v směrném plánu zabezpečení MDM pro verzi květen 2019. I když nemůžete vytvořit nové profily založené na šabloně Preview, můžete upravit a pokračovat v používání profilů, které jste vytvořili dříve, a to na základě šablony ve verzi Preview.

::: zone-end
::: zone pivot="mdm-may-2019,mdm-preview"

## <a name="above-lock"></a>Nad zámkem

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – AboveLock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-abovelock) .  

- **Blokovat zobrazování oznámení informačních**zpráv:  
  Toto nastavení zásad umožňuje zabránit zobrazování oznámení aplikace na zamykací obrazovce. Pokud toto nastavení zásad povolíte, na zamykací obrazovce se nezobrazí žádná oznámení aplikací. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, uživatelé budou moci zvolit, které aplikace budou zobrazovat oznámení na zamykací obrazovce.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067101)

  **Výchozí**: Ano

::: zone-end
::: zone pivot="mdm-may-2019"

- **Hlasové aktivace aplikací z uzamčené obrazovky**:  
  **Výchozí**: zakázáno

::: zone-end
::: zone pivot="mdm-may-2019,mdm-preview"

## <a name="app-runtime"></a>Modul runtime aplikace

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – AppRuntime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-appruntime) .

- **Volitelné účty Microsoft pro aplikace pro Windows Store**:  
  Nastavení této zásady umožňuje řídit, jestli jsou účty Microsoft volitelné pro aplikace pro Windows Store, které vyžadují účet pro přihlášení. Tato zásada ovlivňuje pouze aplikace pro Windows Store, které ji podporují. Pokud toto nastavení zásad povolíte, aplikace pro Windows Store, které obvykle vyžadují účet Microsoft pro přihlášení, umožní uživatelům přihlásit se místo toho podnikovým účtem. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, uživatelé se musí přihlašovat pomocí účet Microsoft.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067104)
  
  **Výchozí**: povoleno

## <a name="application-management"></a>Správa aplikací

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – ApplicationManagement](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-applicationmanagement) .

::: zone-end
::: zone pivot="mdm-may-2019"

- **Blokovat uživatelský ovládací prvek při instalacích**:  
  Nastavení této zásady umožňuje uživatelům změnit možnosti instalace, které jsou obvykle k dispozici pouze správcům systému. Pokud toto nastavení zásad povolíte, přeskočí se některé funkce zabezpečení Instalační služba systému Windows. Umožňuje dokončení instalací, které by jinak bylo zastaveno z důvodu porušení zabezpečení. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, funkce zabezpečení Instalační služba systému Windows zabrání uživatelům měnit možnosti instalace obvykle rezervované pro správce systému, jako je například určení adresáře, do kterého jsou soubory nainstalovány. Pokud Instalační služba systému Windows zjistí, že instalační balíček povolil uživateli změnu chráněné možnosti, zastaví instalaci a zobrazí zprávu. Tyto funkce zabezpečení fungují pouze v případě, že instalační program běží v privilegovaném kontextu zabezpečení, ve kterém má přístup k adresářům odepřeným uživateli. Nastavení této zásady je určené pro méně omezující prostředí. Dá se použít k obcházení chyb v instalačním programu, který brání instalaci softwaru.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067060)

  **Výchozí**: Ano

- **Blokovat instalace aplikací MSI se zvýšenými oprávněními**:  
  Nastavení této zásady směruje Instalační služba systému Windows, aby při instalaci jakéhokoli programu do systému používala zvýšená oprávnění.

  - *Pokud nastavení této zásady povolíte*, budou se oprávnění rozšířit na všechny programy. Obvykle jsou tato oprávnění vyhrazena pro programy, které jsou přiřazeny uživateli (které jsou nabízeny na ploše), jsou přiřazeny k počítači (nainstalovány automaticky), nebo jsou k dispozici v Ovládacích panelech přidat nebo odebrat programy. Toto nastavení profilu umožňuje uživatelům instalovat programy, které vyžadují přístup k adresářům, které uživatel nemusí mít oprávnění k zobrazení nebo změně, včetně adresářů na vysoce omezených počítačích.

  - *Pokud toto nastavení zásad zakážete nebo*nenakonfigurujete, použije systém při instalaci programů, které správce systému nedistribuuje nebo nenabízí, oprávnění aktuálního uživatele. Poznámka: nastavení této zásady se zobrazuje jak v konfiguraci počítače, tak ve složkách Konfigurace uživatele. Aby bylo nastavení této zásady účinné, musíte je povolit v obou složkách. Upozornění: zkušení uživatelé můžou využít výhod oprávnění, která tato zásada umožňuje změnit jejich oprávnění a získat trvalý přístup k souborům a složkám s omezeným přístupem. Verze konfigurace tohoto nastavení zásad uživatele není zaručená zabezpečení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067134)

  **Výchozí**: Ano

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Blokovat hru DVR (jenom Desktop)**:  
  Konfiguruje, zda je povoleno nahrávání a vysílání her.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067056)

  **Výchozí**: Ano

## <a name="auto-play"></a>Automatické přehrávání

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – automatické přehrávání](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-autoplay) .

- **Automatické přehrání výchozího chování při automatickém spuštění**:  
  Toto nastavení má vliv na výchozí chování pro příkazy automatického spouštění. Příkazy automatického spuštění jsou uložené v souborech Autorun. inf a můžou spouštět instalační programy nebo jiné rutiny. Pokud je tato možnost *povolená*, můžou správci změnit výchozí chování při automatickém spouštění na zařízení, na kterém běží Windows Vista nebo novější. Chování může být nastaveno na: a) zcela zakázat příkazy Autorun nebo b) vrátit se zpátky k chování Pre-Windows Vista s automatickým spuštěním příkazu Autorun. Pokud je nastavené na *zakázáno* nebo *není nakonfigurováno*, zařízení se systémem Windows Vista nebo novějším vyzvat uživatele k zadání, zda má být spuštěn příkaz Autorun.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067133)

  **Výchozí**: nespouštět

- **Režim automatického přehrávání**:  
  Toto nastavení zásad umožňuje vypnout funkci automatického přehrávání. Automatické přehrávání začne číst z jednotky hned po vložení média do jednotky. V důsledku toho se hned spustí instalační soubor programů a hudba na zvukovém médiu. V systému Windows XP SP2 a starších verzích je automatické přehrávání ve výchozím nastavení zakázáno na vyměnitelných jednotkách, například na disketové jednotce (nikoli na jednotce CD-ROM) a na síťových jednotkách. Od verze Windows XP SP2 je automatické přehrávání povolené pro vyměnitelné jednotky, včetně jednotek zip a některých velkokapacitních paměťových zařízení USB. Pokud nastavení této zásady povolíte, bude automatické přehrávání na discích CD-ROM a na vyměnitelných jednotkách nebo na všech jednotkách zakázané. Nastavením této zásady zakážete automatické přehrávání na dalších typech jednotek. Toto nastavení nemůžete použít, pokud chcete povolit automatické přehrávání na jednotkách, na kterých je ve výchozím nastavení zakázané. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, bude povoleno automatické přehrávání. Poznámka: nastavení této zásady se zobrazuje jak v konfiguraci počítače, tak ve složkách Konfigurace uživatele. Pokud dojde ke konfliktu nastavení zásad, nastavení zásad v konfiguraci počítače má přednost před nastavením zásad v konfiguraci uživatele.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2066793)

  **Výchozí**: zakázáno

- **Blokovat automatické přehrávání u zařízení bez svazků**:  
  Toto nastavení zásad nepovoluje automatické přehrávání pro zařízení MTP, jako jsou kamery nebo telefony. Pokud nastavení této zásady povolíte, funkce automatického přehrávání není povolená pro zařízení MTP, jako jsou kamery nebo telefony. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, bude pro zařízení bez svazků povolené automatické přehrávání.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067106)

  **Výchozí**: povoleno

## <a name="bitlocker"></a>BitLocker

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – BitLocker](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bitlocker) .

- **Zásada pro vyměnitelné jednotky BitLockeru**:  
  Toto nastavení zásad slouží k řízení metody šifrování a složitosti šifry. Hodnoty této zásady určují sílu šifry, kterou BitLocker používá k šifrování. Podniky můžou chtít řídit úroveň šifrování pro zvýšené zabezpečení (AES-256 je silnější než AES-128). Pokud povolíte toto nastavení, můžete nakonfigurovat šifrovací algoritmus a složitost klíče pro pevné datové jednotky, jednotky operačního systému a vyměnitelné datové jednotky. U pevných jednotek operačního systému doporučujeme použít algoritmus XTS-AES. U vyměnitelných jednotek byste měli použít algoritmus AES-CBC 128-bit nebo AES-CBC 256-bit, pokud se jednotka používá v jiných zařízeních, na kterých běží Windows 10, verze 1511 nebo novější. Změna metody šifrování nemá žádný vliv, pokud je jednotka již zašifrovaná nebo pokud probíhá šifrování. V těchto případech se nastavení této zásady ignoruje.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067140)

  Pro zásady vyměnitelné jednotky nástrojem BitLocker nakonfigurujte následující nastavení:

::: zone-end
::: zone pivot="mdm-may-2019"

  - **Zablokovat přístup pro zápis na vyměnitelné datové jednotky, které nechrání BitLocker**:  
    **Výchozí**: Ano

::: zone-end
::: zone pivot="mdm-preview"

  - **Vyžadovat šifrování pro přístup pro zápis**:  
    **Výchozí**: Ano

- **Zásada pro vyměnitelné jednotky BitLockeru**:  
  Toto nastavení zásad slouží k řízení metody šifrování a složitosti šifry. Hodnoty této zásady určují sílu šifry, kterou BitLocker používá k šifrování. Podniky můžou chtít řídit úroveň šifrování pro zvýšené zabezpečení (AES-256 je silnější než AES-128). Pokud povolíte toto nastavení, můžete nakonfigurovat šifrovací algoritmus a složitost klíče pro pevné datové jednotky, jednotky operačního systému a vyměnitelné datové jednotky. U pevných jednotek operačního systému doporučujeme použít algoritmus XTS-AES. U vyměnitelných jednotek byste měli použít algoritmus AES-CBC 128-bit nebo AES-CBC 256-bit, pokud se jednotka používá v jiných zařízeních, na kterých běží Windows 10, verze 1511 nebo novější. Změna metody šifrování nemá žádný vliv, pokud je jednotka již zašifrovaná nebo pokud probíhá šifrování. V těchto případech se nastavení této zásady ignoruje.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067140)

  Pro zásady vyměnitelné jednotky nástrojem BitLocker nakonfigurujte následující nastavení:

  - **Vyžadovat šifrování pro přístup pro zápis**:  
    **Výchozí**: Ano  

  - **Metoda šifrování**:  
    **Výchozí**: AES 256bit CBC  

- **Zásada pro pevný disk nástroje BitLocker**:  
  Toto nastavení zásad slouží k řízení metody šifrování a složitosti šifry. Hodnoty této zásady určují sílu šifry, kterou BitLocker používá k šifrování. Podniky můžou chtít řídit úroveň šifrování pro zvýšené zabezpečení (AES-256 je silnější než AES-128). Pokud povolíte toto nastavení, můžete nakonfigurovat šifrovací algoritmus a složitost klíče pro pevné datové jednotky, jednotky operačního systému a vyměnitelné datové jednotky. U pevných jednotek operačního systému doporučujeme použít algoritmus XTS-AES. U vyměnitelných jednotek byste měli použít algoritmus AES-CBC 128-bit nebo AES-CBC 256-bit, pokud se jednotka používá v jiných zařízeních, na kterých běží Windows 10, verze 1511 nebo novější. Změna metody šifrování nemá žádný vliv, pokud je jednotka již zašifrovaná nebo pokud probíhá šifrování. V těchto případech se nastavení této zásady ignoruje.

  V části zásady pevné jednotky BitLockeru nakonfigurujte následující nastavení:

  - **Metoda šifrování**:  
    **Výchozí**: AES 256bit XTS  

- **Zásada systémové jednotky nástroje BitLocker**:  
  Toto nastavení zásad slouží k řízení metody šifrování a složitosti šifry. Hodnoty této zásady určují sílu šifry, kterou BitLocker používá k šifrování. Podniky můžou chtít řídit úroveň šifrování pro zvýšené zabezpečení (AES-256 je silnější než AES-128). Pokud povolíte toto nastavení, můžete nakonfigurovat šifrovací algoritmus a složitost klíče pro pevné datové jednotky, jednotky operačního systému a vyměnitelné datové jednotky. U pevných jednotek operačního systému doporučujeme použít algoritmus XTS-AES. U vyměnitelných jednotek byste měli použít algoritmus AES-CBC 128-bit nebo AES-CBC 256-bit, pokud se jednotka používá v jiných zařízeních, na kterých běží Windows 10, verze 1511 nebo novější. Změna metody šifrování nemá žádný vliv, pokud je jednotka již zašifrovaná nebo pokud probíhá šifrování. V těchto případech se nastavení této zásady ignoruje.

  V části zásady systémové jednotky BitLockeru nakonfigurujte následující nastavení:

  - **Metoda šifrování**:  
    **Výchozí**: AES 256bit XTS

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

## <a name="browser"></a>Prohlížeč

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – prohlížeč](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser) .

- **Vyžadovat filtr SmartScreen pro Microsoft Edge**:  
  Microsoft Edge používá filtr SmartScreen v programu Microsoft Defender (zapnutý) k ochraně uživatelů před potenciálními podvodnými zprávami a škodlivým softwarem ve výchozím nastavení. Ve výchozím nastavení uživatelé také nemůžou zakázat (vypnout) filtr SmartScreen v programu Microsoft Defender. Povolením této zásady dojde k vypnutí filtru SmartScreen v programu Microsoft Defender a zabránění uživatelům v jeho zapnutí. Nekonfigurujte tuto zásadu, aby uživatelům umožnila zvolit nebo vypnout filtr SmartScreen v programu Microsoft Defender.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067029)

  **Výchozí**: Ano

- **Blokovat přístup ke škodlivému webu**:  
  Ve výchozím nastavení umožňuje Microsoft Edge uživatelům obejít (Ignorovat) upozornění filtru SmartScreen v programu Microsoft Defender týkající se potenciálně škodlivých webů, což jim umožní pokračovat v lokalitě. Pomocí této zásady můžete ale nakonfigurovat Microsoft Edge, aby uživatelé nemohli obejít upozornění, a zablokovat tak, aby pokračovali na tomto webu.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067040)
  
  **Výchozí**: Ano
  
- **Blokovat stahování neověřených souborů**:  
  Ve výchozím nastavení umožňuje Microsoft Edge uživatelům obejít (Ignorovat) upozornění filtru SmartScreen v programu Microsoft Defender týkající se potenciálně škodlivých souborů, což jim umožní pokračovat v stahování neověřených souborů. Když se tyto zásady povolí, zabráníte tak uživatelům v obcházení upozornění a znemožníte jim stahování neověřených souborů.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067023)
  
  **Výchozí**: Ano
  
- **Blokovat Správce hesel**:  
  Ve výchozím nastavení používá Microsoft Edge správce hesel automaticky a umožňuje uživatelům vytvářet hesla na základě místních správců. Zakázáním této zásady omezíte používání Správce hesel na Microsoft Edge. Tuto zásadu nekonfigurujte, pokud chcete uživatelům umožnit, aby ukládali a spravovali hesla místně pomocí Správce hesel.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067128)
  
  **Výchozí**: Ano
  
- **Zabránit uživateli v přepsání chyb certifikátu**:  
  Nastavení této zásady brání uživateli ignorovat SSL (Secure Sockets Layer)/TLS (Transport Layer Security), které přeruší procházení (například vypršela platnost, odvolaná zpráva nebo "Neshoda názvů") v aplikaci Internet Explorer. Pokud nastavení této zásady povolíte, uživatel nebude moci pokračovat v procházení. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, uživatel se může rozhodnout ignorovat chyby certifikátů a pokračovat v procházení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067126)
  
  **Výchozí**: Ano

## <a name="connectivity"></a>Připojení

Další informace najdete v dokumentaci k Windows v dokumentaci k [zásadě CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-connectivity) .

- **Blokovat stažení z Internetu pro publikování na webu a průvodce pro online řazení**:  
  Nastavení této zásady určuje, jestli má systém Windows stáhnout seznam poskytovatelů pro Průvodce pro publikování na webu a online řazení. Tito průvodci umožňují uživatelům vybrat ze seznamu společností, které poskytují služby, jako je online úložiště a fotografický tisk. Ve výchozím nastavení Windows zobrazuje kromě poskytovatelů uvedených v registru také poskytovatele stažené z webu Windows. Pokud nastavení této zásady povolíte, Windows nestáhne poskytovatele a jenom poskytovatele služeb, které jsou uložené v místním registru. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, zobrazí se seznam zprostředkovatelů, které se stáhnou, když uživatel použije průvodce publikováním na webu nebo online řazení. Další informace, které obsahují podrobnosti o určení poskytovatelů služeb v registru, najdete v dokumentaci pro Průvodce pro publikování na webu a online objednávky.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067136)
  
  **Výchozí**: povoleno

::: zone-end
::: zone pivot="mdm-may-2019"

- **Nakonfigurujte zabezpečený přístup k cestám UNC**:  
  Nastavením této zásady lze nakonfigurovat zabezpečený přístup k cestám UNC. Pokud tuto zásadu povolíte, systém Windows povolí přístup k zadaným cestám UNC jenom po splnění dalších požadavků na zabezpečení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067243)

  **Výchozí**: Nakonfigurujte systém Windows tak, aby povoloval přístup k zadaným cestám UNC jenom po splnění dalších požadavků na zabezpečení.

  Když *nakonfigurujete systém Windows tak, aby povoloval přístup k zadaným cestám UNC jenom po výběru splnění dalších požadavků na zabezpečení* , můžete nakonfigurovat *seznam pro zpřísněnou cestu UNC*.

  - **Seznam cest pro zpřísněnou cestu UNC**:  
    Vyberte **Přidat** a zadejte další příznaky zabezpečení a cesty k serveru.

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Blokovat stahování ovladačů tisku přes http**:  
  Nastavení této zásady určuje, jestli chcete, aby tento klient mohl stahovat balíčky ovladačů tiskáren přes HTTP. Aby bylo možné nastavit tisk přes protokol HTTP, je nutné stáhnout ovladače, které nejsou doručeny přes protokol HTTP. Poznámka: Toto nastavení zásad nebrání klientovi v tisku na tiskárny v intranetu ani na internetu přes HTTP. Zakazuje jenom stahování ovladačů, které ještě nejsou nainstalované místně. Pokud nastavení této zásady povolíte, nebude možné stáhnout ovladače tisku přes HTTP. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, uživatelé mohou stahovat ovladače tisku přes protokol HTTP.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067141)
  
  **Výchozí**: povoleno

## <a name="credentials-delegation"></a>Delegování přihlašovacích údajů

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – CredentialsDelegation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-credentialsdelegation) .

- **Delegování vzdáleného hostitele pro neexportované přihlašovací údaje**:  
  Vzdálený hostitel umožňuje delegování neexportovatelných přihlašovacích údajů. Při použití delegování přihlašovacích údajů zařízení poskytují exportovatelné verze přihlašovacích údajů ke vzdálenému hostiteli, který uživatelům zveřejňuje riziko krádeže přihlašovacích údajů od útočníků na vzdáleném hostiteli. Pokud nastavení této zásady povolíte, hostitel podporuje režim omezené správy nebo vzdáleného Credential Guard. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, režim omezené správy a ochrana před vzdáleným přihlašovacími údaji se nepodporuje. Uživatel bude vždycky muset předat přihlašovací údaje k hostiteli.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067103)
  
  **Výchozí**: povoleno

## <a name="credentials-ui"></a>Přihlašovací uživatelské rozhraní

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – CredentialsUI](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-credentialsui) .

- **Zobrazit výčet správců**:  
  Nastavení této zásady určuje, jestli se účty správců zobrazí, když se uživatel pokusí zvýšit úroveň spuštěné aplikace. Ve výchozím nastavení se účty správců nezobrazují, když se uživatel pokusí zvýšit úroveň spuštěné aplikace. Pokud nastavení této zásady povolíte, zobrazí se všechny účty místních správců v počítači, aby si uživatel mohl vybrat heslo a zadat správné heslo. Pokud nastavení této zásady zakážete, budou uživatelé vždycky muset zadat uživatelské jméno a heslo, aby se mohli zvýšit.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067021)

  **Výchozí**: zakázáno

## <a name="data-protection"></a>Ochrana dat

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – DataProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection) .

- **Zablokovat přímý přístup do paměti**:  
  Toto nastavení zásad umožňuje zablokovat přímý přístup do paměti (DMA) pro všechny horké porty PCI pro příjem po dobu, než se uživatel do Windows přihlásí. Jakmile se uživatel přihlásí, Windows Vypíše zařízení PCI připojená k portům plug-in hostitele PCI. Pokaždé, když uživatel zamkne počítač, je přímý přístup do zásuvky na konektorech PCI bez podřízených zařízení blokovaný, dokud se uživatel znovu nepřipojí. Zařízení, která už jsou ve výčtu, když se počítač odemkne, bude dál fungovat, dokud nebude odpojený. Nastavení této zásady se vynutilo jenom v případě, že je povolené BitLocker nebo šifrování zařízení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067031)

  **Výchozí**: Ano

## <a name="device-guard"></a>Ochrana zařízení

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – DeviceGuard](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-deviceguard) .

- **Zapnout ochranu Credential Guard**:  
  Toto nastavení umožňuje uživatelům zapnout ochranu Credential Guard se zabezpečením na základě virtualizace, které pomáhá chránit přihlašovací údaje při příštím restartování počítače.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067044)

  **Výchozí**: Povolit s ZÁMKem UEFI

::: zone-end
::: zone pivot="mdm-may-2019"

- **Zabezpečení na základě virtualizace**:  
  **Výchozí**: Povolit vbs s zabezpečeným spouštěním

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Povolit zabezpečení na základě virtualizace**:  
  Při příštím restartování zapne zabezpečení na základě virtualizace (VBS). Zabezpečení na základě virtualizace nabízí podporu služeb zabezpečení pomocí hypervisoru Windows.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067066)
  
  **Výchozí**: Ano

- **Spustit ochranu systému**:  
  **Výchozí**: povoleno

## <a name="device-installation"></a>Instalace zařízení

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – DeviceInstallation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-deviceinstallation) .

- **Instalace hardwarových zařízení podle identifikátorů zařízení**:  
  Toto nastavení zásad umožňuje zadat seznam technologie Plug and Play ID hardwaru a kompatibilní ID pro zařízení, na která systém Windows znemožňuje instalaci. Nastavení této zásady má přednost před jinými nastaveními zásad, která umožňují systému Windows nainstalovat zařízení. Pokud nastavení této zásady povolíte, Windows nemůže nainstalovat zařízení, jehož ID hardwaru nebo kompatibilní ID se zobrazí v seznamu, který vytvoříte. Pokud nastavení této zásady povolíte na vzdáleném počítači, nastavení zásad bude mít vliv na přesměrování zadaných zařízení z klienta vzdálené plochy na server vzdálené plochy. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, zařízení se můžou instalovat a aktualizovat tak, aby se povolila nebo zabránila jiným nastavením zásad.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2066794)

  **Výchozí**: blokovat instalaci hardwarového zařízení

  Když je vybraná možnost *blokovat instalaci hardwarového zařízení* , jsou k dispozici následující nastavení.

  - **Odebrat shodná hardwarová zařízení**:  
    Toto nastavení je dostupné, jenom když je *Instalace hardwarového zařízení podle identifikátorů zařízení* nastavená tak, aby *blokovala instalaci hardwarového zařízení*.

    **Výchozí**: Ano

  - **Blokované identifikátory hardwarových zařízení**:  
    Toto nastavení je dostupné, jenom když je *Instalace hardwarového zařízení podle identifikátorů zařízení* nastavená tak, aby *blokovala instalaci hardwarového zařízení*.

    **Výchozí**: Ano

- **Instalace hardwarových zařízení pomocí tříd instalace**:  
  Nastavení této zásady umožňuje zadat seznam globálně jedinečných identifikátorů (GUID) třídy nastavení zařízení pro ovladače zařízení, které systém Windows znemožňuje nainstalovat. Nastavení této zásady má přednost před jinými nastaveními zásad, která umožňují systému Windows nainstalovat zařízení. Pokud nastavení této zásady povolíte, Windows nemůže nainstalovat ani aktualizovat ovladače zařízení, jejichž identifikátory GUID třídy nastavení zařízení se zobrazí v seznamu, který vytvoříte. Pokud nastavení této zásady povolíte na vzdáleném počítači, nastavení zásad bude mít vliv na přesměrování zadaných zařízení z klienta vzdálené plochy na server vzdálené plochy. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, může systém Windows instalovat a aktualizovat zařízení podle povolených nebo zabránících jiným nastavením zásad.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067048)

  **Výchozí**: blokovat instalaci hardwarového zařízení

  Když je vybraná možnost *blokovat instalaci hardwarového zařízení* , jsou k dispozici následující nastavení.

  - **Odebrat shodná hardwarová zařízení**:  
    Toto nastavení je dostupné, jenom když je *Instalace hardwarového zařízení podle instalačních tříd* nastavená tak, aby *blokovala instalaci hardwarového zařízení*.

    **Výchozí**: *žádná výchozí konfigurace*

  - **Blokované identifikátory hardwarových zařízení**:  
    Toto nastavení je dostupné, jenom když je *Instalace hardwarového zařízení podle instalačních tříd* nastavená tak, aby *blokovala instalaci hardwarového zařízení*.

    **Výchozí**: *žádná výchozí konfigurace*

## <a name="device-lock"></a>Zámek zařízení

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – DeviceLock](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock) .

- **Zabránit použití kamery**:  
  Zakáže přepínač kamery zamykací obrazovky v nastavení počítače a zabraňuje tomu, aby se kamera vyvolala na zamykací obrazovce. Ve výchozím nastavení můžou uživatelé povolit vyvolání dostupné kamery na zamykací obrazovce. Pokud povolíte toto nastavení, uživatelé nebudou moci povolit ani zakázat přístup k fotoaparátu zamykací obrazovky v nastavení počítače a fotoaparát nelze vyvolat na zamykací obrazovce.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067052)

  **Výchozí**: povoleno

- **Vyžadovat heslo**:  
  Určuje, jestli je povolený zámek zařízení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067049)  

  **Výchozí**: Ano
  
  Pokud je možnost *vyžadovat heslo* nastavená na *hodnotu Ano*, jsou k dispozici následující nastavení.

  - **Minimální počet znakových sad pro heslo**:  
    Počet komplexních typů prvků (velká a malá písmena, číslice a interpunkční znaménka) vyžadované pro silný kód PIN nebo heslo. PIN kód vynutil následující chování pro stolní a mobilní zařízení: 1-číslice pouze 2 – číslice a malá písmena jsou vyžadována 3 číslicemi, malými písmeny a velkými písmeny. Nepodporováno v účtech Microsoft Desktop a doménových účtů. vyžadují se 4 číslice, malá písmena, Velká písmena a speciální znaky. Nepodporuje se v desktopu.  
    [Další informace](https://go.microsoft.com/fwlink/?linkid=2067055)

    **Výchozí hodnota**: 3

  - **Počet neúspěšných přihlášení před vymazáním zařízení**:  
    Počet povolených neúspěšných ověření, než se zařízení vymaže. Hodnota 0 zakáže funkci vymazání zařízení.  
    [Další informace](https://go.microsoft.com/fwlink/?linkid=2067030)

    **Výchozí**: 10  

  - **Vypršení platnosti hesla (dny)**:  
    Nastavení zásad maximální stáří hesla určuje, jak dlouho (ve dnech) se dá heslo použít, než systém vyžaduje, aby ho uživatel změnil. Můžete nastavit, aby platnost hesla vyprší po uplynutí počtu dní od 1 do 999, nebo můžete zadat, že hesla budou nikdy vypršet nastavením počtu dní na hodnotu 0. Pokud je maximální stáří hesla mezi 1 a 999 dny, minimální stáří hesla musí být kratší než maximální stáří hesla. Pokud je maximální stáří hesla nastavené na 0, minimální stáří hesla může být libovolná hodnota mezi 0 a 998 dny.  
    [Další informace](https://go.microsoft.com/fwlink/?linkid=2067028)

    **Výchozí**: 60

  - **Požadované heslo**:  
    Určuje typ kódu PIN nebo hesla, které se vyžaduje.  
    [Další informace](https://go.microsoft.com/fwlink/?linkid=2067027)

    **Výchozí**: alfanumerické

  - **Minimální délka hesla**:  
    Nastavení zásad minimální délky hesla určuje nejmenší počet znaků, které mohou vytvořit heslo pro uživatelský účet. Můžete nastavit hodnotu v rozmezí 1 až 14 znaků nebo můžete určit, že není vyžadováno žádné heslo nastavením počtu znaků na 0.  
    [Další informace](https://go.microsoft.com/fwlink/?linkid=2067024)

    **Výchozí**: 8

  - **Blokovat jednoduchá hesla**:  
    Určuje, jestli jsou povolené PIN kódy nebo hesla, jako je "1111" nebo "1234". Pro plochu také řídí použití hesel s obrázkem.  
    [Další informace](https://go.microsoft.com/fwlink/?linkid=2067127)

    **Výchozí**: Ano  
    *Nastavení Ano zabraňuje použití jednoduchých hesel.*

  - **Zakázat opakované použití předchozích hesel**:  
    Určuje, kolik hesel je uloženo v historii, kterou nelze použít. Hodnota zahrnuje aktuální heslo uživatele. Například když se nastaví hodnota *1* , nemůže uživatel při volbě nového hesla znovu použít svoje aktuální heslo. Nastavení *5* znamená, že uživatel nemůže nastavit nové heslo na aktuální heslo nebo předchozí čtyři hesla.  
    [Další informace](https://go.microsoft.com/fwlink/?linkid=2066795)

    **Výchozí hodnota**: 24

- **Zabránit zobrazení prezentace**:  
  Zakáže nastavení prezentace snímků zamykací obrazovky v nastavení počítače a zabrání přehrávání prezentace na zamykací obrazovce. Ve výchozím nastavení mohou uživatelé povolit zobrazení prezentace, které se spustí poté, co počítač zamkne. Pokud toto nastavení povolíte, uživatelé nebudou moct měnit nastavení prezentace v nastavení počítače a nebude možné spustit žádné zobrazení prezentace.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067105)

  **Výchozí**: povoleno  

  *Nastavení Enabled zabraňuje spuštění snímků.*

- **Minimální stáří hesla ve dnech**:  
  Nastavení zásad minimální stáří hesla určuje, jak dlouho (ve dnech) se musí heslo použít, než ho uživatel může změnit. Můžete nastavit hodnotu v rozmezí od 1 do 998 dnů nebo můžete změny hesel okamžitě zakázat nastavením počtu dnů na 0. Minimální stáří hesla musí být kratší než maximální stáří hesla, pokud je maximální stáří hesla nastaveno na hodnotu 0, což znamená, že hesla nebudou nikdy vypršet. Pokud je maximální stáří hesla nastavené na 0, minimální stáří hesla se dá nastavit na libovolnou hodnotu mezi 0 a 998.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067022)

  **Výchozí hodnota**: 1

::: zone-end
::: zone pivot="mdm-may-2019"

## <a name="dma-guard"></a>Ochrana DMA

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – DmaGuard](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard) .

- **Výčet externích zařízení nekompatibilních s režimem ochrany DMA v jádře**:  
  Cílem této zásady je zajistit další zabezpečení proti externímu zařízení podporujícím technologii DMA. Umožňuje lepší kontrolu nad výčtem externích zařízení s technologií DMA, která nejsou kompatibilní s přemapováním DMA/izolací paměti zařízení a sandboxing. Tato zásada se projeví jenom v případě, že je ochrana DMA pro jádro podporovaná a povolená systémovým firmwarem. Ochrana pomocí jádra DMA je funkce platformy, kterou nelze řídit pomocí zásad nebo koncového uživatele. Musí být podporován systémem v době výroby. Pokud chcete zjistit, jestli systém podporuje ochranu před nejenom jádrem, na stránce Souhrn v MSINFO32.exe ověřte pole ochrana jádra DMA.  
  [Další informace](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  **Výchozí**: Blokovat vše

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

## <a name="event-log-service"></a>Služba protokolu událostí

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – EventLogService](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-eventlogservice) .

- **Maximální velikost souboru protokolu zabezpečení v KB**:  
  Nastavení této zásady určuje maximální velikost souboru protokolu v kilobajtech. Pokud nastavení této zásady povolíte, můžete nakonfigurovat maximální velikost souboru protokolu na 1 megabajt (1024 kilobajtů) a 2 terabajty (2147483647 kilobajtů) v kilobajtech. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, bude maximální velikost souboru protokolu nastavena na místně konfigurovanou hodnotu. Tuto hodnotu může změnit místní správce pomocí dialogu Vlastnosti protokolu a výchozí hodnota je 20 megabajtů.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067042)

   **Výchozí**: 196608

- **Maximální velikost souboru protokolu systému v KB**:  
  Nastavení této zásady určuje maximální velikost souboru protokolu v kilobajtech. Pokud nastavení této zásady povolíte, můžete nakonfigurovat maximální velikost souboru protokolu na 1 megabajt (1024 kilobajtů) a 2 terabajty (2147483647 kilobajtů) v kilobajtech. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, bude maximální velikost souboru protokolu nastavena na místně konfigurovanou hodnotu. Tuto hodnotu může změnit místní správce pomocí dialogu Vlastnosti protokolu a výchozí hodnota je 20 megabajtů.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2066798)

  **Výchozí**: 32768

- **Maximální velikost souboru protokolu aplikace v KB**:  
  Nastavení této zásady určuje maximální velikost souboru protokolu v kilobajtech. Pokud nastavení této zásady povolíte, můžete nakonfigurovat maximální velikost souboru protokolu na 1 megabajt (1024 kilobajtů) a 2 terabajty (2147483647 kilobajtů) v kilobajtech. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, bude maximální velikost souboru protokolu nastavena na místně konfigurovanou hodnotu. Tuto hodnotu může změnit místní správce pomocí dialogu Vlastnosti protokolu a výchozí hodnota je 20 megabajtů.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067125)

  **Výchozí**: 32768

## <a name="experience"></a>Prostředí

Další informace najdete v dokumentaci k Windows v tématu [zásady pro poskytovatele cloudu](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience) .

- **Blokovat Windows Spotlight**:  
  Umožňuje správcům IT vypnout (blokovat) všechny funkce Windows Spotlightu. To zahrnuje i Windows Spotlight na zamykací obrazovce, tipy pro Windows, funkce Microsoftu pro uživatele a další související funkce.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067037)

  **Výchozí**: Ano

  Když je pro *blokování Windows Spotlight* nastavená možnost *není nakonfigurované*, Windows Spotlight se na zařízeních nezablokuje a pak můžete nakonfigurovat následující nastavení, aby se zablokovaly vybrané položky pro Windows Spotlight:

  - **Zablokovat návrhy třetích stran ve Windows Spotlightu**:  
    Určuje, jestli se mají povolit návrhy aplikací a obsahu od vydavatelů softwaru třetích stran ve funkcích Windows Spotlight, jako je Spotlight na zamykací obrazovce, navrhované aplikace v nabídce Start a tipy pro Windows. Uživatelé se pořád můžou podívat na návrhy funkcí, aplikací a služeb Microsoftu.  
    [Další informace](https://go.microsoft.com/fwlink/?linkid=2067045)

    **Výchozí**: Nenakonfigurováno

  - **Zablokovat funkce specifické pro uživatele**:  
    Umožňuje správcům IT zapnout prostředí, která jsou typicky jenom pro příjemce, jako jsou návrhy spuštění, oznámení o členství, instalace aplikace po POČÁTEČNÍm startu a přesměrovat dlaždice.  
    [Další informace](https://go.microsoft.com/fwlink/?linkid=2067054)

    **Výchozí**: Nenakonfigurováno

## <a name="exploit-guard"></a>Zneužití Guard

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – ExploitGuard](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-exploitguard) .

- **Nahrát XML**:  
  Umožňuje správci IT doručovat konfiguraci, která představuje požadované možnosti pro zmírnění rizika systému a aplikace pro všechna zařízení v organizaci. Konfigurace je reprezentovaná kódem XML. Ochrana před zneužitím pomáhá chránit zařízení před malwarem, který využívá zneužití k rozšíření a nakazit. Pomocí aplikace zabezpečení systému Windows nebo PowerShellu vytvoříte sadu zmírnění hrozeb (označované jako konfigurace). Tuto konfiguraci pak můžete exportovat jako soubor XML a sdílet ho s více počítači ve vaší síti, aby všichni měli stejnou sadu nastavení pro zmírnění rizik. Existující konfigurační soubor XML nástroje EMET můžete také převést a importovat do konfiguračního souboru XML ochrany před zneužitím.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067035)

  **Výchozí**: *je zadaný ukázkový kód XML* .

## <a name="file-explorer"></a>Průzkumník souborů

Další informace najdete v dokumentaci k systému Windows v tématu [zásady CSP – Průzkumník](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-fileexplorer) souborů.  

- **Zabránění spuštění dat blokování**:  
  Zakázání prevence spuštění dat může některé starší verze modulů plug-in umožňovat fungování bez ukončení Průzkumníka.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067043)  

  **Výchozí**: zakázáno

- **Zablokovat ukončení haldy při poškození**:  
  Vypnutí ukončení haldy při poškození může některým starším aplikacím modulu plug-in fungovat bez okamžitého ukončení Průzkumníka, i když se Průzkumník může stále neočekávaně ukončit později.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067107)

  **Výchozí**: zakázáno

## <a name="firewall"></a>Brána firewall

Další informace najdete v tématu [2.2.2 FW_PROFILE_TYPE]( https://docs.microsoft.com/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc) v dokumentaci k Windows Protocols.

- **Doména profilu brány firewall**:  
  Určuje profily, do kterých pravidlo patří: doména, soukromá, veřejná. Tato hodnota představuje profil pro sítě, které jsou připojené k doménám.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Blokovaná příchozí připojení**:  
    **Výchozí**: Ano

  - **Požadovaná odchozí připojení**:  
    **Výchozí**: Ano

  - **Blokovaná příchozí oznámení**:  
    **Výchozí**: Ano

  - **Povolená brána firewall**:  
    **Výchozí**: povoleno

- **Veřejný profil brány firewall**:  
  Určuje profily, do kterých pravidlo patří: doména, soukromá, veřejná. Tato hodnota představuje profil pro veřejné sítě. Tyto sítě jsou klasifikovány jako veřejné správci v hostiteli serveru. Klasifikace proběhne při prvním připojení hostitele k síti. Tyto sítě jsou obvykle na letištích, v kavárnách a na jiných veřejných místech, kde nejsou důvěryhodní partneři v síti nebo správci sítě.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Blokovaná příchozí připojení**:  
    **Výchozí**: Ano

  - **Požadovaná odchozí připojení**:  
    **Výchozí**: Ano

  - **Blokovaná příchozí oznámení**:  
    **Výchozí**: Ano

  - **Povolená brána firewall**:  
    **Výchozí**: povoleno

  - **Pravidla zabezpečení připojení ze zásad skupiny nejsou Sloučená**:  
    **Výchozí**: Ano

  - **Pravidla zásad ze zásad skupiny nejsou Sloučená**:  
    **Výchozí**: Ano

- **Profil brány firewall Private**:  
  Určuje profily, do kterých pravidlo patří: doména, soukromá, veřejná. Tato hodnota představuje profil privátních sítí.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Blokovaná příchozí připojení**:  
    **Výchozí**: Ano

  - **Požadovaná odchozí připojení**:  
    **Výchozí**: Ano

  - **Blokovaná příchozí oznámení**:  
    **Výchozí**: Ano

  - **Povolená brána firewall**:  
    **Výchozí**: povoleno

## <a name="internet-explorer"></a>Internet Explorer

Další informace najdete v dokumentaci k Windows v dokumentaci k [zásadě CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-internetexplorer) .

- **Aktualizace zóny s omezeným přístupem aplikace Internet Explorer na stavovém řádku prostřednictvím skriptu**:  
  Toto nastavení zásad umožňuje spravovat, jestli má skript povoleno aktualizovat stavový řádek v rámci zóny.

  - *Pokud nastavení této zásady povolíte*, můžou skripty aktualizovat stavový řádek.
  - *Pokud toto nastavení zásad zakážete nebo*nenakonfigurujete, skripty nemůžou aktualizovat stavový řádek.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067074)

  **Výchozí**: zakázáno

::: zone-end
::: zone pivot="mdm-may-2019"

- Internet **Explorer zóna Internet přetahováním nebo kopírováním a vkládáním souborů**:  
  Toto nastavení zásad umožňuje spravovat, jestli uživatelé můžou přetahovat soubory nebo kopírovat a vkládat soubory ze zdroje v rámci zóny. Pokud nastavení této zásady povolíte, budou uživatelé moci automaticky přetahovat soubory nebo kopírovat a vkládat soubory z této zóny. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, zobrazí se uživatelům dotaz, zda chcete soubory přetáhnout nebo zkopírovat z této zóny. Pokud nastavení této zásady zakážete, uživatelé nebudou moci přetahovat soubory nebo kopírovat a vkládat soubory z této zóny. Pokud nastavení této zásady nenakonfigurujete, uživatelé mohou automaticky přetahovat soubory nebo kopírovat a vkládat soubory z této zóny.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067076)

  **Výchozí**: zakázat

- **Zóna s omezeným přístupem v Internet exploreru .NET Framework závislé součásti**:  
  Pomocí tohoto nastavení zásad můžete spravovat, jestli .NET Framework součásti, které nejsou podepsané pomocí technologie Authenticode, se dají spouštět z Internet Exploreru. Mezi tyto komponenty patří spravované ovládací prvky, na které se odkazuje ze značky objektu a spravované spustitelné soubory, na které odkazuje odkaz. Pokud nastavení této zásady povolíte, bude aplikace Internet Explorer spouštět nepodepsané spravované součásti. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, Internet Explorer vyzve uživatele, aby určil, zda mají být spuštěny nepodepsané spravované součásti. Pokud nastavení této zásady zakážete, nebude aplikace Internet Explorer spouštět nepodepsané spravované součásti. Pokud nastavení této zásady nenakonfigurujete, nebude aplikace Internet Explorer spouštět nepodepsané spravované součásti.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067077)

  **Výchozí**: zakázat

- **Zóna místního počítače v aplikaci Internet Explorer nespouští Antimalwarový program proti ovládacím prvkům**ActiveX:  
  Nastavení této zásady určuje, jestli aplikace Internet Explorer spouští antimalwarové programy proti ovládacím prvkům ActiveX, aby zkontrolovala, jestli se dají bezpečně načíst na stránkách. Pokud nastavení této zásady povolíte, aplikace Internet Explorer nebude u antimalwarového programu kontrolovat, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Pokud nastavení této zásady zakážete, bude aplikace Internet Explorer vždy kontrolovat váš Antimalwarový program, aby bylo možné zjistit, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Pokud nastavení této zásady nenakonfigurujete, aplikace Internet Explorer nebude kontrolovat váš Antimalwarový program, aby bylo možné zjistit, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Uživatelé můžou toto chování zapnout nebo vypnout pomocí nastavení zabezpečení Internet Exploreru.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067152)

  **Výchozí**: zakázáno

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Přístup k internetovým zónám Internet Exploreru k datovým zdrojům**:  
  Toto nastavení zásad umožňuje spravovat, jestli Internet Explorer může získat přístup k datům z jiné zóny zabezpečení pomocí analyzátoru MSXML (Microsoft XML Parser) nebo rozhraní ADO (ActiveX Data Objects) (ADO). Pokud nastavení této zásady povolíte, uživatelé mohou načíst stránku v zóně, která používá MSXML nebo ADO pro přístup k datům z jiné lokality v zóně. Pokud v rozevíracím seznamu vyberete příkaz Dotázat se na uživatele, zobrazí se dotaz, jestli chcete, aby se stránka načetla do zóny, která používá MSXML nebo ADO pro přístup k datům z jiné lokality v zóně. Pokud nastavení této zásady zakážete, uživatelé nemůžou načíst stránku v zóně, která používá MSXML nebo ADO pro přístup k datům z jiné lokality v zóně. Pokud nastavení této zásady nenakonfigurujete, uživatelé nebudou moci načíst stránku v zóně, která používá MSXML nebo ADO pro přístup k datům z jiné lokality v zóně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067078)  

  **Výchozí**: zakázat

- **Zóna s omezeným přístupem v aplikaci Internet Explorer přetahování obsahu z různých domén v systému Windows**:  
  Toto nastavení zásad umožňuje nastavit možnosti pro přetahování obsahu z jedné domény do jiné domény, pokud je zdroj a cíl ve stejném okně. Pokud nastavení této zásady povolíte a kliknete na tlačítko Povolit, mohou uživatelé přetahovat obsah z jedné domény do jiné domény, když se zdroj a cíl nacházejí ve stejném okně. Uživatelé toto nastavení nemůžou změnit. Pokud nastavení této zásady povolíte a kliknete na zakázat, uživatelé nemůžou přetahovat obsah z jedné domény do jiné domény, pokud je zdroj a cíl ve stejném okně. Uživatelé nemůžou toto nastavení změnit v dialogovém okně Možnosti Internetu. Pokud v Internet Exploreru 10 toto nastavení zásad zakážete nebo nenakonfigurujete, uživatelé nemůžou přetahovat obsah z jedné domény do jiné domény, když se zdroj a cíl nacházejí ve stejném okně. Uživatelé můžou toto nastavení změnit v dialogovém okně Možnosti Internetu. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, uživatelé mohou v aplikaci Internet Explorer 9 a starších verzích přetahovat obsah z jedné domény do jiné domény, pokud je zdroj a cíl ve stejném okně. Uživatelé nemůžou toto nastavení změnit v dialogovém okně Možnosti Internetu.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067079)  

  **Výchozí**: zakázáno

- **Upozornění na nesoulad adres certifikátu Internet Exploreru**:  
  Toto nastavení zásad umožňuje zapnout upozornění zabezpečení neshody adres certifikátů. Pokud je nastavení této zásady zapnuté, bude uživatel upozorněn při návštěvě zabezpečených webů protokolu HTTP (HTTPS), které prezentují certifikáty vydané pro jinou adresu webu. Toto upozornění pomáhá zabránit útokům s falešnou identitou. Pokud nastavení této zásady povolíte, zobrazí se vždy upozornění neshoda adres certifikátu. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, uživatel může zvolit, zda se zobrazí upozornění neshoda adres certifikátu (pomocí stránky Upřesnit v ovládacím panelu Internet).  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067153)  

  **Výchozí**: povoleno

- **Méně privilegované lokality zóny s omezeným přístupem aplikace Internet Explorer**:  
  Toto nastavení zásad umožňuje spravovat, jestli weby z méně privilegovaných zón, jako jsou třeba internetové weby, můžou přejít do této zóny. Pokud nastavení této zásady povolíte, weby z méně privilegovaných zón můžou otevřít nová okna v systému nebo přejít do této zóny. Zóna zabezpečení se spustí bez přidané úrovně zabezpečení, která je k dispozici v rámci funkce zabezpečení z důvodu zvýšení úrovně ochrany zóny. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, uživateli se zobrazí upozornění, že dojde k potenciálně rizikové navigaci. Pokud nastavení této zásady zakážete, je možné, že bude znemožněna škodlivá navigace. Funkce zabezpečení aplikace Internet Explorer je v této zóně zapnutá na základě ochrany před řízením funkcí zvýšení úrovně zóny. Pokud nastavení této zásady nenakonfigurujete, je možné, že bude znemožněna škodlivá navigace. Funkce zabezpečení aplikace Internet Explorer je v této zóně zapnutá na základě ochrany před řízením funkcí zvýšení úrovně zóny.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067148)

  **Výchozí**: zakázat

- **Automatická výzva ke stažení souborů v zóně s omezeným přístupem aplikace Internet Explorer**:  
  Nastavení této zásady určuje, jestli se uživatelům zobrazí výzva k zadání souborů ke stažení, který není inicializovaný uživatelem. Bez ohledu na toto nastavení budou uživatelé dostávat dialogy pro stažení souborů pro uživatelem iniciované soubory ke stažení. Pokud povolíte toto nastavení, uživatelé obdrží dialog pro stažení souboru pro automatické pokusy o stažení. Pokud toto nastavení zakážete nebo nenakonfigurujete, soubory ke stažení, které nejsou inicializované uživatelem, se zablokují a uživatelům se zobrazí oznamovací panel místo dialogového okna pro stažení souboru. Uživatelé pak můžou kliknout na oznamovací pruh, aby se povolilo zobrazení výzvy ke stažení souboru.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067150)

  **Výchozí**: zakázáno

- Internet **Explorer Internet zone .NET Framework závislé součásti**:  
  Toto nastavení zásad umožňuje spravovat, jestli .NET Framework komponenty, které nejsou podepsané přes technologii Authenticode, se dají spouštět z Internet Exploreru. Mezi tyto komponenty patří spravované ovládací prvky, na které se odkazuje ze značky objektu a spravované spustitelné soubory, na které odkazuje odkaz. Pokud nastavení této zásady povolíte, bude aplikace Internet Explorer spouštět nepodepsané spravované součásti. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, Internet Explorer vyzve uživatele, aby určil, zda mají být spuštěny nepodepsané spravované součásti. Pokud nastavení této zásady zakážete, nebude aplikace Internet Explorer spouštět nepodepsané spravované součásti. Pokud nastavení této zásady nenakonfigurujete, bude aplikace Internet Explorer spouštět nepodepsané spravované součásti.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067073)

  **Výchozí**: zakázat

- **Internet Explorer Internet Zone povoluje pouze schválené domény, aby používaly ovládací prvky ovládacích prvků ActiveX ORS**:  
  Nastavení této zásady určuje, jestli uživatel může na webových stránkách spustit ovládací prvek ActiveX ORS. Pokud nastavení této zásady povolíte, ovládací prvek ActiveX ORS se nebude spouštět z webů v této zóně. Pokud nastavení této zásady zakážete, bude se ovládací prvek ORS aktivních X spouštět ze všech lokalit v této zóně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067151)

  **Výchozí**: povoleno

- **Spuštěná okna skriptu zóny s omezeným přístupem aplikace Internet Explorer**:  
  Toto nastavení zásad umožňuje spravovat omezení pro automaticky otevíraná okna spouštěná skriptem a okna, která obsahují nadpis a stavové řádky. Pokud nastavení této zásady povolíte, nebude se zabezpečení na této zóně vztahovat na Windows. Zóna zabezpečení se spouští bez přidané úrovně zabezpečení, kterou poskytuje tato funkce. Pokud nastavení této zásady zakážete, budou možné škodlivé akce obsažené v automaticky otevíraných oknech a oknech spouštěných skriptem, které obsahují název a stavové řádky, které nejdou spustit. Tato funkce zabezpečení aplikace Internet Explorer je v této zóně zapnutá nastavením řízení funkcí skriptovaná omezení zabezpečení systému Windows pro daný proces. Pokud nastavení této zásady nenakonfigurujete, možné škodlivé akce obsažené v automaticky otevíraných oknech a oknech spouštěných skriptem, které obsahují název a stavové řádky, nemůžou běžet. Tato funkce zabezpečení aplikace Internet Explorer je v této zóně zapnutá nastavením řízení funkcí skriptovaná omezení zabezpečení systému Windows pro daný proces.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067075)

  **Výchozí**: zakázáno

- **Internetová zóna Internet Exploreru zahrnuje místní cestu při nahrávání souborů na server**:  
  Nastavení této zásady určuje, jestli se mají odesílat informace o místní cestě, když uživatel nahrává soubor prostřednictvím formuláře HTML. Pokud se odesílají informace o místní cestě, můžou být některé informace neúmyslně odhaleny serveru. Například soubory odeslané z plochy uživatele mohou obsahovat uživatelské jméno jako součást cesty. Pokud toto nastavení zásad povolíte, odesílají se informace o cestě, když uživatel nahraje soubor prostřednictvím formuláře HTML. Pokud toto nastavení zásad zakážete, informace o cestě se odeberou, když uživatel nahraje soubor prostřednictvím formuláře HTML. Pokud nastavení této zásady nenakonfigurujete, může uživatel zvolit, zda budou informace o cestě odesílány při odeslání souboru prostřednictvím formuláře HTML. Ve výchozím nastavení jsou odesílány informace o cestě.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067072)

  **Výchozí**: zakázáno

- Aplikace **Internet Explorer zakazuje procesy v rozšířeném chráněném režimu**:  
  Nastavení této zásady určuje, jestli Internet Explorer 11 používá 64 procesy (pro vyšší zabezpečení) nebo 32 procesy (pro zajištění vyšší kompatibility) při spuštění v rozšířeném chráněném režimu na 64 bitových verzí Windows. Důležité: některé ovládací prvky ActiveX a panely nástrojů nemusí být k dispozici, když se používají 64 procesy. Pokud toto nastavení zásad povolíte, bude aplikace Internet Explorer 11 při spuštění v rozšířeném chráněném režimu na 64 verzích systému Windows používat 64 procesů na kartě bitů. Pokud toto nastavení zásad zakážete, bude aplikace Internet Explorer 11 při spuštění v rozšířeném chráněném režimu na 64 verzích systému Windows používat 32 procesů na kartě bitů. Pokud nastavení této zásady nenakonfigurujete, uživatelé mohou tuto funkci zapnout nebo vypnout pomocí nastavení aplikace Internet Explorer. Tato funkce je ve výchozím nastavení vypnutá.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067149)

  **Výchozí**: povoleno

- **Ignorovat chyby certifikátů v Internet Exploreru**:  
  Nastavení této zásady brání uživateli ignorovat SSL (Secure Sockets Layer)/TLS (Transport Layer Security), které přeruší procházení (například vypršela platnost, odvolaná zpráva nebo "Neshoda názvů") v aplikaci Internet Explorer. Pokud nastavení této zásady povolíte, uživatel nebude moci pokračovat v procházení. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, uživatel může ignorovat chyby certifikátů a pokračovat v procházení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067071)

  **Výchozí**: zakázáno

- **Načítání souborů XAML v internetové zóně Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat načítání souborů jazyk Extensible Application Markup Language (XAML) (XAML). XAML je deklarativní značkovací jazyk založený na jazyce XML, který se běžně používá k vytváření bohatých uživatelských rozhraní a grafiky, které využívají Windows Presentation Foundation. Pokud nastavení této zásady povolíte a nastavíte rozevírací nabídku na povolit, soubory XAML se automaticky načtou v aplikaci Internet Explorer. Uživatel nemůže toto chování změnit. Pokud nastavíte rozevírací seznam na dotazování, uživateli se zobrazí výzva k načtení souborů XAML. Pokud toto nastavení zásad zakážete, soubory XAML nejsou načteny do aplikace Internet Explorer. Uživatel nemůže toto chování změnit. Pokud nastavení této zásady nenakonfigurujete, uživatel se může rozhodnout, zda mají být soubory XAML načteny v aplikaci Internet Explorer.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067147)

  **Výchozí**: zakázat

::: zone-end
::: zone pivot="mdm-may-2019"

- **Automaticky vyzvat k stahování souborů v internetové zóně Internet Exploreru**:  
  Nastavení této zásady určuje, jestli se uživatelům zobrazí výzva k zadání souborů ke stažení, který není inicializovaný uživatelem. Bez ohledu na toto nastavení budou uživatelé dostávat dialogy pro stažení souborů pro uživatelem iniciované soubory ke stažení. Pokud povolíte toto nastavení, uživatelé obdrží dialog pro stažení souboru pro automatické pokusy o stažení. Pokud toto nastavení zakážete nebo nenakonfigurujete, soubory ke stažení, které nejsou inicializované uživatelem, se zablokují a uživatelům se zobrazí oznamovací panel místo dialogového okna pro stažení souboru. Uživatelé pak můžou kliknout na oznamovací pruh, aby se povolilo zobrazení výzvy ke stažení souboru.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067117)

  **Výchozí**: zakázáno

::: zone-end
::: zone pivot="mdm-preview"

- **Automaticky vyzvat k stahování souborů v internetové zóně Internet Exploreru**:  
  Nastavení této zásady určuje, jestli se uživatelům zobrazí výzva k zadání souborů ke stažení, který není inicializovaný uživatelem. Bez ohledu na toto nastavení budou uživatelé dostávat dialogy pro stažení souborů pro uživatelem iniciované soubory ke stažení. Pokud povolíte toto nastavení, uživatelé obdrží dialog pro stažení souboru pro automatické pokusy o stažení. Pokud toto nastavení zakážete nebo nenakonfigurujete, soubory ke stažení, které nejsou inicializované uživatelem, se zablokují a uživatelům se zobrazí oznamovací panel místo dialogového okna pro stažení souboru. Uživatelé pak můžou kliknout na oznamovací pruh, aby se povolilo zobrazení výzvy ke stažení souboru.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067117)

  **Výchozí**: povoleno

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Upozornění zabezpečení zóny s omezeným přístupem aplikace Internet Explorer pro potenciálně nebezpečné soubory**:  
  Toto nastavení zásad určuje, jestli se při pokusu uživatele o otevření spustitelných souborů nebo jiných potenciálně nebezpečných souborů (z intranetového sdílení souborů pomocí Průzkumníka souborů) zobrazí zpráva "otevření souboru – upozornění zabezpečení". Pokud nastavení této zásady povolíte a nastavíte rozevírací nabídku na povolit, tyto soubory se otevřou bez upozornění zabezpečení. Pokud nastavíte rozevírací seznam na dotazování, zobrazí se před otevřením souborů upozornění zabezpečení. Pokud nastavení této zásady zakážete, tyto soubory se neotevřou. Pokud nastavení této zásady nenakonfigurujete, může uživatel nakonfigurovat, jak tento počítač zpracovává tyto soubory. Ve výchozím nastavení jsou tyto soubory zablokované v zóně s omezeným přístupem, které jsou povolené v zónách intranetu a místní počítač, a nastavte, aby se zobrazila výzva v Internetu a v důvěryhodných zónách.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2066797)

  **Výchozí**: zakázat

- **Filtr skriptování mezi weby internetové zóny Internet Exploreru**:  
  Tato zásada řídí, zda filtr skriptování mezi weby (XSS) detekuje a zabraňuje vkládání skriptu mezi weby do webů v této zóně. Pokud toto nastavení zásad povolíte, bude filtr XSS zapnut pro weby v této zóně a filtr XSS se pokusí zablokovat vkládání skriptu mezi weby. Pokud toto nastavení zásad zakážete, je filtr XSS pro weby v této zóně vypnutý a Internet Explorer povoluje vkládání skriptů mezi weby.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067053)

  **Výchozí**: povoleno

- Přechod **do SSL3 v aplikaci Internet Explorer**:  
  Toto nastavení zásad umožňuje zablokovat nezabezpečený přechod na SSL 3,0. Pokud je tato zásada povolená, Internet Explorer se pokusí připojit k webům pomocí protokolu SSL 3,0 nebo níže, když se TLS 1,0 nebo novější nezdaří. Aby nedocházelo k útokům prostředníkem, doporučujeme Nepovolit nezabezpečený záložní přechod. Tato zásada nemá vliv na to, které protokoly zabezpečení jsou povolené. Pokud tuto zásadu zakážete, použijí se výchozí nastavení systému.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067118)

  **Výchozí**: žádné lokality

::: zone-end
::: zone pivot="mdm-may-2019"

- **Podpora šifrování v aplikaci Internet Explorer**:  
  Toto nastavení zásad umožňuje vypnout podporu protokolu TLS (Transport Layer Security) 1,0, TLS 1,1, TLS 1,2, SSL (Secure Sockets Layer) (SSL) 2,0 nebo SSL 3,0 v prohlížeči. TLS a SSL jsou protokoly, které vám pomůžou chránit komunikaci mezi prohlížečem a cílovým serverem. Když se prohlížeč pokusí nastavit chráněnou komunikaci s cílovým serverem, prohlížeč a server vyjednají, který protokol a verze se mají použít. Prohlížeč a server se snaží porovnat seznam podporovaných protokolů a verzí každého druhého a vybere upřednostňovanou shodu. Pokud nastavení této zásady povolíte, bude prohlížeč vyjednávat šifrovací tunel pomocí metod šifrování, které vyberete v rozevíracím seznamu, nebo vyjednávat. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, uživatel může vybrat metodu šifrování, kterou prohlížeč podporuje.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067057)

  **Výchozí**: 2 položky: TLS v 1.1 a TLS v 1.2  
  *Výběrem šipky dolů zobrazíte možnosti, které můžete pro toto nastavení vybrat.*

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Internet Explorer uzamkl inteligentní obrazovka internetové zóny**:  
  Nastavení této zásady určuje, zda bude filtr SmartScreen kontrolovat stránky v této zóně na škodlivý obsah. Pokud toto nastavení zásad povolíte, vyhledá filtr SmartScreen stránky v této zóně pro škodlivý obsah. Pokud nastavení této zásady zakážete, filtr SmartScreen nebude skenovat stránky v této zóně pro škodlivý obsah. Pokud nastavení této zásady nenakonfigurujete, uživatel může zvolit, zda má filtr SmartScreen kontrolovat stránky v této zóně pro škodlivý obsah. Poznámka: v Internet Exploreru 7 Toto nastavení zásad určuje, jestli má filtr útoků phishing kontrolovat stránky v této zóně pro škodlivý obsah.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067059)

  **Výchozí**: povoleno

- **Zóna s omezeným přístupem Internet Exploreru spouští aplikace a soubory v prvku IFRAME**:  
  Toto nastavení zásad umožňuje spravovat, jestli můžou být aplikace spuštěné, a z odkazu na IFRAME v HTML stránek v této zóně se můžou stahovat soubory. Pokud nastavení této zásady povolíte, můžou uživatelé spouštět aplikace a stahovat soubory z IFRAME na stránkách v této zóně bez zásahu uživatele. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, zobrazí se uživatelům dotaz, zda chcete spouštět aplikace a stahovat soubory z prvků IFRAME na stránkách v této zóně. Pokud nastavení této zásady zakážete, uživatelé nebudou moci spouštět aplikace a stahovat soubory z prvků IFRAME na stránkách v této zóně. Pokud nastavení této zásady nenakonfigurujete, uživatelé nebudou moci spouštět aplikace a stahovat soubory z prvků IFRAME na stránkách v této zóně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067061)

  **Výchozí**: zakázat

- **Internet Explorer obejít upozornění na inteligentní obrazovku na Neběžné soubory**:  
  Nastavení této zásady určuje, jestli uživatel může obejít upozornění z filtru SmartScreen. Filtr SmartScreen uživatele upozorní na spustitelné soubory, které uživatelé Internet Exploreru nestahují běžným z Internetu. Pokud toto nastavení zásad povolíte, upozornění filtru SmartScreen blokují uživatele. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, může uživatel obejít upozornění filtru SmartScreen.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067068)

  **Výchozí**: zakázáno

- **Blokování automaticky otevíraných oken internetové zóny Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat, jestli se zobrazí nežádoucí automaticky otevíraná okna. Automaticky otevíraná okna, která se otevřou, když koncový uživatel klikne na odkaz, se nezablokuje. Pokud nastavení této zásady povolíte, nebudete moci zobrazovat většinu nežádoucích překryvných oken. Pokud nastavení této zásady zakážete, automaticky otevíraná okna se nebudou bránit v zobrazování. Pokud nastavení této zásady nenakonfigurujete, nebudete moci zobrazovat většinu nežádoucích překryvných oken.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067069)

  **Výchozí**: Povolit

- **Aplikace Internet Explorer zpracovává konzistentní zpracování MIME**:  
  Internet Explorer obsahuje dynamické binární chování: komponenty, které zapouzdřují konkrétní funkce pro prvky HTML, ke kterým jsou připojené. Nastavení této zásady určuje, jestli se má zakázat nebo povolit nastavení omezení zabezpečení binárního chování. Pokud nastavení této zásady povolíte, binární chování se zabrání pro procesy v Průzkumníkovi souborů a v aplikaci Internet Explorer. Pokud toto nastavení zásad zakážete, pro procesy Průzkumníka souborů a aplikace Internet Explorer jsou povoleny binární chování. Pokud nastavení této zásady nenakonfigurujete, binární chování se zabrání pro procesy v Průzkumníkovi souborů a v aplikaci Internet Explorer.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067144)  

  **Výchozí**: povoleno

- **Oprávnění pro přístup k zóně Java v Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat oprávnění pro aplety v jazyce Java. Pokud nastavení této zásady povolíte, můžete v rozevíracím seznamu zvolit možnosti. Vlastní pro řízení nastavení oprávnění individuálně. Nízké zabezpečení umožňuje apletům provádět všechny operace. Střední zabezpečení umožňuje apletům běžet v izolovaném prostoru (sandboxu) (oblast v paměti mimo rámec toho, že program nemůže provádět volání) a navíc funkce, jako je například pomocné místo (bezpečná a zabezpečená oblast úložiště v klientském počítači) a uživatelem řízený vstup/výstup souborů. Vysoké zabezpečení umožňuje, aby se applety spouštěly v izolovaném prostoru. Zakáže Java, aby se zabránilo spuštění všech apletů. Pokud nastavení této zásady zakážete, aplety Java nepůjde spustit. Pokud nastavení této zásady nenakonfigurujete, aplety Java budou zakázané.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067132)

  **Výchozí**: zakázat Java

- **Ovládací prvky ActiveX aplikace Internet Explorer v chráněném režimu**:  
  Nastavení této zásady zabraňuje spuštění ovládacích prvků ActiveX v chráněném režimu, je-li povolen Rozšířený chráněný režim. Když má uživatel nainstalovaný ovládací prvek ActiveX, který není kompatibilní s rozšířeným chráněným režimem a web se pokusí načíst ovládací prvek, Internet Explorer uživatele upozorní a nabídne možnost spustit web v normálním chráněném režimu. Nastavení této zásady zakáže toto oznámení a vynutí spuštění všech webů v rozšířeném chráněném režimu. Rozšířený chráněný režim poskytuje dodatečnou ochranu před škodlivými weby pomocí 64 procesů na 64 verzích systému Windows. V počítačích s minimálně Windows 8 se v rozšířeném chráněném režimu taky omezují umístění, ze kterých může Internet Explorer číst v registru a v systému souborů. Pokud je povolen Rozšířený chráněný režim a uživatel se nachází na webu, který se pokusí načíst ovládací prvek ActiveX, který není kompatibilní se zapnutým rozšířeným chráněným režimem, Internet Explorer uživatele upozorní a nabídne možnost zakázat Rozšířený chráněný režim pro daný web. Pokud toto nastavení zásad povolíte, uživateli Internet Exploreru nebude umožněno zakázat Rozšířený chráněný režim. Všechny weby s chráněným režimem budou spouštěny v rozšířeném chráněném režimu. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, Internet Explorer upozorní uživatele a nabídne možnost spouštět weby s nekompatibilními ovládacími prvky ActiveX v normálním chráněném režimu.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067145)

  **Výchozí**: zakázáno

- **Načítání souborů XAML v zóně s omezeným přístupem v Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat načítání souborů jazyk Extensible Application Markup Language (XAML) (XAML). XAML je deklarativní značkovací jazyk založený na jazyce XML, který se běžně používá k vytváření bohatých uživatelských rozhraní a grafiky, které využívají Windows Presentation Foundation. Pokud nastavení této zásady povolíte a nastavíte rozevírací nabídku na povolit, soubory XAML se automaticky načtou v aplikaci Internet Explorer. Uživatel nemůže toto chování změnit. Pokud nastavíte rozevírací seznam na dotazování, uživateli se zobrazí výzva k načtení souborů XAML. Pokud toto nastavení zásad zakážete, soubory XAML nejsou načteny do aplikace Internet Explorer. Uživatel nemůže toto chování změnit. Pokud nastavení této zásady nenakonfigurujete, uživatel se může rozhodnout, zda mají být soubory XAML načteny v aplikaci Internet Explorer.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067070)

  **Výchozí**: zakázat

- **Aplikace Internet Explorer zpracovává omezení zabezpečení oken pomocí skriptů**:  
  Internet Explorer umožňuje skriptům otevírání, změny velikosti a přemístění oken různých typů prostřednictvím kódu programu. Funkce zabezpečení omezení okna omezuje místní okna a zakáže zobrazování skriptů v oknech, ve kterých se nezobrazuje název a stavové řádky uživatele nebo zakazují jiné tituly a stavy oken. Pokud nastavení této zásady povolíte, budou se v oknech s použitím skriptů pro všechny procesy omezovat. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, nezobrazí se v oknech s použitím skriptů.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067146)

  **Výchozí**: povoleno

- **Zóna s omezeným přístupem pro Internet Explorer spouští aktivní X ovládací prvky a moduly plug-in**  
  Toto nastavení zásad umožňuje spravovat, jestli se můžou ovládací prvky ActiveX a moduly plug-in spouštět na stránkách ze zadané zóny. Pokud nastavení této zásady povolíte, ovládací prvky a moduly plug-in se můžou spouštět bez zásahu uživatele. Pokud jste vybrali možnost zobrazit v rozevíracím seznamu, zobrazí se uživatelům výzva, aby zvolili, zda mají být ovládací prvky nebo modul plug-in spuštěny. Pokud nastavení této zásady zakážete, ovládací prvky a moduly plug-in se nebudou spouštět. Pokud nastavení této zásady nenakonfigurujete, nebudou moci ovládací prvky a moduly plug-in běžet.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067114)

  **Výchozí**: zakázat

- **Ovládací prvky pro omezený přístup k skriptům v Internet Exploreru označené jako bezpečné pro skriptování**:  
  Toto nastavení zásad umožňuje spravovat, jestli ovládací prvek ActiveX označený jako bezpečný pro skriptování může komunikovat se skriptem. Pokud nastavení této zásady povolíte, bude se interakce skriptu automaticky vyskytnout bez zásahu uživatele. Pokud v rozevíracím seznamu vyberete možnost Dotázat se na uživatele, zobrazí se dotaz, jestli chcete, aby byla povolena interakce skriptu. Pokud nastavení této zásady zakážete, nebude možné docházet k interakci skriptu. Pokud nastavení této zásady nenakonfigurujete, nebudete mít k interakci s skriptem zabráněno.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067062)

  **Výchozí**: zakázat

- **Možnosti přihlášení k zóně omezeného Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat nastavení možností přihlášení. Pokud nastavení této zásady povolíte, můžete si vybrat z následujících možností přihlášení.

  - *Anonymní* – pomocí anonymního přihlášení můžete zakázat ověřování protokolu HTTP a použít účet hosta pouze pro protokol CIFS (Common Internet File System).

  - *Výzva* – pomocí výzvy k zadání uživatelského jména a hesla můžete zadávat dotazy uživatelů na ID a hesla uživatelů. Po zadání dotazu na uživatele lze tyto hodnoty použít v tichém režimu pro zbytek relace.

  - *Automatické přihlašování pouze v zóně intranetu* – pomocí této možnosti můžete zadávat dotazy uživatelů na uživatelská ID a hesla v jiných zónách. Po zadání dotazu na uživatele lze tyto hodnoty použít v tichém režimu pro zbytek relace.

  - *Automatické přihlašování pomocí aktuálního uživatelského jména a hesla*– tuto možnost použijte, pokud se chcete pokusit přihlásit pomocí výzvy Windows NT Challenge Response (označované také jako ověřování NTLM). Pokud server podporuje reakci na výzvu systému Windows NT, přihlašování používá uživatelské jméno a heslo uživatele v síti pro přihlášení. Pokud server nepodporuje reakci Windows NT Challenge, je uživatel dotazován na zadání uživatelského jména a hesla.

  Pokud nastavení této zásady zakážete, přihlašování se nastaví na *Automatické přihlašování jenom v zóně intranetu*. Pokud nastavení této zásady nenakonfigurujete, přihlašování se nastaví tak, aby se *zobrazilo výzva k zadání* uživatelského jména a hesla.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067110)

  **Výchozí**: anonymní

- **Inicializace důvěryhodné zóny aplikace Internet Explorer a ovládací prvky skriptu aktivní X nejsou označeny jako bezpečné**:  
  Toto nastavení zásad umožňuje spravovat ovládací prvky ActiveX, které nejsou označeny jako bezpečné. Pokud nastavení této zásady povolíte, budou ovládací prvky ActiveX spouštěny, načteny s parametry a pomocí skriptů bez nastavení bezpečnosti objektů pro nedůvěryhodná data nebo skripty. Toto nastavení se nedoporučuje, s výjimkou zabezpečených a spravovaných zón. Toto nastavení způsobí, že budou inicializovány nebezpečné i bezpečné ovládací prvky a budou skriptované, ignorování ovládacích prvků ActiveX skriptu označených jako bezpečné pro možnost skriptování. Pokud nastavení této zásady povolíte a v rozevíracím seznamu vyberete možnost zobrazit výzvu, uživatelé se dotazují, jestli chcete ovládacímu prvku povolit načtení pomocí parametrů nebo skriptu. Pokud nastavení této zásady zakážete, nebudou se ovládací prvky ActiveX, které se dají bezpečně nastavit, načítat pomocí parametrů nebo skriptu. Pokud nastavení této zásady nenakonfigurujete, budou uživatelé dotazováni na to, zda má ovládací prvek načíst s parametry nebo pomocí skriptu.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067137)

  **Výchozí**: zakázat

- **Aplikace Internet Explorer kontroluje odvolání certifikátu serveru**:  
  Toto nastavení zásad umožňuje spravovat, jestli Internet Explorer bude kontrolovat stav odvolání certifikátů serverů. Certifikáty jsou odvolány, když jsou ohroženy nebo již nejsou platné, a tato možnost uživatelům chrání v odesílání důvěrných dat do webu, který může být podvodný nebo není zabezpečený. Pokud toto nastavení zásad povolíte, bude aplikace Internet Explorer kontrolovat, zda byly certifikáty serveru odvolány. Pokud nastavení této zásady zakážete, aplikace Internet Explorer nebude kontrolovat certifikáty serveru, aby zjistila, jestli se odvolala. Pokud nastavení této zásady nenakonfigurujete, nebude aplikace Internet Explorer kontrolovat certifikáty serveru, aby bylo možné zjistit, zda byly odvolány.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067046)

  **Výchozí**: povoleno

- **Méně privilegované weby Internet Exploreru Internet Zone**:  
  Toto nastavení zásad umožňuje spravovat, jestli weby z méně privilegovaných zón, jako jsou servery s omezeným přístupem, můžou přejít do této zóny. Pokud nastavení této zásady povolíte, weby z méně privilegovaných zón můžou otevřít nová okna v systému nebo přejít do této zóny. Zóna zabezpečení se spustí bez přidané úrovně zabezpečení, která je k dispozici v rámci funkce zabezpečení z důvodu zvýšení úrovně ochrany zóny. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, uživateli se zobrazí upozornění, že dojde k potenciálně rizikové navigaci. Pokud nastavení této zásady zakážete, je možné, že bude znemožněna škodlivá navigace. Funkce zabezpečení aplikace Internet Explorer je v této zóně zapnutá na základě ochrany před řízením funkcí zvýšení úrovně zóny. Pokud nastavení této zásady nenakonfigurujete, můžou weby z méně privilegovaných zón otevřít nová okna v systému nebo přejít do této zóny.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067109)

  **Výchozí**: zakázat

- **Stažení souborů zóny se zakázaným Internet Explorerem**:  
  Toto nastavení zásad umožňuje spravovat, jestli se mají v zóně povolit stahování souborů. Tato možnost je určena zónou stránky s odkazem způsobující stahování, nikoli zónou, ze které je soubor doručen. Pokud toto nastavení zásad povolíte, soubory je možné stáhnout ze zóny. Pokud nastavení této zásady zakážete, nebudou se soubory ze zóny stahovat. Pokud nastavení této zásady nenakonfigurujete, nebude možné soubory ze zóny stahovat.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067038)

  **Výchozí**: zakázat

- **Internetová zóna Internet Exploreru spouští .NET Framework závislé součásti podepsané pomocí technologie Authenticode**:  
  Toto nastavení zásad umožňuje spravovat, jestli .NET Framework součásti, které jsou podepsané pomocí technologie Authenticode, se dají spouštět z Internet Exploreru. Mezi tyto komponenty patří spravované ovládací prvky, na které se odkazuje ze značky objektu a spravované spustitelné soubory, na které odkazuje odkaz. Pokud toto nastavení zásad povolíte, aplikace Internet Explorer spustí podepsané spravované součásti. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, Internet Explorer vyzve uživatele, aby určil, zda mají být spuštěny podepsané spravované součásti. Pokud nastavení této zásady zakážete, aplikace Internet Explorer neprovede podepsané spravované součásti. Pokud nastavení této zásady nenakonfigurujete, aplikace Internet Explorer neprovede podepsané spravované součásti.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067033)

  **Výchozí**: zakázat

- **Internet Explorer zabraňuje instalaci aktivních X ovládacích prvků podle uživatele**:  
  Toto nastavení zásad umožňuje zabránit instalaci ovládacích prvků ActiveX na základě jednotlivých uživatelů. Pokud toto nastavení zásad povolíte, nebudete moct ovládací prvky ActiveX instalovat individuálně pro jednotlivé uživatele. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, bude možné ovládací prvky ActiveX nainstalovat na základě jednotlivých uživatelů.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067058)

  **Výchozí**: povoleno

- **Aplikace Internet Explorer zabraňuje správě filtru Smart Screen**:  
  Nastavení této zásady zabrání uživateli ve správě filtru SmartScreen, který uživatele upozorní, pokud je web, který navštíví, známý pro podvodné pokusy o shromáždění osobních údajů prostřednictvím "phishing" nebo je známý pro hostování malwaru. Pokud nastavení této zásady povolíte, nezobrazí se uživateli výzva k zapnutí filtru SmartScreen. Všechny webové adresy, které nejsou na seznamu povolených filtrů, se automaticky odesílají do Microsoftu bez vyzvání uživatele. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, uživateli se zobrazí výzva k rozhodnutí, zda zapnout filtr SmartScreen během prvního spuštění.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067135)

  **Výchozí**: Povolit

- **Aplikace Internet Explorer zpracovává funkci bezpečnosti zpracování dat v kódování MIME**:  
  Nastavení této zásady určuje, zda bude služba Internet Explorer MIME zabráněno povýšení souboru jednoho typu na více než nebezpečný typ souboru. Pokud nastavení této zásady povolíte, nebude se v kódování MIME nikdy propagovat soubor jednoho typu na více než nebezpečný typ souboru. Pokud nastavení této zásady zakážete, budou procesy aplikace Internet Explorer umožňovat, aby se pro určitý typ souboru s více než nebezpečným typem souborů mohl sledovat protokol MIME. Pokud nastavení této zásady nenakonfigurujete, nebude monitorování v kódování MIME nikdy podporovat soubor jednoho typu na více než nebezpečný typ souboru.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067124)

  **Výchozí**: povoleno

- **Stažení zóny s omezeným přístupem v aplikaci Internet Explorer: podepsané aktivní X ovládací prvky**:  
  Toto nastavení zásad umožňuje spravovat, jestli uživatelé můžou stahovat podepsané ovládací prvky ActiveX ze stránky v zóně. Pokud tuto zásadu povolíte, můžou uživatelé stahovat podepsané ovládací prvky bez zásahu uživatele. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, uživatelé se dotazují, zda mají stahovat ovládací prvky podepsané vydavateli, kteří nejsou považováni za důvěryhodné. Kód podepsaný důvěryhodnými vydavateli se tiše stáhne. Pokud nastavení zásad zakážete, nepůjde stáhnout podepsané ovládací prvky. Pokud nastavení této zásady nenakonfigurujete, budou se uživatelé dotazovat, zda mají stahovat ovládací prvky podepsané vydavateli, kteří nejsou považováni za důvěryhodné. Kód podepsaný důvěryhodnými vydavateli se tiše stáhne.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067120)

  **Výchozí**: zakázat

- **Automaticky dokončená aplikace Internet Explorer**:  
  Tato funkce automatického dokončování si může pamatovat a navrhovat uživatelská jména a hesla ve formulářích. Pokud povolíte toto nastavení, uživatel nemůže změnit uživatelské jméno a heslo ve formulářích nebo zobrazit výzvu k uložení hesel. Funkce automatického dokončování pro uživatelská jména a hesla ve formulářích je zapnutá. Rozhodněte, jestli se má vybrat výzva k uložení hesel. Pokud toto nastavení zakážete, uživatel nemůže změnit uživatelské jméno a heslo ve formulářích nebo zobrazit výzvu k uložení hesel. Funkce automatického dokončování pro uživatelská jména a hesla ve formulářích je vypnuta. Uživatel se taky nemůže rozhodnout, že se má zobrazit výzva k uložení hesel. Pokud toto nastavení nenakonfigurujete, bude mít uživatel volnost zapínat automatické dokončování pro uživatelské jméno a hesla ve formulářích a možnost zobrazovat výzvy k uložení hesel. Chcete-li tuto možnost zobrazit, uživatelé otevřou dialogové okno Možnosti Internetu, klikněte na kartu obsah a klikněte na tlačítko nastavení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067122)

  **Výchozí**: zakázáno

- **Internet Explorer Internet Zone umožňuje spuštění jazyka VBScript**:  
  Nastavení této zásady umožňuje určit, jestli se může VBScript spouštět na stránkách v určitých zónách Internet Exploreru. Mezi možnosti patří:

  - *Enable* – jazyk VBScript běží na stránkách v určitých zónách bez jakékoli interakce.

  - *Výzva* – zaměstnanci se zobrazí dotaz, jestli chcete, aby se v zóně spouštěl jazyk VBScript.

  - *Disable* – v zóně není možné spouštět skripty VBScript. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, VBScript se spustí bez jakékoli interakce v zadané zóně.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067119)

  **Výchozí**: zakázat

- **Zóna s omezeným přístupem v aplikaci Internet Explorer povoluje použít pouze schválené domény ovládací prvky ORS aktivní X**:  
  Nastavení této zásady určuje, jestli uživatel může na webových stránkách spustit ovládací prvek ActiveX ORS. Pokud nastavení této zásady povolíte, ovládací prvek ActiveX ORS se nebude spouštět z webů v této zóně. Pokud nastavení této zásady zakážete, bude se ovládací prvek ORS aktivních X spouštět ze všech lokalit v této zóně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067032)

  **Výchozí**: povoleno

- **Důvěryhodná zóna aplikace Internet Explorer neběží proti malwaru proti ovládacím prvkům**ActiveX:  
  Nastavení této zásady určuje, jestli aplikace Internet Explorer spouští antimalwarové programy proti ovládacím prvkům ActiveX, aby zkontrolovala, jestli se dají bezpečně načíst na stránkách. Pokud nastavení této zásady povolíte, aplikace Internet Explorer nebude u antimalwarového programu kontrolovat, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Pokud nastavení této zásady zakážete, bude aplikace Internet Explorer vždy kontrolovat váš Antimalwarový program, aby bylo možné zjistit, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Pokud nastavení této zásady nenakonfigurujete, bude aplikace Internet Explorer vždy kontrolovat váš Antimalwarový program, aby bylo možné zjistit, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Uživatelé můžou toto chování zapnout nebo vypnout pomocí nastavení zabezpečení Internet Exploreru.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067115)

  **Výchozí**: zakázáno

- **Oprávnění pro zónu místního počítače v Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat oprávnění pro aplety v jazyce Java. Pokud nastavení této zásady povolíte, můžete v rozevíracím seznamu zvolit možnosti. Vlastní pro řízení nastavení oprávnění individuálně. Nízké zabezpečení umožňuje apletům provádět všechny operace. Střední zabezpečení umožňuje apletům běžet v izolovaném prostoru (sandboxu) (oblast v paměti mimo rámec toho, že program nemůže provádět volání) a navíc funkce, jako je například pomocné místo (bezpečná a zabezpečená oblast úložiště v klientském počítači) a uživatelem řízený vstup/výstup souborů. Vysoké zabezpečení umožňuje, aby se applety spouštěly v izolovaném prostoru. Zakáže Java, aby se zabránilo spuštění všech apletů. Pokud nastavení této zásady zakážete, aplety Java nepůjde spustit. Pokud nastavení této zásady nenakonfigurujete, bude oprávnění nastaveno na střední úroveň zabezpečení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067113)

  **Výchozí**: zakázat Java

- **Intranetová zóna Internet Exploreru nespouští antimalware proti ovládacím prvkům Active X**:  
  Nastavení této zásady určuje, jestli aplikace Internet Explorer spouští antimalwarové programy proti ovládacím prvkům ActiveX, aby zkontrolovala, jestli se dají bezpečně načíst na stránkách. Pokud nastavení této zásady povolíte, aplikace Internet Explorer nebude u antimalwarového programu kontrolovat, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Pokud nastavení této zásady zakážete, bude aplikace Internet Explorer vždy kontrolovat váš Antimalwarový program, aby bylo možné zjistit, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Pokud nastavení této zásady nenakonfigurujete, aplikace Internet Explorer nebude kontrolovat váš Antimalwarový program, aby bylo možné zjistit, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Uživatelé můžou toto chování zapnout nebo vypnout pomocí nastavení zabezpečení Internet Exploreru.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067138)

  **Výchozí**: zakázáno

- **Skriptlety zóny s omezeným přístupem aplikace Internet Explorer**:  
  Toto nastavení zásad umožňuje spravovat, jestli může uživatel spustit skriptlety. Pokud nastavení této zásady povolíte, může uživatel spustit skriptlety. Pokud nastavení této zásady zakážete, nemůže uživatel spustit skriptlety. Pokud nastavení této zásady nenakonfigurujete, uživatel může povolit nebo zakázat skriptlety.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067112)

  **Výchozí**: zakázáno

- **Oznamovací panel procesů aplikace Internet Explorer**:  
  Toto nastavení zásad umožňuje spravovat, zda se má oznamovací panel zobrazovat pro procesy aplikace Internet Explorer při omezení instalace souboru nebo kódu. Ve výchozím nastavení se zobrazuje oznamovací panel pro procesy aplikace Internet Explorer. Pokud toto nastavení zásad povolíte, zobrazí se pro procesy aplikace Internet Explorer oznamovací panel. Pokud nastavení této zásady zakážete, nezobrazí se pro procesy aplikace Internet Explorer oznamovací panel. Pokud nastavení této zásady nenakonfigurujete, oznamovací panel se nezobrazí pro procesy aplikace Internet Explorer.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067139)

  **Výchozí**: povoleno

- **Stažení podepsaných ovládacích prvků ActiveX na internetovou zónu Internet Explorer**:  
  Toto nastavení zásad umožňuje spravovat, jestli uživatelé můžou stahovat podepsané ovládací prvky ActiveX ze stránky v zóně. Pokud tuto zásadu povolíte, můžou uživatelé stahovat podepsané ovládací prvky bez zásahu uživatele. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, uživatelé se dotazují, zda mají stahovat ovládací prvky podepsané vydavateli, kteří nejsou považováni za důvěryhodné. Kód podepsaný důvěryhodnými vydavateli se tiše stáhne. Pokud nastavení zásad zakážete, nepůjde stáhnout podepsané ovládací prvky. Pokud nastavení této zásady nenakonfigurujete, budou se uživatelé dotazovat, zda mají stahovat ovládací prvky podepsané vydavateli, kteří nejsou považováni za důvěryhodné. Kód podepsaný důvěryhodnými vydavateli se tiše stáhne.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067064)

  **Výchozí**: zakázat

- **Inteligentní obrazovka zóny s omezeným přístupem v Internet Exploreru**:  
  Nastavení této zásady určuje, zda bude filtr SmartScreen kontrolovat stránky v této zóně na škodlivý obsah. Pokud toto nastavení zásad povolíte, vyhledá filtr SmartScreen stránky v této zóně pro škodlivý obsah. Pokud nastavení této zásady zakážete, filtr SmartScreen nebude skenovat stránky v této zóně pro škodlivý obsah. Pokud nastavení této zásady nenakonfigurujete, uživatel může zvolit, zda má filtr SmartScreen kontrolovat stránky v této zóně pro škodlivý obsah. Poznámka: v Internet Exploreru 7 Toto nastavení zásad určuje, jestli má filtr útoků phishing kontrolovat stránky v této zóně pro škodlivý obsah.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067034)

  **Výchozí**: povoleno

- **Tlačítko pro odebrání spuštění aplikace Internet Explorer pro zastaralé ovládací prvky X s tímto časem**:  
  Toto nastavení zásad umožňuje zabránit uživatelům v prohlížení tlačítka Spustit tento čas a spouštět konkrétní zastaralé ovládací prvky ActiveX v aplikaci Internet Explorer. Pokud nastavení této zásady povolíte, nebudou se uživatelům zobrazovat tlačítka Spustit tento čas u zprávy s upozorněním, která se zobrazí, když Internet Explorer zablokuje zastaralý ovládací prvek ActiveX. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, uživatelům se zobrazí tlačítko Spustit tento čas u varovné zprávy, která se zobrazí, když aplikace Internet Explorer zablokuje zastaralý ovládací prvek ActiveX. Kliknutím na toto tlačítko umožníte uživateli spustit zastaralý ovládací prvek ActiveX jednou. Další informace najdete v tématu "zastaralé ovládací prvky ActiveX" v knihovně TechNet aplikace Internet Explorer.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067123)

  **Výchozí**: povoleno

- **Internetová zóna Internet Exploreru spouští aplikace a soubory v prvku IFRAME**:  
  Toto nastavení zásad umožňuje spravovat, jestli se můžou aplikace spouštět a jestli se můžou soubory stahovat z odkazu na IFRAME v HTML stránek v této zóně. Pokud nastavení této zásady povolíte, můžou uživatelé spouštět aplikace a stahovat soubory z IFRAME na stránkách v této zóně bez zásahu uživatele. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, zobrazí se uživatelům dotaz, zda chcete spouštět aplikace a stahovat soubory z prvků IFRAME na stránkách v této zóně. Pokud nastavení této zásady zakážete, uživatelé nebudou moci spouštět aplikace a stahovat soubory z prvků IFRAME na stránkách v této zóně. Pokud nastavení této zásady nenakonfigurujete, budou se uživatelé dotazovat, jestli chcete spouštět aplikace a stahovat soubory z IFRAME na stránkách v této zóně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067020)

  **Výchozí**: zakázat

- **Omezená zóna aplikace Internet Explorer navigace v oknech a v různých doménách**:  
  Toto nastavení zásad umožňuje nastavit možnosti pro přetahování obsahu z jedné domény do jiné domény, pokud je zdroj a cíl v různých oknech. Pokud nastavení této zásady povolíte a kliknete na tlačítko Povolit, mohou uživatelé přetahovat obsah z jedné domény do jiné domény, když se zdroj a cíl nacházejí v různých oknech. Uživatelé toto nastavení nemůžou změnit. Pokud nastavení této zásady povolíte a kliknete na zakázat, uživatelé nemůžou přetahovat obsah z jedné domény do jiné domény, pokud je zdroj i cíl v různých oknech. Uživatelé toto nastavení nemůžou změnit. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, uživatelé nebudou moci přetahovat obsah z jedné domény do jiné domény, pokud je zdroj a cíl v různých oknech, a to v aplikaci Internet Explorer 10. Uživatelé můžou toto nastavení změnit v dialogovém okně Možnosti Internetu. Pokud v aplikaci Internet Explorer 9 a starších verzích zakážete tuto zásadu nebo ji nenakonfigurujete, uživatelé mohou přetahovat obsah z jedné domény do jiné domény, pokud je zdroj a cíl v různých oknech. Uživatelé toto nastavení nemůžou změnit.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067050)

  **Výchozí**: zakázat

- **Inteligentní obrazovka internetové zóny Internet Exploreru**:  
  Nastavení této zásady určuje, zda bude filtr SmartScreen kontrolovat stránky v této zóně na škodlivý obsah. Pokud toto nastavení zásad povolíte, vyhledá filtr SmartScreen stránky v této zóně pro škodlivý obsah. Pokud nastavení této zásady zakážete, filtr SmartScreen nebude skenovat stránky v této zóně pro škodlivý obsah. Pokud nastavení této zásady nenakonfigurujete, uživatel může zvolit, zda má filtr SmartScreen kontrolovat stránky v této zóně pro škodlivý obsah. Poznámka: v Internet Exploreru 7 Toto nastavení zásad určuje, jestli má filtr útoků phishing kontrolovat stránky v této zóně pro škodlivý obsah.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067047)

  **Výchozí**: povoleno

- **Aplikace Internet Explorer uzamkl oprávnění pro přístup k důvěryhodné zóně Java**:  
  Toto nastavení zásad umožňuje spravovat oprávnění pro aplety v jazyce Java. Pokud nastavení této zásady povolíte, můžete v rozevíracím seznamu zvolit možnosti. Vlastní pro řízení nastavení oprávnění individuálně. Nízké zabezpečení umožňuje apletům provádět všechny operace. Střední zabezpečení umožňuje apletům běžet v izolovaném prostoru (sandboxu) (oblast v paměti mimo rámec toho, že program nemůže provádět volání) a navíc funkce, jako je například pomocné místo (bezpečná a zabezpečená oblast úložiště v klientském počítači) a uživatelem řízený vstup/výstup souborů. Vysoké zabezpečení umožňuje, aby se applety spouštěly v izolovaném prostoru. Zakáže Java, aby se zabránilo spuštění všech apletů. Pokud nastavení této zásady zakážete, aplety Java nepůjde spustit. Pokud nastavení této zásady nenakonfigurujete, aplety Java budou zakázané.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067142)

  **Výchozí**: zakázat Java

- **Aplikace Internet Explorer zkontroluje podpisy stažených programů**:  
  Toto nastavení zásad umožňuje spravovat, jestli Internet Explorer před stažením spustitelných programů kontroluje digitální podpisy (které identifikují vydavatele podepsaného softwaru a před tím, než je někdo změnil nebo neoprávněný) na počítačích uživatelů. Pokud nastavení této zásady povolíte, bude aplikace Internet Explorer kontrolovat digitální podpisy spustitelných programů a zobrazovat jejich identity před jejich stažením do uživatelských počítačů. Pokud nastavení této zásady zakážete, aplikace Internet Explorer nebude kontrolovat digitální podpisy spustitelných programů nebo zobrazovat jejich identity před jejich stažením do uživatelských počítačů. Pokud tuto zásadu nenakonfigurujete, aplikace Internet Explorer nebude kontrolovat digitální podpisy spustitelných programů nebo zobrazovat jejich identity před jejich stažením do uživatelských počítačů.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067051)

  **Výchozí**: povoleno

- **Skript omezeného skriptování v Internet Exploreru ovládacích prvků webového prohlížeče**:  
  Nastavení této zásady určuje, zda může stránka řídit vložené ovládací prvky WebBrowser prostřednictvím skriptu. Pokud nastavení této zásady povolíte, je povolený přístup ke skriptu ovládacího prvku WebBrowser. Pokud nastavení této zásady zakážete, nebude přístup k skriptu k ovládacímu prvku WebBrowser povolen. Pokud nastavení této zásady nenakonfigurujete, uživatel může povolit nebo zakázat přístup k skriptu ovládacímu prvku WebBrowser. Ve výchozím nastavení je přístup ke skriptu k ovládacímu prvku WebBrowser povolen pouze v zónách místní počítač a intranet.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067098)

  **Výchozí**: zakázáno

- **Filtr skriptování mezi weby zóny s omezeným přístupem v Internet Exploreru**:  
  Tato zásada řídí, zda filtr skriptování mezi weby (XSS) detekuje a zabraňuje vkládání skriptu mezi weby do webů v této zóně. Pokud toto nastavení zásad povolíte, bude filtr XSS zapnut pro weby v této zóně a filtr XSS se pokusí zablokovat vkládání skriptu mezi weby. Pokud toto nastavení zásad zakážete, je filtr XSS pro weby v této zóně vypnutý a Internet Explorer povoluje vkládání skriptů mezi weby.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067178)

  **Výchozí**: povoleno

- **Binární chování zóny omezeného Internet Exploreru a chování skriptu**:  
  Toto nastavení zásad umožňuje spravovat dynamické chování binárních souborů a skriptů: komponenty, které zapouzdřují konkrétní funkce pro prvky HTML, ke kterým byly připojeny. Pokud nastavení této zásady povolíte, budou k dispozici binární chování a chování skriptů. Pokud v rozevíracím seznamu vyberete schválit správce, jsou k dispozici pouze chování uvedená v chování schválená správcem v části binární chování zásady omezení zabezpečení. Pokud toto nastavení zásad zakážete, nebude binární a chování skriptu k dispozici, pokud aplikace neimplementují vlastního správce zabezpečení. Pokud nastavení této zásady nenakonfigurujete, nebude binární chování a chování skriptu k dispozici, pokud aplikace neimplementují vlastního správce zabezpečení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067224)

  **Výchozí**: zakázat

- **Ověření nastavení zabezpečení aplikace Internet Explorer**:  
  Nastavením této zásady dojde k vypnutí funkce kontroly nastavení zabezpečení, která kontroluje nastavení zabezpečení aplikace Internet Explorer a určí, kdy nastavení Internet Explorer ohroženo. Pokud nastavení této zásady povolíte, funkce je vypnutá. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, je tato funkce zapnutá.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067182)

  **Výchozí**: povoleno

- **Upozornění zabezpečení Internetové zóny Internet Exploreru pro potenciálně nebezpečné soubory**:  
  Toto nastavení zásad určuje, jestli se při pokusu uživatele o otevření spustitelných souborů nebo jiných potenciálně nebezpečných souborů (z intranetového sdílení souborů pomocí Průzkumníka souborů) zobrazí zpráva "otevření souboru – upozornění zabezpečení". Pokud nastavení této zásady povolíte a nastavíte rozevírací nabídku na povolit, tyto soubory se otevřou bez upozornění zabezpečení. Pokud nastavíte rozevírací seznam na dotazování, zobrazí se před otevřením souborů upozornění zabezpečení. Pokud nastavení této zásady zakážete, tyto soubory se neotevřou. Pokud nastavení této zásady nenakonfigurujete, může uživatel nakonfigurovat, jak tento počítač zpracovává tyto soubory. Ve výchozím nastavení jsou tyto soubory zablokované v zóně s omezeným přístupem, které jsou povolené v zónách intranetu a místní počítač, a nastavte, aby se zobrazila výzva v Internetu a v důvěryhodných zónách.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067204)

  **Výchozí**: dotázat se

- **Oprávnění pro intranetovou zónu v Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat oprávnění pro aplety v jazyce Java. Pokud nastavení této zásady povolíte, můžete v rozevíracím seznamu zvolit možnosti. Vlastní pro řízení nastavení oprávnění individuálně. Nízké zabezpečení umožňuje apletům provádět všechny operace. Střední zabezpečení umožňuje apletům běžet v izolovaném prostoru (sandboxu) (oblast v paměti mimo rámec toho, že program nemůže provádět volání) a navíc funkce, jako je například pomocné místo (bezpečná a zabezpečená oblast úložiště v klientském počítači) a uživatelem řízený vstup/výstup souborů. Vysoké zabezpečení umožňuje, aby se applety spouštěly v izolovaném prostoru. Zakáže Java, aby se zabránilo spuštění všech apletů. Pokud nastavení této zásady zakážete, aplety Java nepůjde spustit. Pokud nastavení této zásady nenakonfigurujete, bude oprávnění nastaveno na střední úroveň zabezpečení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067206)

  **Výchozí**: vysoká úroveň zabezpečení

- **Blokování zazastaralých aktivních X ovládacích prvků v aplikaci Internet Explorer**:  
  Nastavení této zásady určuje, jestli Internet Explorer blokuje určité zastaralé ovládací prvky ActiveX. Zastaralé ovládací prvky ActiveX nejsou nikdy blokované v zóně intranetu. Pokud nastavení této zásady povolíte, aplikace Internet Explorer zastaví blokování zastaralých ovládacích prvků ActiveX. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, bude aplikace Internet Explorer nadále blokovat určité zastaralé ovládací prvky ActiveX. Další informace najdete v tématu "zastaralé ovládací prvky ActiveX" v knihovně TechNet aplikace Internet Explorer.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067203)

  **Výchozí**: povoleno

- **Blokování automaticky otevíraných oken zóny s omezeným přístupem aplikace Internet Explorer**:  
  Toto nastavení zásad umožňuje spravovat, jestli se zobrazí nežádoucí automaticky otevíraná okna. Automaticky otevíraná okna, která se otevřou, když koncový uživatel klikne na odkaz, se nezablokuje. Pokud nastavení této zásady povolíte, nebudete moci zobrazovat většinu nežádoucích překryvných oken. Pokud nastavení této zásady zakážete, automaticky otevíraná okna se nebudou bránit v zobrazování. Pokud nastavení této zásady nenakonfigurujete, nebudete moci zobrazovat většinu nežádoucích překryvných oken.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067180)

  **Výchozí**: Povolit

- **Aplikace Internet Explorer zpracovává omezení zabezpečení protokolu MK**:  
  Nastavení zásad omezení zabezpečení protokolu MK omezuje prostor pro útoky tím, že brání protokolu MK. Prostředky hostované v protokolu MK nebudou úspěšné. Pokud nastavení této zásady povolíte, protokol MK se zabrání pro Průzkumníka souborů a Internet Explorer a prostředky hostované v protokolu v rámci služby MK nebudou úspěšné. Pokud nastavení této zásady zakážete, můžou aplikace používat rozhraní API protokolu MK. Prostředky hostované v protokolu MK budou fungovat pro procesy Průzkumníka souborů a Internet Exploreru. Pokud nastavení této zásady nenakonfigurujete, nebude možné v Průzkumníkovi souborů a v aplikaci Internet Explorer zabráněno protokolu MK a prostředky hostované v protokolu MK selžou.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067179)

  **Výchozí**: povoleno

- **Oprávnění pro důvěryhodnou zónu Java v Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat oprávnění pro aplety v jazyce Java. Pokud nastavení této zásady povolíte, můžete v rozevíracím seznamu zvolit možnosti. Vlastní pro řízení nastavení oprávnění individuálně. Nízké zabezpečení umožňuje apletům provádět všechny operace. Střední zabezpečení umožňuje apletům běžet v izolovaném prostoru (sandboxu) (oblast v paměti mimo rámec toho, že program nemůže provádět volání) a navíc funkce, jako je například pomocné místo (bezpečná a zabezpečená oblast úložiště v klientském počítači) a uživatelem řízený vstup/výstup souborů. Vysoké zabezpečení umožňuje, aby se applety spouštěly v izolovaném prostoru. Zakáže Java, aby se zabránilo spuštění všech apletů. Pokud nastavení této zásady zakážete, aplety Java nepůjde spustit. Pokud nastavení této zásady nenakonfigurujete, oprávnění je nastaveno na možnost nízká úroveň zabezpečení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067200)

  **Výchozí**: vysoká úroveň zabezpečení

- **Skriptování v zóně s omezeným přístupem aplikace Internet Explorer v apletech Java**:  
  Toto nastavení zásad umožňuje spravovat, jestli jsou aplety vystavené pro skripty v rámci zóny. Pokud toto nastavení zásad povolíte, skripty budou mít přístup k apletům automaticky bez zásahu uživatele. Pokud v rozevíracím seznamu vyberete možnost Dotázat se na uživatele, zobrazí se dotaz, jestli chcete, aby skripty mohly přistupovat k appletům. Pokud nastavení této zásady zakážete, budou se skripty bránit v přístupu k appletům. Pokud nastavení této zásady nenakonfigurujete, budou se skripty bránit v přístupu k appletům.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067202)

  **Výchozí**: zakázat

- **Aplikace Internet Explorer byla uzamčena s omezenou zónou oprávnění Java**:  
  Toto nastavení zásad umožňuje spravovat oprávnění pro aplety v jazyce Java. Pokud nastavení této zásady povolíte, můžete v rozevíracím seznamu zvolit možnosti. Vlastní pro řízení nastavení oprávnění individuálně. Nízké zabezpečení umožňuje apletům provádět všechny operace. Střední zabezpečení umožňuje apletům běžet v izolovaném prostoru (sandboxu) (oblast v paměti mimo rámec toho, že program nemůže provádět volání) a navíc funkce, jako je například pomocné místo (bezpečná a zabezpečená oblast úložiště v klientském počítači) a uživatelem řízený vstup/výstup souborů. Vysoké zabezpečení umožňuje, aby se applety spouštěly v izolovaném prostoru. Zakáže Java, aby se zabránilo spuštění všech apletů. Pokud nastavení této zásady zakážete, aplety Java nepůjde spustit. Pokud nastavení této zásady nenakonfigurujete, aplety Java budou zakázané.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067181)

  **Výchozí**: zakázat Java

- **Internetová zóna Internet Exploreru povoluje použití ovládacích prvků ActiveX pouze u schválených domén**:  
  Nastavení této zásady určuje, jestli se uživateli zobrazí výzva, aby se povolilo spouštění ovládacích prvků ActiveX na jiných webech, než na webu, který nainstaloval ovládací prvek ActiveX. Pokud nastavení této zásady povolíte, zobrazí se uživateli výzva před spuštěním ovládacích prvků ActiveX z webů v této zóně. Uživatel může zvolit, že se má ovládací prvek spouštět z aktuálního webu nebo ze všech lokalit. Pokud nastavení této zásady zakážete, uživatel nebude zobrazovat výzvu ActiveX pro jednotlivé lokality a ovládací prvky ActiveX lze spouštět ze všech lokalit v této zóně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067091)

  **Výchozí**: povoleno

- **Internet Explorer zahrnuje všechny síťové cesty**:  
  Internet Explorer zahrnuje všechny síťové cesty.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067090)

  **Výchozí**: zakázáno

- **Režim chráněný internetovou zónou Internet Exploreru**:  
  Toto nastavení zásad umožňuje zapnout chráněný režim. Chráněný režim pomáhá chránit Internet Explorer před zneužitím ohrožení zabezpečení tím, že snižuje umístění, do kterých aplikace Internet Explorer může zapisovat do registru a systému souborů. Pokud nastavení této zásady povolíte, je chráněný režim zapnutý. Uživatel nemůže vypnout chráněný režim. Pokud nastavení této zásady zakážete, je chráněný režim vypnutý. Uživatel nemůže zapnout chráněný režim. Pokud nastavení této zásady nenakonfigurujete, může uživatel zapnout nebo vypnout chráněný režim.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067171)

  **Výchozí**: Povolit

- **Inicializovat internetovou zónu Internet Explorer a skriptovat aktivní X ovládací prvky, které nejsou označeny jako bezpečné**:  
  Toto nastavení zásad umožňuje spravovat ovládací prvky ActiveX, které nejsou označeny jako bezpečné. Pokud nastavení této zásady povolíte, budou ovládací prvky ActiveX spouštěny, načteny s parametry a pomocí skriptů bez nastavení bezpečnosti objektů pro nedůvěryhodná data nebo skripty. Toto nastavení se nedoporučuje, s výjimkou zabezpečených a spravovaných zón. Toto nastavení způsobí, že budou inicializovány nebezpečné i bezpečné ovládací prvky a budou skriptované, ignorování ovládacích prvků ActiveX skriptu označených jako bezpečné pro možnost skriptování. Pokud nastavení této zásady povolíte a v rozevíracím seznamu vyberete možnost zobrazit výzvu, uživatelé se dotazují, jestli chcete ovládacímu prvku povolit načtení pomocí parametrů nebo skriptu. Pokud nastavení této zásady zakážete, nebudou se ovládací prvky ActiveX, které se dají bezpečně nastavit, načítat pomocí parametrů nebo skriptu. Pokud nastavení této zásady nenakonfigurujete, nebudou se ovládací prvky ActiveX, které se dají bezpečně nastavit, načítat pomocí parametrů nebo skriptu.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067170)

  **Výchozí**: zakázat

- **Aplikace Internet Explorer je uzamčena na inteligentní obrazovku zóny s omezeným přístupem**:  
  Nastavení této zásady určuje, zda bude filtr SmartScreen kontrolovat stránky v této zóně na škodlivý obsah. Pokud toto nastavení zásad povolíte, vyhledá filtr SmartScreen stránky v této zóně pro škodlivý obsah. Pokud nastavení této zásady zakážete, filtr SmartScreen nebude skenovat stránky v této zóně pro škodlivý obsah. Pokud nastavení této zásady nenakonfigurujete, uživatel může zvolit, zda má filtr SmartScreen kontrolovat stránky v této zóně pro škodlivý obsah. Poznámka: v Internet Exploreru 7 Toto nastavení zásad určuje, jestli má filtr útoků phishing kontrolovat stránky v této zóně pro škodlivý obsah.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067092)

  **Výchozí**: povoleno

- **Detekce selhání aplikace Internet Explorer**:  
  Toto nastavení zásad umožňuje spravovat funkci detekce chyb v doplňku pro správu. Pokud nastavení této zásady povolíte, dojde k chybě v aplikaci Internet Explorer v systému Windows XP Professional Service Pack 1 nebo starším, a to proto, aby bylo možné vyvolat Zasílání zpráv o chybách systému Windows. Všechna nastavení zásad pro Zasílání zpráv o chybách systému Windows nadále platí. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, funkce detekce chyb pro správu doplňku je funkční.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067094)

  **Výchozí**: zakázáno

- **Oprávnění Java pro internetovou zónu Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat oprávnění pro aplety v jazyce Java. Pokud nastavení této zásady povolíte, můžete v rozevíracím seznamu zvolit možnosti. Vlastní pro řízení nastavení oprávnění individuálně. Nízké zabezpečení umožňuje apletům provádět všechny operace. Střední zabezpečení umožňuje apletům běžet v izolovaném prostoru (sandboxu) (oblast v paměti mimo rámec toho, že program nemůže provádět volání) a navíc funkce, jako je například pomocné místo (bezpečná a zabezpečená oblast úložiště v klientském počítači) a uživatelem řízený vstup/výstup souborů. Vysoké zabezpečení umožňuje, aby se applety spouštěly v izolovaném prostoru. Zakáže Java, aby se zabránilo spuštění všech apletů. Pokud nastavení této zásady zakážete, aplety Java nepůjde spustit. Pokud nastavení této zásady nenakonfigurujete, bude oprávnění nastaveno na vysokou úroveň zabezpečení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067174)

  **Výchozí**: zakázat Java

- **Aktivní skriptování zóny omezeného Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat, jestli je na stránkách v zóně spuštěný Kód skriptu. Pokud toto nastavení zásad povolíte, bude možné automaticky spouštět kód skriptu na stránkách v zóně. Pokud v rozevíracím seznamu vyberete příkaz Dotázat se na uživatele, zobrazí se dotaz, jestli chcete, aby se na stránkách v zóně mohl spustit kód skriptu. Pokud nastavení této zásady zakážete, nebudete moci spouštět kód skriptu na stránkách v zóně. Pokud nastavení této zásady nenakonfigurujete, nebudete moci spouštět kód skriptu na stránkách v zóně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067172)

  **Výchozí**: zakázat

- **Možnosti přihlášení k internetové zóně Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat nastavení možností přihlášení. Pokud nastavení této zásady povolíte, můžete si vybrat z následujících možností přihlášení. Anonymní přihlášení za účelem zakázání ověřování HTTP a použití účtu hosta pouze pro protokol CIFS (Common Internet File System). Vyzvat k zadání uživatelského jména a hesla k dotazování uživatelů na ID a hesla uživatele Po zadání dotazu na uživatele lze tyto hodnoty použít v tichém režimu pro zbytek relace. Automatické přihlašování pouze v zóně intranetu pro dotazování uživatelů na ID uživatelů a hesla v jiných zónách. Po zadání dotazu na uživatele lze tyto hodnoty použít v tichém režimu pro zbytek relace. Automatické přihlášení pomocí aktuálního uživatelského jména a hesla k pokusu o přihlášení pomocí výzvy Windows NT Challenge Response (označované také jako ověřování NTLM). Pokud server podporuje reakci na výzvu systému Windows NT, přihlašování používá uživatelské jméno a heslo uživatele v síti pro přihlášení. Pokud server nepodporuje reakci Windows NT Challenge, je uživatel dotazován na zadání uživatelského jména a hesla. Pokud nastavení této zásady zakážete, přihlašování se nastaví na automatické přihlašování jenom v zóně intranetu. Pokud nastavení této zásady nenakonfigurujete, přihlašování se nastaví na automatické přihlašování jenom v intranetové zóně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067194)

  **Výchozí**: dotázat se

- **Zóna s omezeným přístupem pro Internet Explorer umožňuje spuštění jazyka VBScript**:  
  Toto nastavení zásad umožňuje spravovat, jestli se může VBScript spouštět na stránkách ze zadané zóny v Internet Exploreru. Pokud jste v rozevíracím seznamu vybrali možnost povolit, bude možné spustit jazyk VBScript bez zásahu uživatele. Pokud jste vybrali možnost zobrazit v rozevíracím seznamu, zobrazí se uživatelům výzva k výběru, zda má být spuštěn jazyk VBScript. Pokud jste v rozevíracím seznamu vybrali možnost zakázat, nebude možné spustit jazyk VBScript. Pokud nastavení této zásady nenakonfigurujete nebo zakážete, nebude se skript VBScript moci spustit.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067173)

  **Výchozí**: zakázat

- **Internetová zóna Internet Exploreru přetáhne obsah z různých domén v systému Windows**:  
  Toto nastavení zásad umožňuje nastavit možnosti pro přetahování obsahu z jedné domény do jiné domény, pokud je zdroj a cíl v různých oknech. Pokud nastavení této zásady povolíte a kliknete na tlačítko Povolit, mohou uživatelé přetahovat obsah z jedné domény do jiné domény, když se zdroj a cíl nacházejí v různých oknech. Uživatelé toto nastavení nemůžou změnit. Pokud nastavení této zásady povolíte a kliknete na zakázat, uživatelé nemůžou přetahovat obsah z jedné domény do jiné domény, pokud je zdroj i cíl v různých oknech. Uživatelé toto nastavení nemůžou změnit. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, uživatelé nebudou moci přetahovat obsah z jedné domény do jiné domény, pokud je zdroj a cíl v různých oknech, a to v aplikaci Internet Explorer 10. Uživatelé můžou toto nastavení změnit v dialogovém okně Možnosti Internetu. Pokud v aplikaci Internet Explorer 9 a starších verzích zakážete tuto zásadu nebo ji nenakonfigurujete, uživatelé mohou přetahovat obsah z jedné domény do jiné domény, pokud je zdroj a cíl v různých oknech. Uživatelé toto nastavení nemůžou změnit.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067093)

  **Výchozí**: zakázáno

- **Inicializovat intranetovou zónu v Internet Exploreru a skriptovat aktivní X ovládací prvky, které nejsou označené jako bezpečné**:  
  Toto nastavení zásad umožňuje spravovat ovládací prvky ActiveX, které nejsou označeny jako bezpečné. Pokud nastavení této zásady povolíte, budou ovládací prvky ActiveX spouštěny, načteny s parametry a pomocí skriptů bez nastavení bezpečnosti objektů pro nedůvěryhodná data nebo skripty. Toto nastavení se nedoporučuje, s výjimkou zabezpečených a spravovaných zón. Toto nastavení způsobí, že budou inicializovány nebezpečné i bezpečné ovládací prvky a budou skriptované, ignorování ovládacích prvků ActiveX skriptu označených jako bezpečné pro možnost skriptování. Pokud nastavení této zásady povolíte a v rozevíracím seznamu vyberete možnost zobrazit výzvu, uživatelé se dotazují, jestli chcete ovládacímu prvku povolit načtení pomocí parametrů nebo skriptu. Pokud nastavení této zásady zakážete, nebudou se ovládací prvky ActiveX, které se dají bezpečně nastavit, načítat pomocí parametrů nebo skriptu. Pokud nastavení této zásady nenakonfigurujete, nebudou se ovládací prvky ActiveX, které se dají bezpečně nastavit, načítat pomocí parametrů nebo skriptu.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067175)

  **Výchozí**: zakázat

- **Skříně pro stažení aplikace Internet Explorer**:  
  Nastavení této zásady zabrání uživateli v zahrnutí (příloh souborů) z informačního kanálu do počítače uživatele. Pokud nastavení této zásady povolíte, nemůže uživatel nastavit modul synchronizace informačního kanálu tak, aby stáhl skříňku prostřednictvím stránky vlastností informačního kanálu. Vývojář nemůže změnit nastavení stahování prostřednictvím rozhraní API informačního kanálu. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, může uživatel nastavit modul synchronizace informačního kanálu tak, aby stáhl skříňku prostřednictvím stránky vlastností informačního kanálu. Vývojář může změnit nastavení stahování prostřednictvím rozhraní API informačního kanálu.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067245)

  **Výchozí**: zakázáno

- **Stažení nepodepsaných ovládacích prvků Active X v Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat, jestli uživatelé můžou stahovat nepodepsané ovládací prvky ActiveX ze zóny. Takový kód je potenciálně škodlivý, zejména když přichází z nedůvěryhodné zóny. Pokud nastavení této zásady povolíte, můžou uživatelé spouštět nepodepsané ovládací prvky bez zásahu uživatele. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, zobrazí se uživatelům dotaz, zda chcete, aby bylo možné spustit nepodepsaný ovládací prvek. Pokud nastavení této zásady zakážete, uživatelé nemůžou spouštět nepodepsané ovládací prvky. Pokud nastavení této zásady nenakonfigurujete, uživatelé nemůžou spouštět nepodepsané ovládací prvky.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067177)

  **Výchozí**: zakázat

- **Internetová zóna Internet Exploreru přetahování obsahu z různých domén v systému Windows**:  
  Toto nastavení zásad umožňuje spravovat, jestli uživatelé můžou stahovat nepodepsané ovládací prvky ActiveX ze zóny. Takový kód je potenciálně škodlivý, zejména když přichází z nedůvěryhodné zóny. Pokud nastavení této zásady povolíte, můžou uživatelé spouštět nepodepsané ovládací prvky bez zásahu uživatele. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, zobrazí se uživatelům dotaz, zda chcete, aby bylo možné spustit nepodepsaný ovládací prvek. Pokud nastavení této zásady zakážete, uživatelé nemůžou spouštět nepodepsané ovládací prvky. Pokud nastavení této zásady nenakonfigurujete, uživatelé nemůžou spouštět nepodepsané ovládací prvky.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067095)

  **Výchozí**: zakázáno

- **Procesy aplikace Internet Explorer omezují aktivní instalaci X**:  
  Nastavení této zásady umožňuje aplikacím, které hostují ovládací prvek webového prohlížeče, blokovat automatické zobrazování výzev k instalaci ovládacího prvku ActiveX. Pokud toto nastavení zásad povolíte, bude ovládací prvek webového prohlížeče blokovat automatické zobrazování výzev k instalaci ovládacího prvku ActiveX pro všechny procesy. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, ovládací prvek webového prohlížeče nebude blokovat automatické zobrazování výzev k instalaci ovládacího prvku ActiveX pro všechny procesy.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067250)

  **Výchozí**: povoleno

- **Skriptlety internetové zóny Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat, jestli může uživatel spustit skriptlety. Pokud nastavení této zásady povolíte, může uživatel spustit skriptlety. Pokud nastavení této zásady zakážete, nemůže uživatel spustit skriptlety. Pokud nastavení této zásady nenakonfigurujete, uživatel může povolit nebo zakázat skriptlety.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067176)

  **Výchozí**: zakázat

- **Zóna s omezeným přístupem, přetahování nebo kopírování a vkládání souborů v Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat, jestli uživatelé můžou přetahovat soubory nebo kopírovat a vkládat soubory ze zdroje v rámci zóny. Pokud nastavení této zásady povolíte, budou uživatelé moci automaticky přetahovat soubory nebo kopírovat a vkládat soubory z této zóny. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, zobrazí se uživatelům dotaz, zda chcete soubory přetáhnout nebo zkopírovat z této zóny. Pokud nastavení této zásady zakážete, uživatelé nebudou moci přetahovat soubory nebo kopírovat a vkládat soubory z této zóny. Pokud nastavení této zásady nenakonfigurujete, zobrazí se uživatelům dotaz, zda chcete soubory z této zóny přetáhnout nebo zkopírovat.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067096)

  **Výchozí**: zakázat

- **Software aplikace Internet Explorer, pokud je podpis neplatný**:  
  Toto nastavení zásad umožňuje spravovat, jestli může uživatel nainstalovat nebo spustit software, jako jsou ovládací prvky ActiveX a soubory ke stažení, i když signatura není platná. Neplatný podpis může indikovat, že někdo záměrně soubor úmyslně udělal. Pokud nastavení této zásady povolíte, budou uživatelé vyzváni k instalaci nebo spuštění souborů s neplatným podpisem. Pokud nastavení této zásady zakážete, uživatelé nemůžou spouštět nebo instalovat soubory s neplatným podpisem. Pokud tuto zásadu nenakonfigurujete, můžou uživatelé spouštět nebo instalovat soubory s neplatným podpisem.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067201)

  **Výchozí**: zakázáno

- **Kopírování a vkládání zóny s omezeným přístupem v aplikaci Internet Explorer pomocí skriptu**:  
  Toto nastavení zásad umožňuje spravovat, jestli můžou skripty provádět operace se schránkou (například vyjmutí, kopírování a vložení) v zadané oblasti. Pokud nastavení této zásady povolíte, skript může provést operaci se schránkou. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, budou se uživatelé dotazovat na to, jestli se mají dělat operace schránky. Pokud nastavení této zásady zakážete, skript nemůže provést operaci se schránkou. Pokud nastavení této zásady nenakonfigurujete, skript nemůže provést operaci se schránkou.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067165)

  **Výchozí**: zakázat

- **Zóna s omezeným přístupem v aplikaci Internet Explorer přetahování obsahu z různých domén v systému Windows**:  
  Toto nastavení zásad umožňuje nastavit možnosti pro přetahování obsahu z jedné domény do jiné domény, pokud je zdroj a cíl v různých oknech. Pokud nastavení této zásady povolíte a kliknete na tlačítko Povolit, mohou uživatelé přetahovat obsah z jedné domény do jiné domény, když se zdroj a cíl nacházejí v různých oknech. Uživatelé toto nastavení nemůžou změnit. Pokud nastavení této zásady povolíte a kliknete na zakázat, uživatelé nemůžou přetahovat obsah z jedné domény do jiné domény, pokud je zdroj i cíl v různých oknech. Uživatelé toto nastavení nemůžou změnit. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, uživatelé nebudou moci přetahovat obsah z jedné domény do jiné domény, pokud je zdroj a cíl v různých oknech, a to v aplikaci Internet Explorer 10. Uživatelé můžou toto nastavení změnit v dialogovém okně Možnosti Internetu. Pokud v aplikaci Internet Explorer 9 a starších verzích zakážete tuto zásadu nebo ji nenakonfigurujete, uživatelé mohou přetahovat obsah z jedné domény do jiné domény, pokud je zdroj a cíl v různých oknech. Uživatelé toto nastavení nemůžou změnit.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067166)

  **Výchozí**: zakázáno

- **Uživatelé Internet Exploreru přidávají lokality**:  
  Zabrání uživatelům přidávat nebo odebírat weby ze zón zabezpečení. Zóna zabezpečení je skupina webů se stejnou úrovní zabezpečení. Pokud tuto zásadu povolíte, nastavení správy lokality pro zóny zabezpečení bude zakázáno. (Pokud chcete zobrazit nastavení správy lokality pro zóny zabezpečení, klikněte v dialogovém okně Možnosti Internetu na kartu zabezpečení a pak klikněte na tlačítko weby.) Pokud tuto zásadu zakážete nebo nenakonfigurujete, můžou uživatelé přidat weby do zón důvěryhodných lokalit a serverů s omezeným přístupem nebo je z nich odebírat a změnit nastavení pro zónu místního intranetu. Tato zásada zabraňuje uživatelům měnit nastavení správy lokality pro zóny zabezpečení zřízené správcem. Poznámka: zásada "Zakázat stránku zabezpečení" (nacházející se v Ovládacích panelech \ Šablony pro správu \ součásti systému Windows\internet Explorer\Internet), která odebere kartu zabezpečení z rozhraní, má přednost před touto zásadou. Pokud je tato zásada povolená, ignoruje se. Podívejte se také na zásady zóny zabezpečení: použít jenom nastavení počítače.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067167)

  **Výchozí**: zakázáno

- **Windows Explorer skript internetové zóny, který spustil Windows**:  
  Toto nastavení zásad umožňuje spravovat omezení pro automaticky otevíraná okna spouštěná skriptem a okna, která obsahují nadpis a stavové řádky. Pokud nastavení této zásady povolíte, nebude se zabezpečení na této zóně vztahovat na Windows. Zóna zabezpečení se spouští bez přidané úrovně zabezpečení, kterou poskytuje tato funkce. Pokud nastavení této zásady zakážete, budou možné škodlivé akce obsažené v automaticky otevíraných oknech a oknech spouštěných skriptem, které obsahují název a stavové řádky, které nejdou spustit. Tato funkce zabezpečení aplikace Internet Explorer je v této zóně zapnutá nastavením řízení funkcí skriptovaná omezení zabezpečení systému Windows pro daný proces. Pokud nastavení této zásady nenakonfigurujete, možné škodlivé akce obsažené v automaticky otevíraných oknech a oknech spouštěných skriptem, které obsahují název a stavové řádky, nemůžou běžet. Tato funkce zabezpečení aplikace Internet Explorer je v této zóně zapnutá nastavením řízení funkcí skriptovaná omezení zabezpečení systému Windows pro daný proces.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067088)

  **Výchozí**: zakázáno

- **Zóny zabezpečení aplikace Internet Explorer používají pouze nastavení počítače**:  
  Aplikuje informace o zóně zabezpečení pro všechny uživatele stejného počítače. Zóna zabezpečení je skupina webů se stejnou úrovní zabezpečení. Pokud tuto zásadu povolíte, budou se změny, které uživatel provede v zóně zabezpečení, vztahovat na všechny uživatele tohoto počítače. Pokud tuto zásadu zakážete nebo nenakonfigurujete, můžou uživatelé stejného počítače vytvořit vlastní nastavení zóny zabezpečení. Pomocí této zásady zajistíte, aby se nastavení zón zabezpečení používalo jednotně pro stejný počítač a nelišilo se od uživatele k uživateli. Podívejte se také na téma zóny zabezpečení: Nepovolit uživatelům měnit zásady.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067086)

  **Výchozí**: povoleno

- **Aplikace Internet Explorer byla uzamčena v zóně místního počítače oprávnění Java**:  
  Toto nastavení zásad umožňuje spravovat oprávnění pro aplety v jazyce Java. Pokud nastavení této zásady povolíte, můžete v rozevíracím seznamu zvolit možnosti. Vlastní pro řízení nastavení oprávnění individuálně. Nízké zabezpečení umožňuje apletům provádět všechny operace. Střední zabezpečení umožňuje apletům běžet v izolovaném prostoru (sandboxu) (oblast v paměti mimo rámec toho, že program nemůže provádět volání) a navíc funkce, jako je například pomocné místo (bezpečná a zabezpečená oblast úložiště v klientském počítači) a uživatelem řízený vstup/výstup souborů. Vysoké zabezpečení umožňuje, aby se applety spouštěly v izolovaném prostoru. Zakáže Java, aby se zabránilo spuštění všech apletů. Pokud nastavení této zásady zakážete, aplety Java nepůjde spustit. Pokud nastavení této zásady nenakonfigurujete, aplety Java budou zakázané.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067253)

  **Výchozí**: zakázat Java

- **Zóna s omezeným přístupem aplikace Internet Explorer nespouští antimalware proti ovládacím prvkům**ActiveX:  
  Nastavení této zásady určuje, jestli aplikace Internet Explorer spouští antimalwarové programy proti ovládacím prvkům ActiveX, aby zkontrolovala, jestli se dají bezpečně načíst na stránkách. Pokud nastavení této zásady povolíte, aplikace Internet Explorer nebude u antimalwarového programu kontrolovat, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Pokud nastavení této zásady zakážete, bude aplikace Internet Explorer vždy kontrolovat váš Antimalwarový program, aby bylo možné zjistit, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Pokud nastavení této zásady nenakonfigurujete, bude aplikace Internet Explorer vždy kontrolovat váš Antimalwarový program, aby bylo možné zjistit, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Uživatelé můžou toto chování zapnout nebo vypnout pomocí nastavení zabezpečení Internet Exploreru.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067089)

  **Výchozí**: zakázáno

- **Zóna s omezeným přístupem v aplikaci Internet Explorer spouštějte .NET Framework závislé součásti podepsané pomocí technologie Authenticode**:  
  Toto nastavení zásad umožňuje spravovat, jestli .NET Framework součásti, které jsou podepsané pomocí technologie Authenticode, se dají spouštět z Internet Exploreru. Mezi tyto komponenty patří spravované ovládací prvky, na které se odkazuje ze značky objektu a spravované spustitelné soubory, na které odkazuje odkaz. Pokud toto nastavení zásad povolíte, aplikace Internet Explorer spustí podepsané spravované součásti. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, Internet Explorer vyzve uživatele, aby určil, zda mají být spuštěny podepsané spravované součásti. Pokud nastavení této zásady zakážete, aplikace Internet Explorer neprovede podepsané spravované součásti. Pokud nastavení této zásady nenakonfigurujete, aplikace Internet Explorer neprovede podepsané spravované součásti.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067169)

  **Výchozí**: zakázat

- **Přístup k zóně s omezeným přístupem v Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat, jestli Internet Explorer může získat přístup k datům z jiné zóny zabezpečení pomocí analyzátoru MSXML (Microsoft XML Parser) nebo rozhraní ADO (ActiveX Data Objects) (ADO). Pokud nastavení této zásady povolíte, uživatelé mohou načíst stránku v zóně, která používá MSXML nebo ADO pro přístup k datům z jiné lokality v zóně. Pokud v rozevíracím seznamu vyberete příkaz Dotázat se na uživatele, zobrazí se dotaz, jestli chcete, aby se stránka načetla do zóny, která používá MSXML nebo ADO pro přístup k datům z jiné lokality v zóně. Pokud nastavení této zásady zakážete, uživatelé nemůžou načíst stránku v zóně, která používá MSXML nebo ADO pro přístup k datům z jiné lokality v zóně. Pokud nastavení této zásady nenakonfigurujete, uživatelé nebudou moci načíst stránku v zóně, která používá MSXML nebo ADO pro přístup k datům z jiné lokality v zóně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067161)

  **Výchozí**: zakázat

- **Internetová zóna Internet Exploreru nespouští Antimalwarový program proti ovládacím prvkům ActiveX**:  
  Nastavení této zásady určuje, jestli aplikace Internet Explorer spouští antimalwarové programy proti ovládacím prvkům ActiveX, aby zkontrolovala, jestli se dají bezpečně načíst na stránkách. Pokud nastavení této zásady povolíte, aplikace Internet Explorer nebude u antimalwarového programu kontrolovat, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Pokud nastavení této zásady zakážete, bude aplikace Internet Explorer vždy kontrolovat váš Antimalwarový program, aby bylo možné zjistit, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Pokud nastavení této zásady nenakonfigurujete, bude aplikace Internet Explorer vždy kontrolovat váš Antimalwarový program, aby bylo možné zjistit, zda je bezpečné vytvořit instanci ovládacího prvku ActiveX. Uživatelé můžou toto chování zapnout nebo vypnout pomocí nastavení zabezpečení Internet Exploreru.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067162)

  **Výchozí**: zakázáno

- **Kopírování a vkládání internetových zón Internet Exploreru prostřednictvím skriptu**:  
  Toto nastavení zásad umožňuje spravovat, jestli můžou skripty provádět operace se schránkou (například vyjmutí, kopírování a vložení) v zadané oblasti. Pokud nastavení této zásady povolíte, skript může provést operaci se schránkou. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, budou se uživatelé dotazovat na to, jestli se mají dělat operace schránky. Pokud nastavení této zásady zakážete, skript nemůže provést operaci se schránkou. Pokud nastavení této zásady nenakonfigurujete, skript může provést operaci se schránkou.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067084)

  **Výchozí**: zakázat

- **Aplikace Internet Explorer používá službu Active X Installer**:  
  Nastavení této zásady umožňuje určit, jak jsou ovládací prvky ActiveX nainstalovány. Pokud nastavení této zásady povolíte, budou se ovládací prvky ActiveX instalovat jenom v případě, že je k dispozici instalační služba ActiveX a je nakonfigurovaná tak, aby umožňovala instalaci ovládacích prvků ActiveX. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, budou ovládací prvky ActiveX, včetně ovládacích prvků pro jednotlivé uživatele, nainstalovány prostřednictvím standardního procesu instalace.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067163)

  **Výchozí**: povoleno

- **Aplikace Internet Explorer zpracovává ochranu před zvýšením úrovně zóny**:  
  Aplikace Internet Explorer umisťuje omezení na každou webovou stránku, kterou otevře. Tato omezení závisí na umístění webové stránky (Internet, intranet, zóna místní počítač atd.). Například webové stránky v místním počítači mají nejnižší bezpečnostní omezení a jsou v zóně místního počítače, takže zóna zabezpečení místního počítače má primární cíl pro uživatele se zlými úmysly. Pokud nastavení této zásady povolíte, může být jakákoli zóna chráněná před zvýšením úrovně pásma pro všechny procesy. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, procesy jiné než Internet Explorer nebo, které jsou uvedeny v seznamu procesů, neobdrží takovou ochranu.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067160)

  **Výchozí**: povoleno

- **Stažení internetových zón Internet Exploreru nepodepsané ovládací prvky ActiveX**:  
  Toto nastavení zásad umožňuje spravovat, jestli uživatelé můžou stahovat nepodepsané ovládací prvky ActiveX ze zóny. Takový kód je potenciálně škodlivý, zejména když přichází z nedůvěryhodné zóny. Pokud nastavení této zásady povolíte, můžou uživatelé spouštět nepodepsané ovládací prvky bez zásahu uživatele. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, zobrazí se uživatelům dotaz, zda chcete, aby bylo možné spustit nepodepsaný ovládací prvek. Pokud nastavení této zásady zakážete, uživatelé nemůžou spouštět nepodepsané ovládací prvky. Pokud nastavení této zásady nenakonfigurujete, uživatelé nemůžou spouštět nepodepsané ovládací prvky.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067325)

  **Výchozí**: zakázat

- **Internet Explorer Internet Zone navigovat okna a rámce napříč různými doménami**:  
  Toto nastavení zásad umožňuje spravovat otevírání oken a rámců a přístup k aplikacím v různých doménách. Pokud nastavení této zásady povolíte, můžou uživatelé otevřít Windows a snímky z jiných domén a přistupovat k aplikacím z jiných domén. Pokud v rozevíracím seznamu vyberete možnost zobrazit výzvu, uživatelům se zobrazí dotaz, zda mají okna a rámce umožňovat přístup k aplikacím z jiných domén. Pokud nastavení této zásady zakážete, uživatelé nemůžou otevřít Windows a snímky pro přístup k aplikacím z různých domén. Pokud nastavení této zásady nenakonfigurujete, můžou uživatelé otevřít Windows a snímky z jiných domén a přistupovat k aplikacím z jiných domén.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067083)

  **Výchozí**: zakázat

- **Aktualizace internetové zóny Internet Exploreru na stavovém řádku prostřednictvím skriptu**:  
  Toto nastavení zásad umožňuje spravovat, jestli skript může aktualizovat stavový řádek v rámci zóny. Pokud nastavení této zásady povolíte, můžou skripty aktualizovat stavový řádek. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, skript nebude moct aktualizovat stavový řádek.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067087)

  **Výchozí**: zakázáno

- **Zóna s omezeným přístupem v Internet Exploreru zahrnuje místní cestu při nahrávání souborů na server**:  
  Nastavení této zásady určuje, jestli se mají odesílat informace o místní cestě, když uživatel nahrává soubor prostřednictvím formuláře HTML. Pokud se odesílají informace o místní cestě, můžou být některé informace neúmyslně odhaleny serveru. Například soubory odeslané z plochy uživatele mohou obsahovat uživatelské jméno jako součást cesty. Pokud toto nastavení zásad povolíte, odesílají se informace o cestě, když uživatel nahraje soubor prostřednictvím formuláře HTML. Pokud toto nastavení zásad zakážete, informace o cestě se odeberou, když uživatel nahraje soubor prostřednictvím formuláře HTML. Pokud nastavení této zásady nenakonfigurujete, může uživatel zvolit, zda budou informace o cestě odeslány při nahrávání souboru prostřednictvím formuláře HTML. Ve výchozím nastavení jsou odesílány informace o cestě.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067085)

  **Výchozí**: zakázáno

- **Procesy aplikace Internet Explorer omezují stahování souborů**:  
  Nastavení této zásady umožňuje aplikacím, které hostují ovládací prvek webového prohlížeče, blokovat automatické zobrazování výzev ke stažení souborů, které neinicioval uživatel. Pokud nastavení této zásady povolíte, bude ovládací prvek webového prohlížeče blokovat automatické zobrazování výzev ke stažení souborů, které neinicioval uživatel pro všechny procesy. Pokud toto nastavení zásad zakážete, nebude ovládací prvek webového prohlížeče blokovat automatické zobrazování výzev ke stažení souborů, které neinicioval uživatel pro všechny procesy.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067164)

  **Výchozí**: povoleno

- **Omezená zóna aplikace Internet Explorer povoluje použití aktivních ovládacích prvků X pouze v schválených doménách**:  
  Nastavení této zásady určuje, jestli se uživateli zobrazí výzva, aby se povolilo spouštění ovládacích prvků ActiveX na jiných webech, než na webu, který nainstaloval ovládací prvek ActiveX. Pokud nastavení této zásady povolíte, zobrazí se uživateli výzva před spuštěním ovládacích prvků ActiveX z webů v této zóně. Uživatel může zvolit, že se má ovládací prvek spouštět z aktuálního webu nebo ze všech lokalit. Pokud nastavení této zásady zakážete, uživatel nebude zobrazovat výzvu ActiveX pro jednotlivé lokality a ovládací prvky ActiveX lze spouštět ze všech lokalit v této zóně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067233)

  **Výchozí**: povoleno

- **Inicializace zóny s omezeným přístupem k aplikaci Internet Explorer a kontrola skriptu aktivní X není označena jako bezpečná**:  
  Toto nastavení zásad umožňuje spravovat ovládací prvky ActiveX, které nejsou označeny jako bezpečné. Pokud nastavení této zásady povolíte, budou ovládací prvky ActiveX spouštěny, načteny s parametry a pomocí skriptů bez nastavení bezpečnosti objektů pro nedůvěryhodná data nebo skripty. Toto nastavení se nedoporučuje, s výjimkou zabezpečených a spravovaných zón. Toto nastavení způsobí, že budou inicializovány nebezpečné i bezpečné ovládací prvky a budou skriptované, ignorování ovládacích prvků ActiveX skriptu označených jako bezpečné pro možnost skriptování. Pokud nastavení této zásady povolíte a v rozevíracím seznamu vyberete možnost zobrazit výzvu, uživatelé se dotazují, jestli chcete ovládacímu prvku povolit načtení pomocí parametrů nebo skriptu. Pokud nastavení této zásady zakážete, nebudou se ovládací prvky ActiveX, které se dají bezpečně nastavit, načítat pomocí parametrů nebo skriptu. Pokud nastavení této zásady nenakonfigurujete, nebudou se ovládací prvky ActiveX, které se dají bezpečně nastavit, načítat pomocí parametrů nebo skriptu.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067097)

  **Výchozí**: zakázat

- **Uživatelé aplikace Internet Explorer měnící zásady**:  
  Zabrání uživatelům měnit nastavení zón zabezpečení. Zóna zabezpečení je skupina webů se stejnou úrovní zabezpečení. Pokud tuto zásadu povolíte, na kartě zabezpečení v dialogovém okně Možnosti Internetu jsou zakázaná tlačítka vlastní úroveň a posuvník úrovně zabezpečení. Pokud tuto zásadu zakážete nebo nenakonfigurujete, můžou uživatelé změnit nastavení zón zabezpečení. Tato zásada zabraňuje uživatelům měnit nastavení zón zabezpečení vytvořená správcem. Poznámka: zásada "Zakázat stránku zabezpečení" (nacházející se v části \ Šablony pro správu \ součásti \ Windows\internet ovládací panely), která odebere kartu zabezpečení z Internet Exploreru v Ovládacích panelech, má přednost před touto zásadou. Pokud je tato zásada povolená, ignoruje se. Podívejte se také na zásady zóny zabezpečení: použít jenom nastavení počítače.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067155)

  **Výchozí**: zakázáno

- **Chráněný režim omezené zóny Internet Exploreru**:  
  Toto nastavení zásad umožňuje zapnout chráněný režim. Chráněný režim pomáhá chránit Internet Explorer před zneužitím ohrožení zabezpečení tím, že snižuje umístění, do kterých aplikace Internet Explorer může zapisovat do registru a systému souborů. Pokud nastavení této zásady povolíte, je chráněný režim zapnutý. Uživatel nemůže vypnout chráněný režim. Pokud nastavení této zásady zakážete, je chráněný režim vypnutý. Uživatel nemůže zapnout chráněný režim. Pokud nastavení této zásady nenakonfigurujete, může uživatel zapnout nebo vypnout chráněný režim.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067080)

  **Výchozí**: Povolit

- **Trvalost uživatelských dat pro internetovou zónu Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat uchovávání informací v historii prohlížeče, v oblíbených položkách v úložišti XML nebo přímo na webové stránce uložené na disku. Když se uživatel vrátí na trvalou stránku, může se stát, že se stav stránky obnoví, pokud je toto nastavení zásad vhodně nakonfigurované. Pokud nastavení této zásady povolíte, mohou uživatelé uchovávat informace v historii prohlížeče, v oblíbených položkách v úložišti XML nebo přímo v rámci webové stránky uložené na disk. Pokud nastavení této zásady zakážete, uživatelé nebudou moci uchovávat informace v historii prohlížeče, v oblíbených položkách v úložišti XML nebo přímo na webové stránce uložené na disku. Pokud nastavení této zásady nenakonfigurujete, mohou uživatelé uchovávat informace v historii prohlížeče, v oblíbených položkách v úložišti XML nebo přímo v rámci webové stránky uložené na disk.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067156)

  **Výchozí**: zakázáno

- Internet **Explorer Internet Zone skriptování ovládacích prvků webového prohlížeče**:  
  Nastavení této zásady určuje, zda může stránka řídit vložené ovládací prvky WebBrowser prostřednictvím skriptu. Pokud nastavení této zásady povolíte, je povolený přístup ke skriptu ovládacího prvku WebBrowser. Pokud nastavení této zásady zakážete, nebude přístup k skriptu k ovládacímu prvku WebBrowser povolen. Pokud nastavení této zásady nenakonfigurujete, uživatel může povolit nebo zakázat přístup k skriptu ovládacímu prvku WebBrowser. Ve výchozím nastavení je přístup ke skriptu k ovládacímu prvku WebBrowser povolen pouze v zónách místní počítač a intranet.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067157)

  **Výchozí**: zakázáno

- **Trvalost uživatelských dat zóny s omezeným přístupem aplikace Internet Explorer**:  
  Toto nastavení zásad umožňuje spravovat uchovávání informací v historii prohlížeče, v oblíbených položkách v úložišti XML nebo přímo na webové stránce uložené na disku. Když se uživatel vrátí na trvalou stránku, může se stát, že se stav stránky obnoví, pokud je toto nastavení zásad vhodně nakonfigurované. Pokud nastavení této zásady povolíte, mohou uživatelé uchovávat informace v historii prohlížeče, v oblíbených položkách v úložišti XML nebo přímo v rámci webové stránky uložené na disk. Pokud nastavení této zásady zakážete, uživatelé nebudou moci uchovávat informace v historii prohlížeče, v oblíbených položkách v úložišti XML nebo přímo na webové stránce uložené na disku. Pokud nastavení této zásady nenakonfigurujete, uživatelé nebudou moci zachovat informace v historii prohlížeče, v oblíbených položkách v úložišti XML nebo přímo v rámci webové stránky uložené na disk.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067081)

  **Výchozí**: zakázáno

- **Aplikace Internet Explorer byla uzamčena v intranetové zóně oprávnění Java**:  
  Toto nastavení zásad umožňuje spravovat oprávnění pro aplety v jazyce Java. Pokud nastavení této zásady povolíte, můžete v rozevíracím seznamu zvolit možnosti. Vlastní pro řízení nastavení oprávnění individuálně. Nízké zabezpečení umožňuje apletům provádět všechny operace. Střední zabezpečení umožňuje apletům běžet v izolovaném prostoru (sandboxu) (oblast v paměti mimo rámec toho, že program nemůže provádět volání) a navíc funkce, jako je například pomocné místo (bezpečná a zabezpečená oblast úložiště v klientském počítači) a uživatelem řízený vstup/výstup souborů. Vysoké zabezpečení umožňuje, aby se applety spouštěly v izolovaném prostoru. Zakáže Java, aby se zabránilo spuštění všech apletů. Pokud nastavení této zásady zakážete, aplety Java nepůjde spustit. Pokud nastavení této zásady nenakonfigurujete, aplety Java budou zakázané.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067082)

  **Výchozí**: zakázat Java

- **Rozšířený chráněný režim aplikace Internet Explorer**:  
  Rozšířený chráněný režim poskytuje dodatečnou ochranu před škodlivými weby pomocí 64 procesů na 64 verzích systému Windows. V počítačích s minimálně Windows 8 se v rozšířeném chráněném režimu taky omezují umístění, ze kterých může Internet Explorer číst v registru a v systému souborů. Pokud nastavení této zásady povolíte, je zapnutý režim Enhanced Protected. Všechny zóny, které mají povolený chráněný režim, budou používat Rozšířený chráněný režim. Uživatelé nemůžou zakázat Rozšířený chráněný režim. Pokud nastavení této zásady zakážete, je vypnutý Rozšířený chráněný režim. Všechny zóny s povoleným chráněným režimem budou používat verzi chráněného režimu představenou v aplikaci Internet Explorer 7 pro systém Windows Vista. Pokud tuto zásadu nenakonfigurujete, uživatelé můžou zapnout nebo vypnout Rozšířený chráněný režim na kartě Upřesnit dialogového okna Možnosti Internetu.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067158)

  **Výchozí**: povoleno

- **Upozornění na vynechání inteligentní obrazovky Internet Exploreru**:  
  Nastavení této zásady určuje, jestli uživatel může obejít upozornění z filtru SmartScreen. Filtr SmartScreen uživatele upozorní na spustitelné soubory, které uživatelé Internet Exploreru nestahují běžným z Internetu. Pokud toto nastavení zásad povolíte, upozornění filtru SmartScreen blokují uživatele. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, může uživatel obejít upozornění filtru SmartScreen.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067159)

  **Výchozí**: zakázáno

- **Meta aktualizace zóny omezeného Internet Exploreru**:  
  Toto nastavení zásad umožňuje spravovat, jestli je možné prohlížeč uživatele přesměrovat na jinou webovou stránku, pokud autor webové stránky používá nastavení Meta Refresh (tag) k přesměrování prohlížečů na jinou webovou stránku. Pokud nastavení této zásady povolíte, bude prohlížeč uživatele, který načte stránku obsahující aktivní nastavení Meta Refresh, přesměrovat na jinou webovou stránku. Pokud nastavení této zásady zakážete, nebude možné přesměrovat prohlížeč uživatele, který načte stránku obsahující aktivní nastavení Meta Refresh, na jinou webovou stránku. Pokud nastavení této zásady nenakonfigurujete, nebude možné přesměrovat prohlížeč uživatele, který načte stránku obsahující aktivní nastavení Meta Refresh, na jinou webovou stránku.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067154)

  **Výchozí**: zakázáno

## <a name="local-policies-security-options"></a>Možnosti zabezpečení místních zásad

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – LocalPoliciesSecurityOptions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions) .

- **Omezit anonymní přístup k pojmenovaným kanálům a sdíleným složkám**:  
  Když je toto nastavení zabezpečení povolené, omezí anonymní přístup ke sdíleným složkám a kanálům na nastavení pro: (1) pojmenované kanály, ke kterým se dá přistupovat anonymně (2) ke sdíleným složkám, ke kterým se dá přistupovat anonymně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067212)

  **Výchozí**: Ano

- **Minimální zabezpečení relace pro servery založené na NTLM SSP**:  
  Toto nastavení zabezpečení umožňuje serveru vyžadovat vyjednávání 128 bitů šifrování a zabezpečení relace NTLMv2. Tyto hodnoty jsou závislé na hodnotě nastavení zabezpečení na úrovni ověřování v programu LAN Manager. Možnosti: vyžadovat zabezpečení relace NTLMv2: připojení selže, pokud není vyjednána integrita zprávy. Vyžadovat 128 bitů šifrování. Pokud není vyjednáno silné šifrování (128 bitů), připojení se nezdaří.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067246)

  **Výchozí**: vyžadování protokolu NTLM V2 a 128 bitového šifrování

- Počet **minut nečinnosti uzamčené obrazovky, po které se spořič obrazovky aktivuje**:  
  Systém Windows zaznamená nečinnost relace přihlášení, a pokud neaktivní doba překračuje limit nečinnosti, pak se spustí šetřič obrazovky, který relaci uzamkne.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067210)

  **Výchozí**: 15

- **Vyžadovat od klienta vždycky digitálně podepsat komunikaci**:  
  Toto nastavení zabezpečení určuje, zda musí být veškerý provoz zabezpečeného kanálu iniciované členem domény podepsán nebo zašifrován. Když se počítač připojí k doméně, vytvoří se účet počítače. Po tom, co se systém spustí, se pomocí hesla účtu počítače vytvoří zabezpečený kanál s řadičem domény pro svoji doménu. Tento zabezpečený kanál se používá k provádění operací, jako je například ověřování pomocí protokolu NTLM, ověřování názvů zabezpečení LSA a další informace. Toto nastavení určuje, zda veškerý provoz zabezpečeného kanálu iniciované členem domény splňuje minimální požadavky na zabezpečení. Konkrétně určuje, zda je nutné všechny přenosy zabezpečeného kanálu spuštěné členem domény podepsat nebo zašifrovat. Pokud je tato zásada povolená, zabezpečený kanál se nevytvoří, pokud se nepoužije podepisování nebo šifrování veškerého provozu zabezpečeného kanálu. Pokud je tato zásada zakázaná, pak se šifrování a podepsání veškerého provozu zabezpečeného kanálu vyjednávají s řadičem domény. v takovém případě je úroveň podepisování a šifrování závislá na verzi řadiče domény a nastavení těchto dvou zásad: člen domény: digitálně šifrovat data zabezpečeného kanálu (Pokud je to možné): digitálně podepsat data zabezpečeného kanálu (Pokud je to možné).  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067187)

  **Výchozí**: Ano

- **Úroveň ověřování**:  
  Toto nastavení zabezpečení určuje, který ověřovací protokol pro ověření výzvou a odpovědí se používá pro přihlášení k síti. Tato volba ovlivňuje úroveň protokolu ověřování používaného klienty, úroveň vyjednané zabezpečení relace a úroveň ověřování, kterou tyto servery akceptují:

  - *Posílání odpovědí LM a NTLM* – klienti používají ověřování LM a NTLM a nikdy nepoužívají zabezpečení relace NTLMv2; řadiče domény přijímají ověřování LM, NTLM a NTLM.

  - *Odeslat LM a NTLM-NTLMv2, pokud jsou vyjednáno* – klienti používají ověřování LM a NTLM a používají zabezpečení relace NTLMv2, pokud je server podporuje. Řadiče domény přijímají ověřování LM, NTLM a NTLM.

  - *Poslat jenom odpovědi NTLM* – klienti používají jenom ověřování NTLM a používají zabezpečení relace NTLMv2, pokud je server podporuje. řadiče domény přijímají ověřování LM, NTLM a NTLM.

  - *Poslat jenom odpovědi NTLMv2* – klienti používají jenom ověřování NTLMv2 a v případě, že ho Server podporuje, používá zabezpečení relace NTLMv2. řadiče domény přijímají ověřování LM, NTLM a NTLM.

  - *Poslat jenom odpověď NTLMv2 Odmítat LM* – klienti používají jenom ověřování NTLMv2 a v případě, že ho Server podporuje, použijte zabezpečení relace NTLMv2. Řadiče domény odmítnou LM (přijímá pouze ověřování NTLM a NTLM).

  - *Poslat jenom odpověď NTLMv2 Odmítat LM a NTLM* – klienti používají jenom ověřování NTLMv2 a v případě, že ho Server podporuje, použijte zabezpečení relace NTLMv2. Řadiče domény odmítnou LM a NTLM (přijímají pouze ověřování NTLMv2).

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067189)

  **Výchozí**: odeslat pouze odpověď NTLMv2. Odmítat LM a NTLM

- **Zabránit klientům v posílání nezašifrovaných hesel na servery SMB třetích stran**:  
  Pokud je toto nastavení zabezpečení povolené, přesměrovači protokolu SMB (Server Message Block) může posílat hesla ve formátu prostého textu na servery SMB jiných společností než Microsoft, které při ověřování nepodporují šifrování hesla. Posílání nezašifrovaných hesel je bezpečnostní riziko.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067235)

  **Výchozí**: Ano

- **Vyžadovat komunikaci s digitálním podpisem serveru vždycky**:  
  Toto nastavení zabezpečení určuje, jestli se klient SMB pokusí vyjednat podepisování paketů SMB. Protokol SMB (Server Message Block) poskytuje základ pro sdílení souborů a tiskáren společnosti Microsoft a mnoho dalších síťových operací, například vzdálenou správu systému Windows. Aby nedocházelo k útokům prostředníkem, které mění pakety SMB při přenosu, podporuje protokol SMB digitální podepisování paketů SMB. Nastavení této zásady určuje, jestli se součást klienta protokolu SMB pokusí vyjednat podepisování paketů SMB při připojení k serveru SMB. Pokud je toto nastavení povolené, bude klient sítě Microsoftu požádat server, aby po nastavení relace provede podepisování paketů SMB. Pokud je na serveru podepisování paketů povolené, podepisování paketů se vyjedná. Pokud je tato zásada zakázaná, klient SMB nebude nikdy vyjednávat podepisování paketů SMB.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067319)

  **Výchozí**: Ano

- **Chování výzvy ke zvýšení úrovně oprávnění správce**:  
  Toto nastavení zásady řídí chování výzvy ke zvýšení oprávnění pro správce. Dostupné možnosti:

  - *Zvýšení oprávnění bez výzvy* – umožňuje privilegovaným účtům provést operaci, která vyžaduje zvýšení oprávnění bez vyžadování souhlasu nebo přihlašovacích údajů. Poznámka: tuto možnost použijte jenom v nejvíc omezených prostředích.

  - *Vyzvat k zadání přihlašovacích údajů na zabezpečené ploše* – Pokud operace vyžaduje zvýšení oprávnění, zobrazí se uživateli výzva k zadání privilegovaného uživatelského jména a hesla na zabezpečené ploše. Pokud uživatel zadá platné přihlašovací údaje, operace pokračuje s největším dostupným oprávněním uživatele.

  - *Vyzvat k vyjádření souhlasu na zabezpečené ploše* – Pokud operace vyžaduje zvýšení oprávnění, zobrazí se uživateli výzva na zabezpečené ploše, aby bylo možné vybrat možnost povolit nebo odepřít. Pokud uživatel vybere povolit, operace pokračuje s největším dostupným oprávněním uživatele.

  - *Vyzvat k zadání přihlašovacích údajů* – Pokud operace vyžaduje zvýšení oprávnění, zobrazí se uživateli výzva k zadání uživatelského jména a hesla pro správu. Pokud uživatel zadá platné přihlašovací údaje, operace pokračuje s příslušným oprávněním.

  - *Vyzvat k vyjádření souhlasu* – Pokud operace vyžaduje zvýšení oprávnění, zobrazí se uživateli výzva k výběru možnost povolit nebo odepřít. Pokud uživatel vybere povolit, operace pokračuje s největším dostupným oprávněním uživatele.

  - *Vyzvat k vyjádření souhlasu s binárními soubory, které nejsou v systému Windows* – Pokud operace pro aplikaci od jiného výrobce než od Microsoftu vyžaduje zvýšení oprávnění, zobrazí se uživateli výzva k výběru možnost povolit nebo zamítnout. Pokud uživatel vybere povolit, operace pokračuje s největším dostupným oprávněním uživatele.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067215)

  **Výchozí**: vyzvat k vyjádření souhlasu na zabezpečené ploše

- **Minimální zabezpečení relace pro klienty založené na NTLM SSP**:  
  Toto nastavení zabezpečení umožňuje klientovi vyžadovat vyjednávání 128 bitů šifrování a zabezpečení relace NTLMv2. Tyto hodnoty jsou závislé na hodnotě nastavení zabezpečení na úrovni ověřování v programu LAN Manager. Dostupné možnosti:

  - *Vyžadovat zabezpečení relace NTLMv2* – Pokud není protokol NTLMv2 vyjednávat, připojení se nezdaří.

  - *Vyžadovat 128 bitů* – připojení selže, pokud se vyjednává silné šifrování (128 bitů).

  - *Vyžadovat šifrování NTLMv2 a 128 bitů*.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067324)

  **Výchozí**: vyžadovat šifrování NTLM v2 128

- **Chování při odebrání čipové karty**:  
  Toto nastavení zabezpečení určuje, co se stane, když se čipová karta přihlášeného uživatele odebere z čtecího zařízení s čipovou kartou. Dostupné možnosti:

  - *Žádná akce*.

  - *Zamknout pracovní stanici* – pracovní stanice je při odebrání čipové karty uzamčená a umožňuje uživatelům opustit oblast, přebírat jejich čipové karty a zachovat chráněnou relaci.

  - *Vynutit odhlášení* – při odebrání čipové karty se uživatel automaticky odhlásí.

  - *Odpojit relaci vzdálené plochy* – odebrání čipové karty odpojí relaci bez odhlášení uživatele. To umožňuje uživateli vložit čipovou kartu a později pokračovat v relaci nebo na jiném počítači vybaveném čtečkou čipových karet, aniž by se museli znovu přihlašovat. Pokud je relace místní, funguje tato zásada stejně jako možnost Zamknout pracovní stanici.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067331)

  **Výchozí**: zamknout pracovní stanici

- **Blokuje anonymní výčet účtů SAM a sdílených složek**:  
  Toto nastavení zabezpečení určuje, zda má být povoleno anonymní výčet účtů SAM a sdílených složek. Systém Windows umožňuje anonymním uživatelům provádět určité aktivity, jako je například vytváření výčtu názvů doménových účtů a síťových sdílených složek. To je užitečné, například když chce správce udělit přístup uživatelům v důvěryhodné doméně, které neudržují vzájemnou důvěryhodnost. Pokud nechcete povolit anonymní výčet účtů SAM a sdílených složek, nastavte tuto zásadu na *Ano*.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067191)

  **Výchozí**: Ano

- **Blokovat vzdálené přihlášení s prázdným heslem**:  
  Toto nastavení zabezpečení určuje, zda lze místní účty, které nejsou chráněny heslem, použít k přihlášení z jiných umístění, než je konzola fyzického počítače. Pokud je povoleno, přihlaste se k místnímu účtu, který není chráněn heslem, pomocí klávesnice počítače.

  *Upozornění*: počítače, které nejsou v fyzicky zabezpečených umístěních, by měly vždy vyhovět silným zásadám hesel pro všechny místní uživatelské účty. V opačném případě může kdokoli s fyzickým přístupem k počítači přihlásit pomocí uživatelského účtu, který nemá heslo. To je zvlášť důležité u přenosných počítačů.

  Pokud použijete tuto zásadu zabezpečení pro skupinu Everyone, nikdo se nemůže přihlásit přes službu Vzdálená plocha. Toto nastavení nemá vliv na přihlášení, která používají účty domény. Pro aplikace, které používají vzdálené interaktivní přihlášení, je možné toto nastavení obejít.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067219)

  **Výchozí**: Ano

- **Chování výzvy ke zvýšení úrovně Standard uživatele**:  
  Toto nastavení zásady řídí chování výzvy ke zvýšení oprávnění pro standardní uživatele.

  - *Automaticky odepřít žádosti o zvýšení oprávnění* – Pokud operace vyžaduje zvýšení oprávnění, zobrazí se chybová zpráva konfigurovatelný přístup byl odepřen. Podnik, na kterém běží stolní počítače jako standardní uživatel, může zvolit toto nastavení, aby se snížila volání helpdesku.

  - *Vyzvat k zadání přihlašovacích údajů na zabezpečené ploše* – Pokud operace vyžaduje zvýšení oprávnění, zobrazí se uživateli výzva k zadání jiného uživatelského jména a hesla na zabezpečené ploše. Pokud uživatel zadá platné přihlašovací údaje, operace pokračuje s příslušným oprávněním.

  - *Vyzvat k zadání přihlašovacích údajů* – Pokud operace vyžaduje zvýšení oprávnění, zobrazí se uživateli výzva k zadání uživatelského jména a hesla pro správu. Pokud uživatel zadá platné přihlašovací údaje, operace pokračuje s příslušným oprávněním.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067183)

  **Výchozí**: automaticky zamítnout žádosti o zvýšení oprávnění

- **Vyžadovat režim schválení správce pro správce**:  
  Toto nastavení zásady řídí chování všech nastavení zásad řízení uživatelských účtů (UAC) v počítači. Pokud toto nastavení zásad změníte, musíte restartovat počítač. Dostupné možnosti:

  - *Nenakonfigurováno* – režim schválení správce a všechna související nastavení zásad nástroje řízení uživatelských účtů jsou zakázaná. Poznámka: Pokud je toto nastavení zásad zakázané, Security Center vás upozorní, že celkové zabezpečení operačního systému bylo omezené.

  - *Ano* – režim schválení správcem je povolen. Tato zásada musí být povolená a odpovídající nastavení zásad nástroje řízení uživatelských účtů musí být nastavené tak, aby byl povolen integrovaný účet správce a všichni ostatní uživatelé, kteří jsou členy skupiny správců, aby mohli běžet v režimu schválení správce.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067184)

  **Výchozí**: Ano

- **Zabránit anonymnímu výčtu účtů SAM**:  
  Toto nastavení zabezpečení určuje, jaká další oprávnění budou udělena anonymním připojením k počítači. Systém Windows umožňuje anonymním uživatelům provádět určité aktivity, jako je například vytváření výčtu názvů doménových účtů a síťových sdílených složek. To je užitečné, například když chce správce udělit přístup uživatelům v důvěryhodné doméně, které neudržují vzájemnou důvěryhodnost. Tato možnost zabezpečení umožňuje umístit do anonymních připojení další omezení následujícím způsobem:

  - *Ano* – Nepovolit výčet účtů SAM. Tato možnost nahrazuje všechny ověřené uživatele v oprávnění zabezpečení pro prostředky.

  - *Nenakonfigurováno* – žádná další omezení. Spoléhá se na výchozí oprávnění.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067318)

  **Výchozí**: Ano

- **Povolte vzdálená volání do správce účtů zabezpečení**:  
  Toto nastavení zásad umožňuje omezit vzdálená připojení RPC k SAM. Pokud není vybraná, použije se výchozí popisovač zabezpečení.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067209)

  **Výchozí**: *O:Bag: Bad: (A;; RC;;; BA)*

- **Použít režim schválení správce**:  
  Toto nastavení zásady řídí chování režimu schválení správcem pro předdefinovaný účet správce. Dostupné možnosti:

  - *Ano* – integrovaný účet správce používá režim schválení správcem. Ve výchozím nastavení vyzve uživatel ke schválení operace všechny operace, které vyžadují zvýšení oprávnění.

  - *Nenakonfigurováno* – integrovaný účet správce spouští všechny aplikace s úplnými oprávněními správce.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067186)

  **Výchozí**: Ano
  
- **Povolte pouze aplikace přístupu uživatelského rozhraní pro zabezpečená umístění**:  
  Nastavení této zásady určuje, jestli programy pro usnadnění přístupu k uživatelskému rozhraní (UIAccess nebo UIA) můžou automaticky zakázat zabezpečenou plochu pro výzvy ke zvýšení oprávnění používané standardním uživatelem.

  - *Ano* – UIA programy, včetně vzdálené pomoci Windows, automaticky zakažte zabezpečenou plochu pro výzvy ke zvýšení oprávnění. Pokud nezakážete řízení uživatelských účtů: při zobrazení výzvy ke zvýšení oprávnění přepnout na zabezpečenou plochu, zobrazí se výzva na ploše interaktivního uživatele místo na zabezpečené ploše.

  - *Nenakonfigurováno*: zabezpečená plocha může být zakázaná jenom uživatelem interaktivní plochy nebo zakázáním možnosti řízení uživatelských účtů: při zobrazení výzvy ke zvýšení oprávnění přepnout na zabezpečenou plochu.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067185)

  **Výchozí**: Ano

- **Zjišťovat instalace aplikací a vyzvat ke zvýšení oprávnění**:  
  Toto nastavení zásady řídí chování detekce instalace aplikace pro daný počítač. Dostupné možnosti:

  - *Povoleno* – při zjištění instalačního balíčku aplikace, který vyžaduje zvýšení oprávnění, se uživateli zobrazí výzva k zadání uživatelského jména a hesla pro správu. Pokud uživatel zadá platné přihlašovací údaje, operace pokračuje s příslušným oprávněním.

  - *Zakázané* – instalační balíčky aplikací se nerozpoznají a zobrazí se výzva ke zvýšení oprávnění. U podniků, ve kterých běží standardní stolní počítače a využívají technologie delegované instalace, například Zásady skupiny pro instalaci softwaru nebo Systems Management Server (SMS), by měli toto nastavení zásad zakázat. V takovém případě je zjišťování instalační služby zbytečné.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067208)

  **Výchozí**: Ano

- **Zabránit ukládání hodnoty hash systému LAN Manager při příští změně hesla**:  
  Toto nastavení zabezpečení určuje, jestli se při další změně hesla uloží hodnota hash LAN Manageru (LM) pro nové heslo. Hodnota hash LM je poměrně slabá a náchylná k útokům v porovnání s kryptograficky silnější hodnotou hash systému Windows NT. Vzhledem k tomu, že hodnota hash LM je uložená v místním počítači v databázi zabezpečení, můžou být hesla ohrožená, pokud je databáze zabezpečení napadená.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067213)

  **Výchozí**: Ano

- **Virtualizovat selhání zápisu souborů a registrů do umístění uživatelů**:  
  Nastavení této zásady určuje, zda jsou chyby zápisu aplikace přesměrovány do definovaného registru a umístění systému souborů. Nastavení této zásady snižuje riziko aplikací spouštěných jako správce a zápis dat aplikace za běhu do *% ProgramFiles%*, *% windir%*, *%windir%\System32*nebo *HKLM\Software*.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067321)

  **Výchozí**: Ano

## <a name="microsoft-defender"></a>Microsoft Defender

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – Defender](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender) .

::: zone-end
::: zone pivot="mdm-may-2019"

- **Zablokuje Adobe Reader při vytváření podřízených procesů**:  
Toto pravidlo zabraňuje útokům blokováním aplikace Adobe Reader v vytváření dalších procesů. Prostřednictvím sociálního inženýrství nebo zneužití může malware stahovat a spouštět další datové části a přerušit z aplikace Adobe Reader. Blokováním podřízených procesů, které jsou vygenerovány aplikací Adobe Reader, se pokus o použití malwaru jako vektoru zabrání v rozprostření.
[Další informace](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  **Výchozí**: Povolit

- **Aplikace Office Communications se spouští v podřízeném procesu**:  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874499)

  **Výchozí**: Povolit

- **Zadejte, jak často (0-24 hodin) se mají kontrolovat aktualizace služby Security Intelligence.**  
  CSP: [Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)
  
  Určete, jak často se mají kontrolovat nové podpisy. Hodnota 1 je jedna hodina, 2 je dvě hodiny atd.

  **Výchozí**: 4

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

- **Den kontroly plánu Defenderu**:  
  Den kontroly plánu Defenderu

  **Výchozí**: každý den

- **Zapnout ochranu s doručováním v cloudu**:  
  CSP: [Defender/AllowCloudProtection](https://go.microsoft.com/fwlink/?linkid=2113937)
  
  Když se nastaví na Ano, Defender pošle Microsoftu informace o všech nalezených problémech. Pokud je nastavené na Nenakonfigurováno, klient se vrátí k výchozímu, který funkci povolí, ale umožní uživateli ho zakázat.

  **Výchozí**: Ano  

- **Zapnout ochranu v reálném čase**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050)

  Pokud je toto nastavení nastaveno na Ano, vynutilo se monitorování v reálném čase a uživatel ho nebude moct zakázat. Pokud je nastavené na Nenakonfigurováno, nastavení se vrátí do výchozího nastavení klienta, které je zapnuté, ale uživatel ho může změnit. Pokud chcete zakázat monitorování v reálném čase, použijte vlastní identifikátor URI.

  **Výchozí**: Ano  

- **Kontrolovat archivní soubory**:  
  CSP: [Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)
  
  Pokud je nastaveno na Ano, vynutily se soubory archivu, jako je například skenování souborů ZIP nebo CAB. Pokud je nastavené na Nenakonfigurováno, nastavení se vrátí zpátky do výchozího nastavení klienta, které bude kontrolovat archivované soubory, ale uživatel to může zakázat.

  **Výchozí**: Ano

- **Zapnout monitorování chování**:  
  CSP: [Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  Pokud je toto nastavení nastaveno na Ano, vynutilo se monitorování chování a uživatel ho nemůže zakázat. Pokud je nastavené na Nenakonfigurováno, nastavení se vrátí do výchozího nastavení klienta, které je zapnuté, ale uživatel ho může změnit. Pokud chcete zakázat monitorování v reálném čase, použijte vlastní identifikátor URI.

  **Výchozí**: Ano

- **Kontrolovat příchozí e-mailové zprávy**:  
  CSP: [Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Při nastavení Ano se prohledají poštovní schránka a e-mailové soubory, například PST, DBX, MNX, MIME a BINHEX. Pokud není nakonfigurovaný, nastavení se vrátí do výchozího nastavení klienta e-mailových souborů, které se nekontrolují.

  **Výchozí**: Ano

- **Kontrolovat vyměnitelné jednotky během úplného prohledávání**:  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  Když se nastaví na Ano, provedou se při úplné kontrole vyměnitelných jednotek (například jednotky USB Flash). Když se nastaví jako nenakonfigurované, nastavení se vrátí do výchozího klienta, který prohledá vyměnitelné jednotky, ale uživatel ho může zakázat.
  **Výchozí**: Ano  

- **Blokovat aplikacím Office vkládání kódu do jiných procesů**:  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872974)

  Při nastavení Ano budou aplikace Office zablokované v vkládání kódu do jiných procesů. Pokud je nastaveno pouze na audit, budou namísto blokování zavolány události systému Windows. Nastavení Nenakonfigurováno vrátí nastavení výchozí nastavení systému Windows, které je vypnuté. Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84

  **Výchozí**: blok

- **Blokovat aplikacím Office vytváření spustitelného obsahu**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872975)

  Pokud nastavíte Ano, aplikace Office nepovolí vytvoření spustitelného obsahu. Pokud je nastaveno pouze na audit, budou namísto blokování zavolány události systému Windows. Nastavení Nenakonfigurováno vrátí nastavení výchozí nastavení systému Windows, které je vypnuté. Toto pravidlo ASR se řídí pomocí následujícího identifikátoru GUID: 3B576869-A4EC-4529-8536-B80A7769E899

  **Výchozí**: blok

- **Zablokovat všechny aplikace Office z vytváření podřízených procesů**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872976)

  Při nastavení režimu auditování budou události systému Windows vyvolány namísto blokování. Nastavení Nenakonfigurováno vrátí nastavení výchozí nastavení systému Windows, které je vypnuté. Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A

  **Výchozí**: blok

- **Blokovat volání Win32 API z makra Office**:  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872977)

  Pokud je nastaveno na Ano, bude se pro makro Office zablokovat použití volání Win32 API. Pokud je nastaveno pouze na audit, budou namísto blokování zavolány události systému Windows. Nastavení Nenakonfigurováno vrátí nastavení výchozí nastavení systému Windows, které je vypnuté. Toto pravidlo ASR se řídí pomocí následujícího identifikátoru GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  
  **Výchozí**: blok

- **Zablokovat provádění potenciálně zablokovaných skriptů (js/vbs/PS)**:  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872978)

  Když je nastaveno na Ano, Defender zablokuje provádění zavedených skriptů. Pokud je nastaveno pouze na audit, budou namísto blokování zavolány události systému Windows. Nastavení Nenakonfigurováno vrátí nastavení výchozí nastavení systému Windows, které je vypnuté. Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  
  **Výchozí**: blok

- **Typ spuštění obsahu e-mailu**:    
  [Blokovat stahování spustitelného obsahu z e-mailu a klientů webové pošty](https://go.microsoft.com/fwlink/?linkid=872980)

  Pokud je nastaveno na Ano, spustitelný obsah stažený z e-mailu a klientů webové pošty se zablokuje. Pokud je nastaveno pouze na audit, budou namísto blokování zavolány události systému Windows. Nastavení Nenakonfigurováno vrátí nastavení výchozí nastavení systému Windows, které je vypnuté.

  **Výchozí**: blok

- **Zabránit krádeži pověření typu**:  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874499)
  
  Pokud je nastaveno na Ano, pokusy o odcizení přihlašovacích údajů prostřednictvím lsass.exe budou zablokovány. Pokud je nastaveno pouze na audit, budou namísto blokování zavolány události systému Windows. Nastavení Nenakonfigurováno vrátí nastavení výchozí nastavení systému Windows, které je vypnuté. Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2

  **Výchozí**: Povolit

- **Akce potenciálně nežádoucí aplikace v Defenderu**:  
  CSP: [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)+

  Funkce ochrany potenciálně nežádoucí aplikace (PUA) v antivirové ochraně v programu Microsoft Defender může identifikovat a blokovat PUAs ze stahování a instalace do koncových bodů ve vaší síti. Tyto aplikace nejsou považovány za viry, malware nebo jiné typy hrozeb, ale mohou provádět akce s koncovými body, které nepříznivě ovlivňují jejich výkon nebo použití. PUA může také odkazovat na aplikace, které se považují za nekvalitní pověst. Typické chování PUA zahrnuje různé typy softwaru, které je možné vydávat do ovladačů pro webové prohlížeče a optimalizace registru, které zjišťují problémy, vyžádají si platbu, aby opravila chyby, ale zůstaly na koncovém bodu a neobsahují žádné změny ani optimalizace (označované taky jako "neautorizovaný antivirový program"). Tyto aplikace můžou zvýšit riziko napadení vaší sítě malwarem, způsobit obtížnější nákazu malwaru a může obcházet prostředky IT při čištění aplikací.

  **Výchozí**: blok

- **Zablokovat nedůvěryhodné a nepodepsané procesy, které se spouštějí z USB**:  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=874502)
  
  Při nastavení Ano se zablokuje nedůvěryhodné a nepodepsané procesy, které se spouštějí z USB jednotky. Pokud je nastaveno pouze na audit, budou namísto blokování zavolány události systému Windows. Nastavení Nenakonfigurováno vrátí nastavení výchozí nastavení systému Windows, které je vypnuté. Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4

  **Výchozí**: blok

- **Ochrana sítě**:  
  [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  Pokud je nastaveno na Ano, bude ochrana sítě povolena pro všechny uživatele systému. Ochrana sítě chrání zaměstnance před přístupem k podvodným podvodům a škodlivému obsahu na internetu. Patří sem prohlížeče třetích stran. Když nastavení nastavíte jenom na audit, nebudou se uživatelé z nebezpečných domén zablokovat, ale místo toho se vyvolají události Windows. Nastavení Nenakonfigurováno vrátí nastavení výchozí nastavení systému Windows, které je zakázáno.

  **Výchozí**: Povolit

- **Typ souhlasu pro odeslání ukázky**v programu Defender:  
  [Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  Kontroluje, jestli se na úrovni souhlasu uživatele v programu Microsoft Defender odesílají data. Pokud je požadovaný souhlas již udělen, Microsoft Defender je odešle. V takovém případě se uživatelské rozhraní spustí, aby požádalo o souhlas uživatele (když je povolený program Defender/AllowCloudProtection) před odesláním dat.

  **Výchozí**: automaticky odesílat bezpečné vzorky

::: zone-end
::: zone pivot="mdm-may-2019"

- **Prohledat síťové soubory**  
  [Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049)

  - **Výchozí**: Ano

- **Blokování spouštění staženého spustitelného obsahu pomocí JavaScriptu nebo VBScript**  
  [Chránit zařízení před zneužitím](https://go.microsoft.com/fwlink/?linkid=872979)

  Když se nastaví hodnota Ano, Defender bude blokovat spouštění souborů JavaScript nebo VBScript, které byly staženy z Internetu. Pokud je nastaveno pouze na audit, budou namísto blokování zavolány události systému Windows. Nastavení Nenakonfigurováno vrátí nastavení výchozí nastavení systému Windows, které je vypnuté. Toto pravidlo ASR se ovládá pomocí následujícího identifikátoru GUID: D3E037E1-3EB8-44C8-A917-57927947596D

::: zone-end
::: zone pivot="mdm-may-2019,mdm-preview"

## <a name="ms-security-guide"></a>Průvodce zabezpečením MS

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – MSSecurityGuide](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-mssecurityguide) .

- **Použijte omezení nástroje řízení uživatelských účtů na místní účty při přihlášení k síti**:  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067188)

  **Výchozí**: povoleno

- **Konfigurace spuštění ovladače klienta SMB v1**:  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067214)

  **Výchozí**: zakázaný ovladač

- **Server SMB v1**:  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067190)

  **Výchozí**: zakázáno

- **Ověřování hodnotou hash**:  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067193)

  **Výchozí**: zakázáno

- **Ochrana před přepsáním strukturovaného zpracování výjimek**:  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067217)

  **Výchozí**: povoleno

## <a name="mss-legacy"></a>MSS – starší

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – MSSLegacy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-msslegacy) .

- **Úroveň ochrany směrování zdroje IP sítě**:  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067220)

  **Výchozí**: nejvyšší ochrana  

- **Síť ignoruje žádosti o vydání názvů NetBIOS s výjimkou serverů WINS**:  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067218)

  **Výchozí**: povoleno

- **Úroveň ochrany směrování zdrojového síťového protokolu IPv6**:  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067216)

  **Výchozí**: nejvyšší ochrana

- **Přesměrování sítě ICMP přepisují trasy vygenerované protokolem OSPF**:  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067326)

  **Výchozí**: zakázáno

## <a name="power"></a>Napájení

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – napájení](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-power) .

- **Vyžadovat heslo při probuzení během napájení**:  
  Nastavení této zásady určuje, jestli se uživateli zobrazí výzva k zadání hesla, když se systém obnoví z režimu spánku. Pokud nastavení této zásady povolíte nebo nenakonfigurujete, bude uživatel vyzván k zadání hesla, když se systém obnoví z režimu spánku. Pokud nastavení této zásady zakážete, uživatel nebude vyzván k zadání hesla, když se systém obnoví z režimu spánku.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067221)

  **Výchozí**: povoleno

- **Pohotovostní stav při přechodu do režimu spánku při napájení z baterie**:  
  Toto nastavení zásad spravuje, jestli systém Windows může použít pohotovostní stav při uvedení počítače do režimu spánku. Pokud nastavení této zásady povolíte nebo nenakonfigurujete, systém Windows použije pohotovostní stav k uvedení počítače do režimu spánku. Pokud toto nastavení zásad zakážete, nepovolí se pohotovostní stav (S1 – S3).  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067195)

  **Výchozí**: zakázáno

- **Pohotovostní stav při přechodu do režimu spánku během napájení**:  
  Toto nastavení zásad spravuje, jestli systém Windows může použít pohotovostní stav při uvedení počítače do režimu spánku. Pokud nastavení této zásady povolíte nebo nenakonfigurujete, systém Windows použije pohotovostní stav k uvedení počítače do režimu spánku. Pokud toto nastavení zásad zakážete, nepovolí se pohotovostní stav (S1 – S3).  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067196)

  **Výchozí**: zakázáno

- **Vyžadovat heslo při probuzení při napájení z baterie**:  
  Nastavení této zásady určuje, jestli se uživateli zobrazí výzva k zadání hesla, když se systém obnoví z režimu spánku. Pokud nastavení této zásady povolíte nebo nenakonfigurujete, bude uživatel vyzván k zadání hesla, když se systém obnoví z režimu spánku. Pokud nastavení této zásady zakážete, uživatel nebude vyzván k zadání hesla, když se systém obnoví z režimu spánku.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067322)

  **Výchozí**: povoleno

::: zone-end
::: zone pivot="mdm-may-2019"

## <a name="remote-assistance"></a>Vzdálená pomoc

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – RemoteAssistance](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-remoteassistance#remoteassistance-solicitedremoteassistance) .

- **Vyžádané vzdálené pomoci**:  
  Toto nastavení zásad umožňuje zapnout nebo vypnout funkci vyžádaná (požádat o) o vzdálenou pomoc na tomto počítači.
  
  - *Pokud nastavení této zásady povolíte*, mohou uživatelé v tomto počítači použít e-mail nebo přenos souborů a požádat někoho o pomoc. Uživatelé můžou taky používat programy pro rychlé zasílání zpráv k povolení připojení k tomuto počítači a můžete nakonfigurovat další nastavení vzdálené pomoci.

  - *Pokud nastavení této zásady zakážete*, uživatelé v tomto počítači nebudou moct pomocí e-mailu nebo přenosu souborů požádat někoho o pomoc. Uživatelé navíc nemohou použít programy pro rychlé zasílání zpráv k povolení připojení k tomuto počítači.

  - *Pokud nastavení této zásady*nenakonfigurujete, uživatelé můžou v Ovládacích panelech zapnout nebo vypnout funkci vyžádaná (požádat o) pro vzdálenou pomoc na ovládacím panelu Vlastnosti systému. Uživatelé můžou taky nakonfigurovat nastavení vzdálené pomoci.

  Pokud toto nastavení zásad povolíte, budete mít dva způsoby, jak pomocníkům umožnit poskytování vzdálené pomoci: "Povolit pomocníkům pouze zobrazit počítač" nebo "Povolit pomoc při vzdáleném řízení počítače." Nastavení "maximální doba lístku" Nastavuje omezení pro dobu, po kterou může být otevřené pozvání vzdálené pomoci vytvořené pomocí e-mailu nebo přenosu souborů. Nastavení vyberte metodu pro odesílání e-mailových pozvánek určuje, která e-mailová norma se má použít k odeslání pozvání vzdálené pomoci. V závislosti na e-mailovém programu můžete použít buď standard *mailto* (příjemce pozvánky prostřednictvím připojení k Internetu), nebo rozhraní SMAPI (Simple MAPI) Standard (Pozvánka je připojená k vaší e-mailové zprávě). Nastavení této zásady není k dispozici v systému Windows Vista, protože rozhraní SMAPI je jedinou podporovanou metodou. Pokud nastavení této zásady povolíte, měli byste taky povolit příslušné výjimky brány firewall, aby bylo možné povolit komunikaci vzdálené pomoci.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067198)

  **Výchozí**: zakázat vzdálenou pomoc

<!-- These settings are not available: 
  When set to *Enable Remote Assistance*, configure the following additional settings:

  - **Remote Assistance solicited permission**:  
    **Default**: View

  - **Maximum ticket time value**:  
    **Default**: *Not configured*

  - **Maximum ticket time period**:  
    **Default**: Minutes

  - **E-Mail invitation method**:  
    **Default**: Simple MAPI
-->

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

## <a name="remote-desktop-services"></a>Vzdálená plocha

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – RemoteDesktopServices](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-remotedesktopservices) .

- **Blokovat ukládání hesla**:  
  Určuje, jestli je možné ukládat hesla na tomto počítači z Připojení ke vzdálené ploše. Pokud povolíte toto nastavení, zaškrtávací políčko pro uložení hesla v Připojení ke vzdálené ploše je zakázané a uživatelé nebudou moct hesla ukládat. Když uživatel otevře soubor RDP pomocí Připojení ke vzdálené ploše a uloží jeho nastavení, odstraní se všechna hesla, která dříve existovala v souboru RDP. Pokud toto nastavení zakážete nebo necháte není nakonfigurované, může uživatel ukládat hesla pomocí Připojení ke vzdálené ploše.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067301)

   **Výchozí**: povoleno

- **Zabezpečená komunikace RPC**:  
  Určuje, jestli Hostitel relace vzdálené plochy Server vyžaduje zabezpečenou komunikaci RPC se všemi klienty, nebo umožňuje nezabezpečenou komunikaci. Pomocí tohoto nastavení můžete posílit zabezpečení komunikace RPC s klienty tím, že povolíte jenom ověřené a šifrované požadavky. Pokud je stav nastaven na povoleno, služba Vzdálená plocha přijímá žádosti od klientů RPC, které podporují zabezpečené požadavky, a nepovoluje nezabezpečenou komunikaci s nedůvěryhodnými klienty. Pokud je stav nastaven na zakázáno, služba Vzdálená plocha vždy vyžádá zabezpečení pro všechny přenosy RPC. Pro klienty RPC, kteří na žádost nereagují, se ale povoluje nezabezpečená komunikace. Pokud je stav nastavený na Nenakonfigurováno, je povolená nezabezpečená komunikace. Poznámka: rozhraní RPC se používá pro správu a konfiguraci služby Vzdálená plocha.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067248)

  **Výchozí**: povoleno

- **Zablokovat přesměrování jednotky**:  
  Nastavení této zásady určuje, jestli se má zabránit mapování klientských jednotek v relaci vzdálené plochy (přesměrování jednotky). Ve výchozím nastavení server Hostitel relace VP mapuje jednotky klienta automaticky po připojení. Mapované jednotky se zobrazí ve stromu složky relace v Průzkumníkovi souborů nebo v počítači ve formátu *\<driveletter>* zapnuto *\<computername>* . Toto chování můžete přepsat pomocí tohoto nastavení zásad. Pokud toto nastavení zásad povolíte, přesměrování jednotky klienta není v relacích služby Vzdálená plocha povoleno a přesměrování kopírování souborů ve schránce není povoleno v počítačích se systémem Windows Server 2003, Windows 8 a Windows XP. Pokud nastavení této zásady zakážete, přesměrování klientské jednotky je vždycky povolené. I když je povolené přesměrování schránky, přesměrování kopírování souborů ve schránce je vždycky povolené. Pokud nastavení této zásady nenakonfigurujete, přesměrování jednotky klienta a přesměrování kopírování souborů ve schránce nejsou zadané na úrovni Zásady skupiny.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067197)

  **Výchozí**: povoleno

- **Vyzvat k zadání hesla při připojení**:  
  Nastavení této zásady určuje, jestli služba Vzdálená plocha vždy po připojení vyzve klienta k zadání hesla. Toto nastavení můžete použít k vykonání výzvy k zadání hesla pro uživatele přihlášené ke vzdálené ploše, i když už heslo zadali v Připojení ke vzdálené ploše klientovi. Ve výchozím nastavení služba Vzdálená plocha umožňuje uživatelům, aby se automaticky přihlásili zadáním hesla v klientovi Připojení ke vzdálené ploše. Pokud nastavení této zásady povolíte, nebudou se uživatelé automaticky přihlašovat ke službě Vzdálená plocha zadáním hesel v klientovi Připojení ke vzdálené ploše. při přihlášení se zobrazí výzva k zadání hesla. Pokud nastavení této zásady zakážete, uživatelé se budou moct kdykoli přihlásit ke vzdálené ploše tak, že poskytnou svá hesla v klientovi Připojení ke vzdálené ploše. Pokud nastavení této zásady nenakonfigurujete, automatické přihlašování se na úrovni Zásady skupiny nezadá.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067328)

  **Výchozí**: povoleno

- **Úroveň šifrování připojení klienta služby Vzdálená plocha**:  
  Určuje, jestli se má vyžadovat použití konkrétní úrovně šifrování k zabezpečení komunikace mezi klientskými počítači a Hostitel relace VP servery během připojení protokol RDP (Remote Desktop Protocol) (RDP). Tato zásada platí jenom v případě, že používáte nativní šifrování RDP. Nativní šifrování RDP (na rozdíl od šifrování SSL) se ale nedoporučuje. Tato zásada se nevztahuje na šifrování SSL. Pokud nastavení této zásady povolíte, musí být při všech komunikacích mezi klienty a Hostitel relace VP servery používána metoda šifrování uvedená v tomto nastavení. Ve výchozím nastavení je úroveň šifrování nastavena na hodnotu Vysoká. K dispozici jsou následující metody šifrování:

  - *Vysoká* – vysoká hodnota nastavení šifruje data odesílaná z klienta na server a ze serveru do klienta pomocí silného 128-bitového šifrování. Tato úroveň šifrování se používá v prostředích, která obsahují jenom 128 klientů (například klientů se spuštěným Připojení ke vzdálené ploše). Klienti, kteří tuto úroveň šifrování nepodporují, se nemohou připojit k Hostitel relace VPm serverům.

  - *Kompatibilní s klientem* – nastavení kompatibilní s klientem šifruje data odesílaná mezi klientem a serverem s maximální silou klíče podporovanou klientem. Tato úroveň šifrování se používá v prostředích, která zahrnují klienty, kteří nepodporují 128 bitů šifrování.

  - *Nízká* – nastavení nízká šifruje pouze data odesílaná z klienta na server pomocí 56 bitového šifrování.  
  
  Pokud toto nastavení zakážete nebo nenakonfigurujete, úroveň šifrování, která se má použít pro vzdálené připojení k Hostitel relace VP servery, nebude využívána prostřednictvím Zásady skupiny. Důležité dodržování předpisů FIPS je možné nakonfigurovat prostřednictvím kryptografie systému. Použijte algoritmy kompatibilní se standardem FIPS pro nastavení šifrování, hashování a podepisování v Zásady skupiny (v části počítač \ zabezpečení \ \ Policies\Security možnosti.) Nastavení kompatibilní se standardem FIPS šifruje a dešifruje data odesílaná z klienta na server a ze serveru do klienta se šifrovacími algoritmy FIPS (Federal Information Processing Standard) 140 pomocí kryptografických modulů Microsoftu. Tato úroveň šifrování se používá v případě, že komunikace mezi klienty a Hostitel relace VP servery vyžaduje nejvyšší úroveň šifrování.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067222)

  **Výchozí**: vysoká

## <a name="remote-management"></a>Vzdálená správa

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – RemoteManagement](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-remotemanagement) .

- **Blokovat ukládání přihlašovacích údajů spustit jako**:  
  Základní ověřování klienta.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067300)

  **Výchozí**: povoleno

- **Základní ověřování**:  
  Toto nastavení zásad umožňuje spravovat, jestli služba Vzdálená správa systému Windows (WinRM) akceptuje základní ověřování od vzdáleného klienta. Pokud nastavení této zásady povolíte, služba WinRM přijme základní ověřování od vzdáleného klienta. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, služba WinRM nepřijme základní ověřování ze vzdáleného klienta.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067223)

  **Výchozí**: zakázáno

- **Zablokovat ověřování algoritmem Digest klienta**:  
  Toto nastavení zásad umožňuje spravovat, jestli klient Vzdálená správa systému Windows (WinRM) používá ověřování hodnotou hash. Pokud nastavení této zásady povolíte, klient WinRM nebude používat ověřování hodnotou hash. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, bude klient WinRM používat ověřování hodnotou hash.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067302)

  **Výchozí**: povoleno

- **Nešifrovaný provoz**:  
  Toto nastavení zásad umožňuje spravovat, jestli služba Vzdálená správa systému Windows (WinRM) odesílá a přijímá nešifrované zprávy přes síť. Pokud nastavení této zásady povolíte, klient WinRM odesílá a přijímá nešifrované zprávy přes síť. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, bude klient WinRM odesílat nebo přijímat pouze šifrované zprávy přes síť.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067226)

  **Výchozí**: zakázáno

- **Nešifrovaný provoz klienta**:  
  Toto nastavení zásad umožňuje spravovat, jestli klient Vzdálená správa systému Windows (WinRM) odesílá a přijímá nešifrované zprávy přes síť. Pokud nastavení této zásady povolíte, klient WinRM odesílá a přijímá nešifrované zprávy přes síť. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, bude klient WinRM odesílat nebo přijímat pouze šifrované zprávy přes síť.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067304)

  **Výchozí**: zakázáno

- **Základní ověřování klienta**:  
  Toto nastavení zásad umožňuje spravovat, jestli klient Vzdálená správa systému Windows (WinRM) používá základní ověřování. Pokud nastavení této zásady povolíte, bude klient WinRM používat základní ověřování. Pokud je služba WinRM nakonfigurovaná tak, aby používala přenos přes protokol HTTP, uživatelské jméno a heslo se přes síť odesílají jako nešifrovaný text. Pokud nastavení této zásady zakážete nebo nenakonfigurujete, klient WinRM nebude používat základní ověřování.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067252)

  **Výchozí**: zakázáno

## <a name="remote-procedure-call"></a>Vzdálené volání procedur

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – RemoteProcedureCall](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-remoteprocedurecall) .

- **Možnosti neověřeného klienta RPC**:  
  Nastavení této zásady určuje, jak bude modul runtime serveru RPC zpracovávat neověřené klienty RPC připojující se k serverům RPC. Nastavení této zásady má vliv na všechny aplikace RPC. V prostředí domény použijte nastavení této zásady opatrně, protože může mít vliv na celou řadu funkcí, včetně samotného zpracování zásad skupiny. Vrácení změny nastavení této zásady může vyžadovat ruční zásah na každém dotčeném počítači. Toto nastavení zásad nepoužívejte pro řadič domény. Pokud nastavení této zásady zakážete, bude modul runtime serveru RPC používat hodnotu "Ověřený" v klientovi Windows a hodnotu "žádné" ve verzích Windows serveru, které podporují toto nastavení zásad. Pokud nastavení této zásady nenakonfigurujete, zůstane zakázané. Modul runtime serveru RPC se chová, jako by byl povolen s hodnotou "ověřené" používané pro klienta Windows, a s hodnotou "none" použitou pro skladové položky serveru, které podporují toto nastavení zásad. Pokud nastavení této zásady povolíte, přesměruje modul runtime serveru RPC, aby omezil neověřené klienty RPC připojující se k serverům RPC běžícím v počítači. Klient se považuje za ověřeného klienta, pokud používá pojmenovaný kanál ke komunikaci se serverem nebo v případě, že používá zabezpečení RPC. Rozhraní RPC, která jsou výslovně vyžadovaná k přístupu neověřeným klientům, můžou být z tohoto omezení vyloučená v závislosti na zvolené hodnotě pro toto nastavení zásad.

  - *Žádné* umožňuje všem klientům RPC připojit se k serverům RPC běžícím na počítači, na kterém je nastavení zásad použito.

  - Možnost *ověřeno* umožňuje připojit se k serverům RPC běžícím na počítači, na kterém je nastavená zásada, jenom ověřeným klientům RPC (podle definice výše). Výjimky jsou udělovány rozhraním, která je požaduje.

  - *Ověřování bez výjimek* umožňuje připojit se k serverům RPC běžícím na počítači, na kterém je nastavená zásada, jenom ověřeným klientům RPC (podle definice výše). Nejsou povoleny žádné výjimky. Poznámka: nastavení této zásady se nepoužije, dokud se systém nerestartuje.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067225)

  **Výchozí**: ověřeno

## <a name="search"></a>Hledat

Další informace najdete v tématu [zásady CSP – hledání](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-search) v dokumentaci k Windows.

- **Zakázat indexování šifrovaných položek**:  
  Tato zásada povolí nebo zakáže indexování položek. Tento přepínač je určen pro indexer služby Windows Search, který určuje, zda budou zašifrovány položky, například soubory chráněné jako Windows Information Protection (nedokončené výroby). Pokud je tato zásada povolená, chráněné položky WIP se indexují a metadata o nich se ukládají do nešifrovaného umístění. Součástí metadat jsou takové položky jako cesta k souboru a datum změny. Když je zásada zakázaná, položky chráněné při nedokončené výrobě nejsou indexované a nezobrazují se ve výsledcích v Cortana nebo v Průzkumníkovi souborů. Pokud se v zařízení nachází mnoho souborů médií chráněných WIP, může to mít také dopad na výkon fotografií a aplikací Groove.  
  [Další informace]( https://go.microsoft.com/fwlink/?linkid=2067303)

  **Výchozí**: Ano

## <a name="smart-screen"></a>Inteligentní obrazovka

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – filtr](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen) .

::: zone-end
::: zone pivot="mdm-preview"

- **Zablokovat provádění neověřených souborů**:  
  Zablokuje uživateli spouštění neověřených souborů.

  - *Nenakonfigurováno* – zaměstnanci můžou ignorovat upozornění filtru SmartScreen a spouštět škodlivé soubory.

  - *Ano* – zaměstnanci nemůžou ignorovat upozornění filtru SmartScreen a spouštět škodlivé soubory.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067228)

  **Výchozí**: Ano

- **Vyžadovat filtr SmartScreen pro aplikace a soubory**:  
  Umožňuje správcům IT konfigurovat filtr SmartScreen pro Windows.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067168)

  **Výchozí**: Ano

::: zone-end
::: zone pivot="mdm-may-2019"

- **Zapnout filtr Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  Při nastavení Ano se vynutilo použití filtru SmartScreen pro všechny uživatele. Když nastavení nastavíte na Nenakonfigurováno, vrátí nastavení výchozí nastavení systému Windows, které povoluje filtr SmartScreen, ale uživatelé můžou toto nastavení změnit. Chcete-li zakázat filtr SmartScreen, použijte vlastní identifikátor URI.

  **Výchozí**: Ano

- **Zablokovat uživatelům ignorovat upozornění filtru SmartScreen**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  Pokud je nastaveno na Ano, je povolen filtr SmartScreen a uživatelé nemohou obejít upozornění pro soubory nebo škodlivé aplikace. Pokud je nastavené na Nenakonfigurováno, uživatelé můžou ignorovat upozornění filtru SmartScreen pro soubory a škodlivé aplikace.  

  Toto nastavení vyžaduje, aby se nastavení zapnout filtr SmartScreen pro Windows nastavilo na Ano.

  **Výchozí**: Ano

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

## <a name="system"></a>Systém

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – systém](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-system) .

- **Inicializace ovladače spuštění systému**:  
  Nastavení této zásady umožňuje určit, které spouštěcí ovladače se mají inicializovat, na základě klasifikace, která je určená ovladačem spuštění antimalwarového spuštění od předčasného spuštění. Spouštěcí ovladač předčasného spuštění antimalwarového spuštění může pro každý ovladač spouštěcího spuštění vrátit následující klasifikace:

  - *Dobrá* – ovladač je podepsaný a nebyl zfalšován.

  - *Chybné* – ovladač byl identifikován jako malware. Doporučujeme, abyste nepovolili inicializaci známých špatných ovladačů.

  - *Chybné, ale vyžaduje se pro spuštění* – ovladač byl identifikován jako malware, ale počítač nemůže úspěšně spustit bez načtení tohoto ovladače.

  - *Neznámý* – tento ovladač se nezískal na základě vaší aplikace pro detekci malwaru a neklasifikovaný ovladačem spuštění antimalwarového spuštění antimalwarového programu.

  Pokud nastavení této zásady povolíte, můžete zvolit, které ovladače spouštěcího spuštění se mají inicializovat při příštím spuštění počítače. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, budou ovladače spouštění pro spuštění správné, neznámé nebo chybné, ale kritické pro spouštění a inicializace ovladačů, které byly zjištěny jako chybné, budou vynechány. Pokud vaše aplikace pro detekci malwaru neobsahuje počáteční ovladač spuštění antimalwarové spouštěcí sady nebo pokud je vypnutý ovladač počátečního spuštění antimalwarové služby, nemá toto nastavení žádný vliv a všechny ovladače spouštěcího spuštění jsou inicializované.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067307)

  **Výchozí**: dobrý neznámý a špatný kritický

## <a name="wi-fi"></a>Wi-Fi

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – WiFi](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-wifi) .

- **Blokovat sdílení internetu**:  
  Určuje, jestli je na zařízení možné sdílení internetu.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067327)

  **Výchozí**: Ano

- **Blokovat automatické připojení k Wi-Fi hotspotům**:  
  Povolí nebo zakáže, aby se zařízení automaticky připojovala k Wi-Fi hotspotům.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067320)

  **Výchozí**: Ano

## <a name="windows-connection-manager"></a>Správce připojení k Windows

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – WindowsConnectionManager](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsconnectionmanager) .

- **Blokovat připojení k sítím mimo doménu**:  
  Nastavení této zásady zabraňuje počítačům v připojení k síti založené na doméně i k síti, která není založená na doméně. Pokud je toto nastavení zásad povolené, počítač reaguje na automatické a ruční pokusy o připojení k síti na základě následujících okolností:

  - *Automatické pokusy o připojení* – Pokud je počítač už připojený k síti založené na doméně, zablokují se všechny automatické pokusy o připojení k sítím, které nejsou v doméně. Pokud je počítač již připojen k síti založené na doméně, jsou blokovány automatické pokusy o připojení do sítí založených na doméně.

  - *Ruční pokusy o připojení* – Pokud je počítač už připojený k síti, která není založená na doméně, nebo k síti založené na doméně přes jiné médium než Ethernet a uživatel se pokusí vytvořit ruční připojení k další síti v rozporu s nastavením této zásady, dojde k odpojení stávajícího síťového připojení a ruční připojení je povolené. Pokud je počítač již připojen k síti založené na doméně nebo k síti založené na doméně přes síť Ethernet a uživatel se pokusí vytvořit ruční připojení k další síti s porušením tohoto nastavení zásad, bude zachováno existující připojení k síti Ethernet a je blokováno ruční pokus o připojení.

  Pokud nastavení této zásady není nakonfigurované nebo je zakázané, počítače se můžou současně připojit k doméně i k sítím, které nejsou v doméně.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067323)

  **Výchozí**: povoleno

::: zone-end
::: zone pivot="mdm-may-2019"

## <a name="windows-hello-for-business"></a>Windows Hello pro firmy

- **Blokovat Windows Hello pro firmy**  
  Windows Hello pro firmy je alternativní metoda pro přihlašování do systému Windows tím, že nahrazujete hesla, čipové karty a virtuální čipové karty. Pokud toto nastavení zásad zakážete nebo nenakonfigurujete, zařízení zřídí Windows Hello pro firmy. Pokud nastavení této zásady povolíte, zařízení nezřídí Windows Hello pro firmy pro žádného uživatele.

  **Výchozí**: povoleno
  
  Pokud je nastavené na *zakázáno*, můžete nakonfigurovat následující nastavení:

  - **Minimální délka PIN kódu**  
    Minimální délka kódu PIN musí být mezi 4 a 127.

    **Výchozí**: *Nenakonfigurováno*

  - **Povolit používání rozšířené ochrany proti falšování identity, pokud je dostupná**  
    [Ochrana proti falšování identity](https://go.microsoft.com/fwlink/?linkid=2067192)

    Pokud je tato možnost povolená, budou zařízení používat rozšířenou ochranu proti falšování identity, pokud je dostupná. Pokud není nakonfigurováno, bude dodržena konfigurace klienta pro ochranu proti falšování identity.

    **Výchozí**: Nenakonfigurováno

  - **Malá písmena v PIN kódu**:  
    V případě potřeby musí kód PIN uživatele obsahovat aspoň jedno malé písmeno.

    **Výchozí**: nepovolené

  - **Speciální znaky v PIN kódu**:  
    V případě potřeby musí kód PIN uživatele zahrnovat aspoň jeden speciální znak.

    **Výchozí**: nepovolené
 

  - **Velká písmena v PIN kódu**:  
    Pokud se to vyžaduje, PIN kód uživatele musí obsahovat aspoň jedno velké písmeno.

    **Výchozí**: nepovolené

::: zone-end
::: zone pivot="mdm-preview,mdm-may-2019"

## <a name="windows-ink-workspace"></a>Pracovní prostor Windows Ink

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – WindowsInkWorkspace](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsinkworkspace) .

- **Pracovní prostor rukopisu**:  
  Určuje, jestli má uživatel přístup k pracovnímu prostoru rukopisu.

  - *Zakázáno* – přístup k pracovnímu prostoru Ink je zakázán. Tato funkce je vypnutá.

  - *Povoleno* – funkce pracovní prostor rukopisu je zapnutá, ale uživatel k ní nemá přístup nad zamykací obrazovkou.

  - *Nenakonfigurováno* – funkce pracovní prostor rukopisu je zapnutá a uživatel ji může použít nad zamykací obrazovkou.

  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067241)

  **Výchozí**: povoleno

## <a name="windows-powershell"></a>Windows PowerShell

Další informace najdete v dokumentaci k Windows v tématu [zásady CSP – WindowsPowerShell](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowspowershell) .

- **Protokolování bloku skriptu PowerShellu**:  
  Nastavením této zásady lze povolit protokolování veškerého vstupu skriptu PowerShell do protokolu Microsoft-Windows-PowerShell/Operational Event Log. Pokud toto nastavení zásad povolíte, bude Windows PowerShell protokolovat zpracování příkazů, bloků skriptu, funkcí a skriptů – ať už se vyvolají interaktivně nebo prostřednictvím automatizace. Pokud nastavení této zásady zakážete, protokolování vstupu skriptu PowerShellu je zakázané. Pokud povolíte protokolování volání bloku skriptu, PowerShell kromě toho při vyvolání příkazu, bloku skriptu, funkce nebo skriptu spustí nebo zastaví protokol události. Povolení protokolování vyvolání generuje velké množství protokolů událostí. Poznámka: Toto nastavení zásad existuje v editoru Zásady skupiny v části Konfigurace počítače i Konfigurace uživatele. Nastavení zásad konfigurace počítače má přednost před nastavením zásad konfigurace uživatele.  
  [Další informace](https://go.microsoft.com/fwlink/?linkid=2067330)

  **Výchozí**: povoleno

::: zone-end
::: zone pivot="mdm-may-2019"

## <a name="whats-changed-in-the-new-template"></a>Co se změnilo v nové šabloně

Šablona *základní hodnoty zabezpečení MDM pro šablonu květen 2019* obsahuje následující změny v šabloně *Preview* .

### <a name="changes-to-the-baseline-settings"></a>Změny nastavení standardních hodnot

Následující nastavení:

- *Novinka* v této nejnovější verzi směrného plánu.
- *Odebral* z této nejnovější základní verze, ale byly k dispozici v předchozí verzi.
- *V některém ze způsobů, jak* se nastavení objevilo v předchozí verzi.

*[New]* [**nad zámkem**](#above-lock):

- **Hlasové aktivace aplikací z uzamčené obrazovky**

*[Nový]* [**Správa aplikací**](#application-management):

- **Blokovat uživatelský ovládací prvek pro instalace**
- **Blokovat instalaci MSI aplikace se zvýšenými oprávněními**

*[Odebrané]* [**BitLocker**](#bitlocker):

- Zásada pro vyměnitelné jednotky BitLockeru > **Metoda šifrování**
- **Zásady pevné jednotky BitLockeru** *(všechna nastavení)*
- **Zásady systémové jednotky BitLockeru** *(všechna nastavení)*

*[Nové]* [**připojení**](#connectivity):

- **Konfigurace zabezpečeného přístupu k cestám UNC**

*[Novinka]* [**Ochrana zařízení**](#device-guard):

- **Zabezpečení na základě virtualizace**

*[Nové]* [**ochrana DMA**](#dma-guard):

- **Výčet externích zařízení nekompatibilních s režimem ochrany DMA v jádře**

*[Nové]* [**Internet Explorer**](#internet-explorer):

- **Aktualizace internetových zón Internet Exploreru na stavovém řádku prostřednictvím skriptu**
- **Internet Explorer zóna Internetu přetahování nebo kopírování a vkládání souborů**
- **Zóna s omezeným přístupem v Internet Exploreru .NET Framework závislé součásti**
- **Zóna místního počítače v aplikaci Internet Explorer nespouští antimalware proti ovládacím prvkům ActiveX**
- **Podpora šifrování v aplikaci Internet Explorer**

*[Revidované]* [**Internet Explorer**](#internet-explorer):

- **Automaticky vyzvat k stažení souborů** v Internet Exploreru internet Zone > výchozí hodnota je teď **zakázaná**. Ve verzi Preview bylo toto nastavení nastaveno na povoleno.

*[Nová]* [**Vzdálená pomoc**](#remote-assistance):

- **Vyžádané vzdálené pomoci**
  - **Žádosti o vzdálenou pomoc – vyžádaná oprávnění**
  - **Maximální hodnota času lístku**
  - **Maximální časové období lístku**
  - **Metoda pozvánky e-mailu**

*[Novinka]* [**Microsoft Defender**](#microsoft-defender):

- **Spuštění aplikace Adobe Reader v podřízeném procesu**
- **Aplikace Office Communications se spouští v podřízeném procesu**

*[New]* [ **Brána firewall**](#firewall)

- **Doména profilu brány firewall**
  - **Blokovaná příchozí připojení**
  - **Vyžadují se odchozí připojení.**
  - **Blokovaná příchozí oznámení**
  - **Povolená brána firewall**
- **Veřejný profil brány firewall**
  - **Blokovaná příchozí připojení**
  - **Vyžadují se odchozí připojení.**
  - **Blokovaná příchozí oznámení**
  - **Povolená brána firewall**
  - **Pravidla zabezpečení připojení ze zásad skupiny nejsou sloučena.**
  - **Pravidla zásad ze zásad skupiny nejsou sloučena.**
- **Profil brány firewall Private**
  - **Blokovaná příchozí připojení**
  - **Vyžadují se odchozí připojení.**
  - **Blokovaná příchozí oznámení**
  - **Povolená brána firewall**

*[Nové]* [**Windows Hello pro firmy**](#windows-hello-for-business):

- **Vyžadovat rozšířenou ochranu proti falšování identity, pokud je dostupná**
- **Konfigurace Windows Hello pro firmy**
- **Vyžadovat v PIN kódu malá písmena**
- **Vyžadovat speciální znaky v PIN kódech**
- **Minimální délka PIN kódu**
- **Vyžadovat v PIN kódu velká písmena**

::: zone-end

## <a name="next-steps"></a>Další kroky

- [Další informace o standardních hodnotách zabezpečení](security-baselines.md)
- [Vyhnout se konfliktům](security-baselines.md#avoid-conflicts)
- [Řešení potíží se zásadami a profily v Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
