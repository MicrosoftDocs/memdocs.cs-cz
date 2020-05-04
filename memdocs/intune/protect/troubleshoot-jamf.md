---
title: Řešení potíží s integrací Jamf pro s Microsoft Intune
titleSuffix: Microsoft Intune
description: Návrhy pro řešení některých nejběžnějších problémů při integraci zařízení Jamf pro pro Mac s Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49749ec3a839b11062b1cc2655a1cca4e3d6cfb0
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81525696"
---
# <a name="troubleshoot-integration-of-jamf-pro-with-microsoft-intune"></a>Řešení potíží s integrací Jamf pro s Microsoft Intune

Tento článek pomáhá správcům Intune pochopit a řešit problémy s integrací Jamf pro pro macOS s Intune.

> [!TIP]  
> Většina informací v tomto článku se původně objevila při [řešení potíží při integraci Jamf s Microsoft Intune](https://support.microsoft.com/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune) v support.Microsoft.com.

## <a name="prerequisites"></a>Požadavky

Než začnete s odstraňováním potíží, shromážděte některé základní informace pro objasnění problému a zkrácení doby hledání řešení. Například pokud narazíte na problém související s integrací Jamf-Intune, vždy ověřte, že byly splněny všechny požadavky. Než začnete řešit potíže, přečtěte si následující skutečnosti:

- V závislosti na tom, jak nakonfigurujete integraci Jamf pro s Intune, si přečtěte požadavky z následujících článků:
  - [Integrace Jamf pro s Intune pomocí cloudového konektoru Jamf](conditional-access-jamf-cloud-connector.md)
  - [Integrace Jamf pro s Intune](conditional-access-integrate-jamf.md#prerequisites)
- Všichni uživatelé musí mít licence Microsoft Intune a Microsoft AAD Premium P1.
- V konzole Jamf pro musíte mít uživatelský účet, který má oprávnění Microsoft Intune Integration.
- Musíte mít uživatelský účet, který má v Azure oprávnění globálního správce.

Při zkoumání integrace Jamf pro s Intune Vezměte v úvahu následující informace:

- Jaké je přesné znění chybové zprávy?
- Kde je chybová zpráva?
- Kdy tento problém začal?  Pracovala integrace s Jamf pro s Intune neustále?
- Kolik uživatelů je ovlivněno? Ovlivnili všichni uživatelé nebo jen některé?
- Kolik zařízení je ovlivněno? Jsou všechna zařízení ovlivněná nebo jenom některá?
 
## <a name="common-problems"></a>Běžné problémy

Následující informace vám pomůžou identifikovat a vyřešit běžné problémy pro zařízení po nastavení integrace Intune a Jamf pro.  

| Problém   | Další informace                  |
|-----------------|--------------------------|
| **Zařízení se v Jamf pro označí jako nereagující.**  | [Zařízení se nepodařilo zaregistrovat pomocí Jamf pro nebo pomocí Azure AD.](#devices-are-marked-as-unresponsive-in-jamf-pro) |
| **Zařízení se systémem Mac se při spuštění přihlášení k řetězci klíčů při otevření zařízení aplikace vyzvat k chybě registrace**  | [Uživatelům se zobrazí výzva k zadání hesla, aby se aplikace mohla registrovat ve službě Azure AD](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app). |
| **Registrace zařízení se nezdařila**  | Můžou se vztahovat následující příčiny: <br> **-**[ ***Příčina 1*** – aplikace Jamf pro v Azure má nesprávná oprávnění](#cause-1) <br> **-**[ ***Příčina 2*** – došlo k potížím s *konektorem Jamf Native MACOS* ve službě Azure AD.](#cause-2) <br> **-**[ ***Příčina 3*** – uživatel nemá platnou licenci Intune nebo Jamf.](#cause-3) <br> **-**[ ***Příčina 4*** – uživatel nepoužívá samoobslužnou službu Jamf ke spuštění aplikace Portál společnosti.](#cause-4) <br> **-**[ ***Příčina 5*** – integrace Intune je vypnutá](#cause-5) <br> **-**[ ***Příčina 6*** – zařízení bylo dříve zaregistrováno v Intune nebo se uživatel pokusil zaregistrovat zařízení vícekrát](#cause-6) <br> **-**[ ***Příčina 7*** -JamfAAD žádá o přístup k klíči Microsoft Workplace Joinu z řetězce klíčů uživatelů](#cause-7) |
|  **Zařízení Mac zobrazuje vyhovující předpisy v Intune, ale nedodržuje předpisy v Azure.** | [Problémy s registrací zařízení](#mac-device-shows-compliant-in-intune-but-noncompliant-in-azure) |
| **V konzole Intune pro zařízení Mac, které jsou zaregistrované pomocí Jamf, se zobrazí duplicitní položky.** | [Několik registrací má stejné zařízení.](#duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf) |
| **Zásada dodržování předpisů nedokáže vyhodnotit zařízení** | [Zásady cílí na skupiny zařízení.](#compliance-policy-fails-to-evaluate-the-device) |
| **Nepovedlo se načíst přístupový token pro rozhraní Microsoft Graph API.** | Můžou se vztahovat následující příčiny: <br> -[Oprávnění pro aplikaci Jamf pro v Azure](#theres-a-permission-issue-with-the-jamf-pro-application-in-azure) <br> - [Vypršela licence pro Jamf nebo Intune](#a-license-required-for-jamf-intune-integration-has-expired) <br> **-**[Porty nejsou otevřené](#the-required-ports-arent-open-on-your-network) .|
 

### <a name="devices-are-marked-as-unresponsive-in-jamf-pro"></a>Zařízení se v Jamf pro označí jako nereagující.  

**Příčina**: v následujícím seznamu jsou běžné příčiny zařízení označená jako *nereagující* nástrojem Jamf pro:

- Zařízení se nepodařilo vrátit se změnami pomocí Jamf pro.  
  Jamf pro očekává, že se zařízení zaregistrují každých 15 minut. Zařízení jsou označena jako nereagující Jamf, když se nepodaří zaregistrovat se za 24 hodin.  

- Zařízení se nepodařilo zaregistrovat se pomocí Azure AD.  
  Po úspěšné registraci do Azure AD obdrží zařízení macOS token Azure:
  - Tento token se aktualizuje každých 12 hodin.   
  - Pokud se neúspěšná aktualizace tokenu na 24 hodin nebo více, Jamf pro zařízení označí jako nereagující.  
  - Pokud vyprší platnost tokenu Azure, zobrazí se uživatelům výzva, abyste se přihlásili k Azure a získali nový token. Obnovovací token pro Azure Access se vygeneruje každých 7 dní.

**Rozlišení**  
Po označení *zařízení jako nereagující* Jamf pro se musí zaregistrovaný uživatel zařízení přihlásit a opravit nereagující stav. Musí to být uživatel, který má k účtu připojený pracovní vztah, protože má v přihlašovacím řetězci pro přihlášení identitu z Intune.



### <a name="mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app"></a>Zařízení Mac – při otevření aplikace se zobrazí výzva pro přihlášení k řetězci klíčů  

Když nakonfigurujete integraci Intune a Jamf pro a nasadíte zásady podmíněného přístupu, zobrazí se uživatelům zařízení spravovaných pomocí Jamf pro heslo při otevírání aplikací systém Microsoft Office 365, jako jsou týmy, Outlook a další aplikace, které vyžadují ověřování Azure AD. 

Například při otevření Microsoft Teams se zobrazí výzva s textem podobným následujícímu příkladu:

``` 
  Microsoft Teams wants to sign using key "Microsoft Workplace Join Key" in your keychain.  
  To allow this, enter the "login" keychain password 
```

**Příčina**: tyto výzvy vygeneruje Jamf pro pro každou platnou aplikaci, která vyžaduje registraci Azure AD. 

**Rozhodnutí**   
V příkazovém řádku musí uživatel pro přihlášení ke službě Azure AD zadat heslo zařízení. Mezi možnosti patří:
- **Odepřít** – Přihlaste se a nepoužívejte aplikaci.
- **Povolení** – jednorázové přihlášení Při příštím spuštění aplikace se zobrazí výzva k opětovnému přihlášení.
- **Vždy povoleno** – přihlašovací údaje pro aplikaci jsou ukládány do mezipaměti. Při dalším spuštění aplikace se nezobrazí výzva k přihlášení.  

Výběr možnosti *vždy povolit* pro jednu aplikaci schválí pouze tuto aplikaci pro budoucí přihlášení. Další aplikace se zobrazí při ověřování, dokud nejsou nastavené jako *vždy povolené*. Přihlašovací údaje uložené v mezipaměti pro jednu aplikaci nejde použít v jiné aplikaci.  

### <a name="devices-fail-to-register"></a>Registrace zařízení se nezdařila  

K dispozici je několik běžných příčin pro zařízení Mac, která se nepodaří zaregistrovat.  

#### <a name="cause-1"></a>Příčina 1  

**Podniková aplikace Jamf pro v Azure má nesprávné oprávnění nebo má více než jedno oprávnění.**

  Když vytváříte aplikaci v Azure, musíte odebrat všechna výchozí oprávnění rozhraní API a potom přiřadit Intune jedno oprávnění *update_device_attributes*. 

  **Rozlišení**  
  Zkontrolujte a v případě potřeby opravte oprávnění pro aplikaci Jamf. Pokud používáte cloudový konektor Jamf pro, vytvořila se tato aplikace za vás. Pokud jste integraci nakonfigurovali ručně, vytvořili jste aplikaci ve službě Azure AD. Oprávnění aplikace najdete v postupu [Vytvoření aplikace pro Jamf ve službě Azure AD](conditional-access-integrate-jamf.md#create-an-application-in-azure-active-directory).

#### <a name="cause-2"></a>Příčina 2  

**V tenantovi Azure AD se nevytvořila aplikace **konektoru Jamf Native MacOS** ani se pro tento konektor podepsal účet, který nemá oprávnění globálního správce.**  

  **Rozlišení**  
  Informace najdete v části *Konfigurace integrace MacOS Intune* v tématu [integrace s Microsoft Intune](https://docs.jamf.com/10.13.0/jamf-pro/administrator-guide/Integrating_with_Microsoft_Intune.html) v docs.jamf.com.

#### <a name="cause-3"></a>Příčina 3

**Uživatel nemá platnou licenci Intune nebo Jamf.**

  Chybějící platná licence může vést k následující chybě, která indikuje, že platnost licence Jamf vypršela:  
  ```
    Unable to connect to Microsoft Intune.  
    
    Check your Microsoft Intune Integration configuration.
  ```  

  **Rozlišení**
  - Jamf licence: obraťte se na Jamf s žádostí o pomoc, abyste získali novou licenci pro Jamf.  
  - Licence Intune: přiřaďte uživateli platnou licenci nebo kontaktujte společnost Microsoft nebo svého partnera, kde najdete informace o tom, jak získat aktuální licenci.

#### <a name="cause-4"></a>Příčina 4  

**Uživatel nepoužívá *samoobslužnou službu Jamf* ke spuštění aplikace Portál společnosti.**

Aby se zařízení úspěšně zaregistrovalo a zaregistrovalo v Intune prostřednictvím Jamf, musí uživatel pomocí samoobslužné služby Jamf otevřít Portál společnosti Intune. Pokud uživatel otevře portál společnosti ručně, zařízení se zaregistruje a zaregistruje bez připojení k Jamf.  

Pokud chcete zjistit, která služba zařízení použila k registraci a registraci, podívejte se na Portál společnosti aplikaci na zařízení. Při registraci prostřednictvím Jamf byste měli obdržet oznámení o otevření samoobslužné aplikace, aby provedla změny.

V aplikaci Portál společnosti se uživatel může zobrazit **`Not registered`** a v protokolech portál společnosti se může zobrazit položka podobná následujícímu příkladu:  

```
   Line 7783: <DATE> <IP ADDRESS> INFO com.microsoft.ssp.application TID=1  
 
   WelcomeViewController.swift: 253 (startLogin()) Portal launched without WPJ only arg while account is under partner management
```

**Rozlišení**  
Změna zdroje registrace z Intune na Jamf:
1. Zruší [registraci zařízení MacOS v Intune](https://docs.microsoft.com/mem/intune/user-help/unenroll-your-device-from-intune-macos). Aby nedocházelo k dalším komplikacím u zařízení, která nejsou úplně odebrána z Intune, přečtěte si část [*Příčina 6*](#cause-6) v tomto seznamu příčin.  

2. V zařízení pomocí samoobslužné služby Jamf otevřete aplikaci Portál společnosti a pak zařízení Zaregistrujte v Intune. Tato úloha vyžaduje, abyste [použili Jamf k nasazení aplikace Portál společnosti pro MacOS](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro)a [vytvořili zásadu v Jamf pro, která zaregistruje zařízení uživatelů do služby Azure AD](conditional-access-assign-jamf.md#create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory).  

3. Po otevření portálu se zobrazí první obrazovka, která vás vyzve k přihlášení. Použití pracovního nebo školního účtu  

4. Portál společnosti potvrdí informace o účtu a zobrazí vaše registrace zařízení a stav dodržování předpisů zařízením. Žlutými trojúhelníky jsou zvýrazněny akce, které je potřeba provést k zabezpečení zařízení s macOS pro školní nebo pracovní účely. Kliknutím na Začít spusťte registraci.  

5. Pokud se zobrazí výzva, zadejte přihlašovací údaje počítače.  
     
Registrace zařízení do správy může trvat několik minut. Během toho ale můžete se zařízením pracovat. Jakmile se dokončí nastavení přístupu společnosti, zobrazí se zpráva, že je vše hotovo.

#### <a name="cause-5"></a>Příčina 5  

**Integrace Intune je vypnutá.**

Pokud je integrace Intune vypnutá, uživatelé při pokusu o registraci zařízení obdrží v Portál společnosti automaticky otevírané okno s následující zprávou:  

```
   Invalid command line input
   
   Registration-only command line flag (-r) can only be used when partner management is enabled in Intune. Please contact your IT admin.
```  

Server Jamf pro pošle pulsi serverům Intune, když je vypnutá integrace, která oznamuje Intune, že integrace je zakázaná. 

**Rozlišení**  
Znovu povolit integraci Intune v Jamf pro. Podívejte se na následující informace v závislosti na tom, jak nakonfigurujete integraci:

- [Integrace Jamf pro s Intune pomocí cloudového konektoru Jamf](conditional-access-jamf-cloud-connector.md)
- [Ručně nakonfigurujte integraci Microsoft Intune v Jamf pro](conditional-access-integrate-jamf.md#enable-intune-to-integrate-with-jamf-pro).

#### <a name="cause-6"></a><a name="cause-6"></a>Příčina 6  

**Zařízení bylo dřív zaregistrované v Intune nebo se uživatel pokusil zaregistrovat zařízení víckrát.**

Pokud je zařízení odregistrované z Jamf, ale není správně odebrané z Intune nebo se provede několik pokusů o registraci, můžete na portálu zobrazit víc instancí stejného zařízení. To způsobí selhání registrace Jamf.

**Rozlišení**  
1. Na Macu spusťte **terminál**.
2. Spusťte **sudo JAMF removemdmprofile**.
3. Spusťte **sudo JAMF removeFramework**.
4. Na serveru JAMF pro odstraňte záznam inventáře počítače.
5. Odstraňte zařízení z AzureAD.
6. V zařízení odstraňte následující soubory, pokud existují:
   - /Library/Application Support support/com. Microsoft. CompanyPortal. UserContext. info
   - /Library/Application Support support/com. Microsoft. CompanyPortal
   - /Library/Application Support support/com. jamfsoftware. samoobslužný. Mac
   - Aplikace/Library/Saved
   - State/com. jamfsoftware. samoobslužný. Mac. savedState
   - Stav aplikace/Library/Saved/com. Microsoft. CompanyPortal. savedState
   - /Library/Preferences/com.microsoft.CompanyPortal.plist
   - /Library/Preferences/com.jamfsoftware.selfservice.mac.plist
   - /Library/Preferences/com.jamfsoftware.management.jamfAAD.plist
   - /Users/<username>/Library/cookies/com.Microsoft.CompanyPortal.binarycookies
   - /Users/<username>/Library/cookies/com.jamf.Management.jamfAAD.binarycookies
   - com. Microsoft. CompanyPortal
   - com. Microsoft. CompanyPortal. HockeySDK
   - enterpriseregistration.windows.net
   - https://device.login.microsoftonline.com
   - https://device.login.microsoftonline.com/
   - Přenosový klíč relace Microsoft (veřejné a privátní klíče)
   - Klíč Microsoft Workplace Join Key (veřejné a privátní klíče)
7. Odstraňte cokoli z řetězce klíčů na zařízení, které odkazuje na *Microsoft*, *intune*nebo *portál společnosti*, včetně certifikátů DeviceLogin.Microsoft.com. Odeberte odkazy *JAMF* s výjimkou veřejného a privátního klíče JAMF. 
   > [!IMPORTANT]  
   > Odebrání veřejného a soukromého klíče zruší registraci zařízení.

8. Odstraňte libovolnou z následujících položek, které najdete:  
   - Druh: heslo aplikace; Účet: com. Microsoft. workplacejoin. kryptografický otisk
   - Druh: heslo aplikace; Účet: com. Microsoft. workplacejoin. registeredUserPrincipalName
   - Druh: certifikát; Vystavitel: MS-Organization-Access
   - Druh: preference identity; Název (adresa URL služby ADFS STS, pokud je k dispozici):https://adfs\<DNSName>.com/adfs/ls
   - Druh: preference identity; Jméno:`https://enterpriseregistration.windows.net`
   - Druh: preference identity; Jméno:`https://enterpriseregistration.windows.net/`
9. Restartujte zařízení Mac.
10. Odinstalujte Portál společnosti ze zařízení.
11. Přejít na portal.manage.microsoft.com a odstranit všechny instance zařízení Mac. Před přechodem k dalšímu kroku počkejte aspoň 30 minut.
12. Znovu zaregistrujte zařízení v JAMF pro.
13. Znovu otevřete samoobslužné služby a spusťte zásadu registrace.


#### <a name="cause-7"></a>Příčina 7  

**JamfAAD žádá o přístup k klíči Microsoft Workplace Joinu z řetězce klíčů uživatele.**

Během registrace obdrží uživatel zařízení macOS následující výzvu, aby JamfAAD přístup k klíči ze svého řetězce klíčů: 

```
   JamfAAD wants to access key "Microsoft Workplace Join Key" in your keychain. 
    
   To allow this, enter the "login" keychain password
```

**Rozlišení**  
Aby bylo možné zařízení úspěšně zaregistrovat do Azure AD, Jamf vyžaduje, aby uživatel poskytoval heslo k účtu, a vyberte možnost **udělit**.

Tato žádost se podobá žádosti o [přihlášení k řetězci pro řetězce klíčů v počítačích Mac, když otevřete aplikaci](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app), dříve v tomto článku.  

 
### <a name="mac-device-shows-compliant-in-intune-but-noncompliant-in-azure"></a>Zařízení Mac zobrazuje vyhovující předpisy v Intune, ale nedodržuje předpisy v Azure.  

**Příčina**: následující podmínky můžou způsobit, že se zařízení v Intune zobrazí jako kompatibilní, ale ne jako vyhovující předpisům v Azure:  
- Zařízení není správně zaregistrované.  
- Zařízení bylo zaregistrováno několikrát bez nezbytného vyčištění.

**Rozlišení**  
Pokud chcete tento problém vyřešit, postupujte podle pokynů v části [*Příčina 6*](#cause-6) , aby se zařízení nepovedlo *zaregistrovat*, výše v tomto článku. 


### <a name="duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf"></a>V konzole Intune pro zařízení Mac, které jsou zaregistrované pomocí Jamf, se zobrazí duplicitní položky.  
 
**Příčina**: zařízení je zaregistrované v Intune několikrát, obvykle se registruje po jeho odebrání z Intune.  

Když se zařízení odebere z integrace Intune a Jamf pro, mohou být některá data ponechána za tím, že by mohlo dojít k následným registrům při vytváření duplicitních položek.  

**Rozlišení**  
Pokud chcete tento problém vyřešit, postupujte podle pokynů v části [*Příčina 6*](#cause-6) , aby se zařízení nepovedlo *zaregistrovat*, výše v tomto článku.

### <a name="compliance-policy-fails-to-evaluate-the-device"></a>Zásada dodržování předpisů nedokáže vyhodnotit zařízení  

**Příčina**: integrace Jamf s Intune nepodporuje zásady dodržování předpisů, které cílí na skupiny zařízení.

**Rozlišení**  
Upravte zásady dodržování předpisů pro zařízení macOS, která se mají přiřadit ke skupinám uživatelů.

### <a name="could-not-retrieve-the-access-token-for-microsoft-graph-api"></a>Nepovedlo se načíst přístupový token pro rozhraní Microsoft Graph API.

Zobrazí se následující chyba:

`Could not retrieve the access token for Microsoft Graph API. Check the configuration for Microsoft Intune Integration.`

Zdrojem této chyby může být jeden z následujících příčin:

#### <a name="theres-a-permission-issue-with-the-jamf-pro-application-in-azure"></a>Došlo k potížím s oprávněním pro aplikaci Jamf pro v Azure.

Při registraci aplikace Jamf pro v Azure došlo k jedné z následujících podmínek:

- Aplikace přijala více než jedno oprávnění.
- Nebyla vybrána možnost **udělení souhlasu správce * \<vaší společnosti>* ** .  

**Rozlišení**  
Podívejte se na řešení příčin 1, kdy [se zařízení nepodaří zaregistrovat](#devices-fail-to-register), výše v tomto článku.

#### <a name="a-license-required-for-jamf-intune-integration-has-expired"></a>Platnost licence vyžadované pro integraci Jamf-Intune vypršela.

**Řešení**: Podívejte se na řešení pro příčinu 3, že [se zařízení nepodaří zaregistrovat](#devices-fail-to-register).

#### <a name="the-required-ports-arent-open-on-your-network"></a>Požadované porty nejsou v síti otevřené.

**Řešení**:  
Přečtěte si informace o síťových portech v části [předpoklady](conditional-access-jamf-cloud-connector.md#prerequisites) pro integraci Jamf pro s Intune.

## <a name="next-steps"></a>Další kroky

Další informace o [integraci Jamf pro s Intune](conditional-access-integrate-jamf.md)