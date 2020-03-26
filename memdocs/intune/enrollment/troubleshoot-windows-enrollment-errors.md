---
title: Řešení potíží s registrací zařízení s Windows v Microsoft Intune
titleSuffix: Microsoft Intune
description: Návrhy pro řešení některých nejběžnějších problémů při registraci zařízení s Windows v Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/29/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 128b63f2b7b789fdd6a11fb196c4d92b14a88cf0
ms.sourcegitcommit: fe7484e86ec8a109fa5f54fe9cceef8aac94bd9f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/26/2020
ms.locfileid: "80274825"
---
# <a name="troubleshoot-windows-device-enrollment-problems-in-microsoft-intune"></a>Řešení potíží s registrací zařízení s Windows v Microsoft Intune

Tento článek pomáhá správcům Intune pochopit a řešit problémy při registraci zařízení s Windows v Intune.

## <a name="prerequisites"></a>Požadavky
Než začnete řešit potíže, je důležité shromáždit některé základní informace. Tyto informace vám pomůžou lépe porozumět problému a zkrátit dobu, po kterou je možné najít řešení.

Shromážděte následující informace o problému:
- Má uživatel přiřazenou platnou licenci Intune? Než si uživatelé můžou zaregistrovat svoje zařízení, musí mít přiřazenou potřebnou licenci.
- Je na zařízení s Windows nainstalovaná nejnovější aktualizace? Některé funkce Intune fungují jenom s nejnovější verzí Windows. K dispozici je mnoho oprav pro známé problémy, které jsou dostupné prostřednictvím web Windows Update. Použití všech nejnovějších aktualizací často řeší potíže s registrací zařízení s Windows. 
- Jaká je přesná chybová zpráva?
- Kde se zobrazí chybová zpráva?
- Kdy problém začal? Byl zápis někdy zpracován? 
- Jakou platformu (Android, iOS/iPadOS, Windows) má problém?
- Kolika uživatelů se to týká? Ovlivnili všichni uživatelé nebo jen některé?
- Kolik zařízení je ovlivněno? Jsou všechna zařízení ovlivněná nebo jenom některá?
- Co je Autorita MDM?
- Jak se provádí registrace? Znamená to, že vlastní zařízení (BYOD) nebo Apple automatického zápisu zařízení (ADE) pomocí registračních profilů?

## <a name="error-messages"></a>Chybovými zprávami

### <a name="this-user-is-not-authorized-to-enroll"></a>Tento uživatel nemá autorizaci k registraci.

Chyba 0x801c003: Tento uživatel nemá oprávnění k registraci. Můžete to zkusit znovu nebo se obraťte na správce systému a sdělte mu kód chyby (0x801c0003). "
Chyba 80180003: něco se pokazilo. Tento uživatel nemá autorizaci k registraci. Můžete to zkusit znovu nebo se obraťte na správce systému s kódem chyby 80180003. "

**Příčina:** Kterákoli z následujících podmínek: 

- Uživatel už zaregistroval maximální počet zařízení povolených v Intune.    
- Zařízení je blokováno omezeními typů zařízení.    
- V počítači je spuštěný systém Windows 10 Home. Registrace v Intune nebo připojení služby Azure AD je ale podporovaná jenom v edicích Windows 10 pro a vyšší.

#### <a name="resolution"></a>Rozlišení
Tento problém může být několik možných řešení:

##### <a name="remove-devices-that-were-enrolled"></a>Odebrat zařízení, která byla zaregistrována
1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).    
2. Přejít na **uživatele** > **všech uživatelích**.    
3. Vyberte příslušný účet uživatele a pak klikněte na **zařízení**.    
4. Vyberte všechna nepoužívaná nebo nežádoucí zařízení a pak klikněte na **Odstranit**. 

##### <a name="increase-the-device-enrollment-limit"></a>Zvýšení limitu pro registraci zařízení

> [!NOTE]
> Tato metoda zvyšuje limit pro registraci zařízení pro všechny uživatele, nikoli jenom ovlivněného uživatele.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. V části **zařízení** > **omezení registrace** > **výchozí** (v části **omezení počtu zařízení**) > **vlastnosti** > **Upravit** (u možnosti **limit zařízení**) > zvyšte **limit počtu zařízení** (maximálně 15) > **zkontrolovat + Uložit**.    
 

##### <a name="check-device-type-restrictions"></a>Ověřit omezení typu zařízení
1. Přihlaste se k [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431) pomocí účtu globálního správce.
2. V části **zařízení** > **omezení registrace**a v části **omezení typů zařízení**vyberte **výchozí** omezení.    
3. Vyberte **platformy**a pak vyberte možnost **Povolení** pro **Windows (MDM)** .

    > [!IMPORTANT]
    > Pokud je aktuální nastavení již **povoleno**, změňte ho na **blokovat**, uložte nastavení a pak ho změňte zpět na **povoleno** a uložte nastavení znovu. Tím se obnoví nastavení registrace.

4. Počkejte asi 15 minut a pak příslušné zařízení znovu zaregistrujte.    

##### <a name="upgrade-windows-10-home"></a>Upgradovat domovskou stránku Windows 10
[Upgradujte Windows 10 Home na Windows 10 pro](https://support.microsoft.com/help/12384/windows-10-upgrading-home-to-pro) nebo vyšší edici. 



### <a name="this-user-is-not-allowed-to-enroll"></a>Tento uživatel není povolen k registraci.

Chyba 0x801c0003: Tento uživatel není povolen k registraci. Můžete to zkusit znovu nebo se obraťte na správce systému a sdělte mu kód chyby 801c0003. "

**Příčina:** **Uživatelé můžou připojovat zařízení k nastavení Azure AD** je nastavená na **žádná**. To zabrání novým uživatelům v připojení svých zařízení k Azure AD. Proto se registrace v Intune nezdařila.

#### <a name="resolution"></a>Rozlišení
1. Přihlaste se k [Azure Portal](https://portal.azure.com/) jako správce.    
2. Přejít na **Azure Active Directory** > **zařízení** > **nastavení zařízení**.    
3. Nastavení **Uživatelé můžou připojovat zařízení ke službě Azure AD** **všem**.    
4. Znovu zaregistrujte zařízení.   

### <a name="the-device-is-already-enrolled"></a>Zařízení je už zaregistrované.

Chyba 8018000a: něco se pokazilo. Zařízení je už zaregistrované.  Můžete se obrátit na správce systému s kódem chyby 8018000a. "

**Příčina:** Platí jedna z následujících podmínek:
- Jiný uživatel už zařízení zaregistroval v Intune nebo se připojil k zařízení do Azure AD. Pokud chcete zjistit, jestli se jedná o tento případ, přejděte na **nastavení** > **účty** > **pracovní přístup**. Vyhledejte zprávu podobnou následující: "jiný uživatel v systému je již připojen k práci nebo škole. Odeberte prosím toto pracovní nebo školní připojení a zkuste to znovu. "    

#### <a name="resolution"></a>Rozlišení

K vyřešení tohoto problému použijte jednu z následujících metod:

##### <a name="remove-the-other-work-or-school-account"></a>Odebrat jiný pracovní nebo školní účet
1. Odhlaste se z Windows a pak se přihlaste pomocí jiného účtu, který je zaregistrovaný nebo připojený k zařízení.    
2. Přejděte na **nastavení** > **účty** > **pracovní přístup**a pak odstraňte pracovní nebo školní účet.
3. Odhlaste se z Windows a pak se přihlaste pomocí svého účtu.    
4. Zaregistrujte zařízení v Intune nebo ho připojte k Azure AD. 



### <a name="this-account-is-not-allowed-on-this-phone"></a>Tento účet není na tomto telefonu povolený.

Chyba: Tento účet není na tomto telefonu povolen. Ujistěte se, že informace, které jste zadali, jsou správné a potom to zkuste znovu nebo si vyžádejte podporu od vaší společnosti. "

**Příčina:** Uživatel, který se pokusil zaregistrovat zařízení, nemá platnou licenci Intune.

#### <a name="resolution"></a>Rozlišení
Přiřaďte uživateli platnou licenci Intune a pak zařízení zaregistrujte.


### <a name="looks-like-the-mdm-terms-of-use-endpoint-is-not-correctly-configured"></a>Vypadá to, že koncový bod podmínek použití MDM není správně nakonfigurovaný.

**Příčina:** Platí jedna z následujících podmínek: 
 - Pro Office 365 a Intune na tenantovi používáte správu mobilních zařízení (MDM) a uživatel, který se pokusí zaregistrovat zařízení, nemá platnou licenci Intune nebo licenci na Office 365.     
- Podmínky a ujednání MDM ve službě Azure AD jsou prázdné nebo neobsahují správnou adresu URL.    

#### <a name="resolution"></a>Rozlišení

Chcete-li tento problém vyřešit, použijte jednu z následujících metod: 
 
##### <a name="assign-a-valid-license-to-the-user"></a>Přiřadit uživateli platnou licenci
Otevřete centrum pro [správu Microsoft 365](https://admin.microsoft.com)a přiřaďte uživateli buď licenci Intune, nebo Office 365.

##### <a name="correct-the-mdm-terms-of-use-url"></a>Opravte adresu URL podmínek použití MDM.
  1. Přihlaste se k [Azure Portal](https://portal.azure.com/)a pak vyberte **Azure Active Directory**.    
  2. Vyberte **mobilita (MDM a mam)** a pak klikněte na **Microsoft Intune**.    
  3. Vyberte **Obnovit výchozí adresy URL MDM**a ověřte, že **Adresa URL podmínek použití MDM** je nastavená na **https://portal.manage.microsoft.com/TermsofUse.aspx** .    
  4. Zvolte **Uložit**.    


### <a name="something-went-wrong"></a>Něco se pokazilo.

Chyba 80180026: něco se pokazilo. Potvrďte, že používáte správné přihlašovací údaje a že vaše organizace tuto funkci používá. Můžete to zkusit znovu nebo se obraťte na správce systému a sdělte mu kód chyby 80180026.

**Příčina:** K této chybě může dojít, když se pokusíte připojit počítač s Windows 10 ke službě Azure AD a platí obě následující podmínky: 
- V Azure je povolený automatický zápis MDM.    
- Počítačového klienta Intune pro počítače (agent Intune pro počítače) je nainstalovaný v počítači s Windows 10.

#### <a name="resolution"></a>Rozlišení
K vyřešení tohoto problému použijte jednu z následujících metod:

##### <a name="disable-mdm-automatic-enrollment-in-azure"></a>Zakáže automatickou registraci MDM v Azure.
1. Přihlaste se k [portálu Azure](https://portal.azure.com/).    
2. Přejít na **Azure Active Directory** > **mobility (MDM a MAM)**  > **Microsoft Intune**.    
3. Nastavte **obor uživatele MDM** na **žádný**a pak klikněte na **Uložit**.    
     
##### <a name="uninstall"></a>Odinstalace
Odinstalujte klientského agenta Intune pro počítače z počítače.    

### <a name="the-software-cannot-be-installed"></a>Software nelze nainstalovat.

Chyba: software nelze nainstalovat, 0x80cf4017.

**Příčina:** Software klienta není aktuální.

#### <a name="resolution"></a>Rozlišení
1. Přihlaste se k [https://admin.manage.microsoft.com](https://admin.manage.microsoft.com).    
2. Přejděte na **správce** > **stažení klientského softwaru**a pak klikněte na **Stáhnout klientský software**.    
3. Uložte instalační balíček a pak nainstalujte klientský software. 


### <a name="the-account-certificate-is-not-valid-and-may-be-expired"></a>Certifikát účtu není platný a pravděpodobně jeho platnost vypršela.

Chyba: "certifikát účtu není platný a pravděpodobně vypršela jeho platnost, 0x80cf4017."

**Příčina:** Software klienta není aktuální.

#### <a name="resolution"></a>Rozlišení
1. Přihlaste se k [https://admin.manage.microsoft.com](https://admin.manage.microsoft.com).    
2. Přejděte na **správce** > **stažení klientského softwaru**a pak klikněte na **Stáhnout klientský software**.    
3. Uložte instalační balíček a pak nainstalujte klientský software.    

### <a name="your-organization-does-not-support-this-version-of-windows"></a>Vaše organizace nepodporuje tuto verzi Windows. 

Chyba: došlo k problému. Vaše organizace nepodporuje tuto verzi Windows.  (0x80180014)"

**Příčina:** Registrace Windows MDM je v tenantovi Intune zakázaná.

#### <a name="resolution"></a>Rozlišení
Pokud chcete tento problém vyřešit v samostatném prostředí Intune, postupujte takto: 
 
1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení** > **omezení registrace** > vyberte omezení typu zařízení.    
2. Vyberte **vlastnosti** > **Upravit** (vedle **Nastavení platformy**) > **Povolení** pro **Windows (MDM)** .    
3. Klikněte na tlačítko **zkontrolovat a uložit**.    

### <a name="a-setup-failure-has-occurred-during-bulk-enrollment"></a>Při hromadné registraci došlo k chybě instalace.

**Příčina:** Uživatelské účty Azure AD v balíčku účtů (Package_GUID) pro příslušný zřizovací balíček neumožňují připojení zařízení ke službě Azure AD. Tyto účty Azure AD se automaticky vytvoří při nastavení zřizovacího balíčku pomocí nástroje Windows Configuration Designer (WCD) nebo nastavení aplikace školních počítačů. tyto účty se pak použijí pro připojení zařízení k Azure AD.

#### <a name="resolution"></a>Rozlišení
1. Přihlaste se k [Azure Portal](https://portal.azure.com/) jako správce.    
2. Přejít na **Azure Active Directory > zařízení > nastavení zařízení**.    
3. Nastavení uživatelé můžou ke **všem** nebo **vybraným** **uživatelům připojovat zařízení do Azure AD** .

   Pokud zvolíte **vybrané** **, klikněte na vybrat a**potom kliknutím na **přidat členy** přidejte všechny uživatele, kteří se můžou ke svým zařízením připojit do Azure AD. Ujistěte se, že jsou přidané všechny účty Azure AD pro zřizovací balíček.
 
Další informace o tom, jak vytvořit zřizovací balíček pro Windows Configuration Designer, najdete v tématu [Vytvoření zřizovacího balíčku pro Windows 10](https://docs.microsoft.com/windows/configuration/provisioning-packages/provisioning-create-package).

Další informace o tom, jak nainstalovat aplikaci školních počítačů, najdete v tématu [použití aplikace s nastavením školních počítačů](https://docs.microsoft.com/education/windows/use-set-up-school-pcs-app).


### <a name="auto-mdm-enroll-failed"></a>Automatický zápis MDM: selhání 

Při automatickém pokusu o registraci zařízení s Windows 10 pomocí Zásady skupiny dojde k následujícím problémům: 
- V Plánovač úloh v části **Microsoft** > **Windows** > **EnterpriseMgmt**, poslední výsledek spuštění **plánu vytvořeného klientem registrace pro automatické registraci v MDM z úlohy AAD** je následující: **událost 76 automatické registrace MDM: nezdařilo se (Neznámý kód chyby Win32:0x8018002b)**       
- V Prohlížeč událostí se v **protokolech aplikací a služeb zaprotokolují následující události/Microsoft/Windows/DeviceManagement-Enterprise-Diagnostics-Provider/admin**:   
    ```asciidoc
    Log Name: Microsoft-Windows-DeviceManagement-Enterprise-Diagnostics-Provider/Admin
    Source: DeviceManagement-Enterprise-Diagnostics-Provider
    Event ID: 76
    Level: Error
    Description: Auto MDM Enroll: Failed (Unknown Win32 Error code: 0x80180002b)
    ```
**Příčina:** Platí jedna z následujících podmínek: 
- Hlavní název uživatele obsahuje neověřenou nebo Nesměrovatelné domény, jako je například. Local (například joe@contoso.local).    
- **Obor uživatele MDM** je nastavený na **None (žádné**). 

#### <a name="resolution"></a>Rozlišení
Pokud hlavní název uživatele obsahuje neověřenou nebo Nesměrovatelné domény, použijte následující postup: 

1. Na serveru, na kterém Active Directory Domain Services (služba AD DS) běží na, otevřete modul **Uživatelé a počítače služby Active Directory** zadáním **DSA. msc** v dialogovém okně **Spustit** a pak klikněte na **OK**.    
2. Klikněte na **Uživatelé** ve vaší doméně a pak postupujte takto:  
    - Pokud existuje jenom jeden ovlivněný uživatel, klikněte na něj pravým tlačítkem a pak klikněte na **vlastnosti**. Na kartě **účet** v rozevíracím seznamu PŘÍPONa UPN v části **přihlašovací jméno uživatele**vyberte platnou příponu UPN, třeba contoso.com, a pak klikněte na **OK**.    
    - Pokud existuje více ovlivněných uživatelů, vyberte uživatele v nabídce **Akce** klikněte na možnost **vlastnosti**. Na kartě **účet** zaškrtněte políčko **přípona UPN** , v rozevíracím seznamu vyberte platnou příponu upn, jako je contoso.com, a pak klikněte na **OK**.
3. Počkejte na další synchronizaci nebo vynuťte rozdílovou synchronizaci z synchronizačního serveru spuštěním následujících příkazů v příkazovém řádku PowerShellu se zvýšenými oprávněními:
    ```powershell
    Import-Module ADSync
    Start-ADSyncSyncCycle -PolicyType Delta
    ```

Pokud je **obor uživatele MDM** nastavený na **None (žádné**), postupujte takto: 
 
1. Přihlaste se k [Azure Portal](https://portal.azure.com/)a pak vyberte **Azure Active Directory**.
2. Vyberte **mobilita (MDM a mam)** a pak vyberte **Microsoft Intune**.    
3. Nastavte **obor uživatele MDM** na **vše**. Nebo nastavte **obor uživatele MDM** na **nějaké**a vyberte skupiny, které můžou automaticky registrovat svoje zařízení s Windows 10.    
4. Nastavte **obor uživatele mam** na **žádný**.


### <a name="an-error-occurred-while-creating-autopilot-profile"></a>Při vytváření profilu autopilotu došlo k chybě.

**Příčina:** Zadaný formát pojmenování v šabloně názvu zařízení nesplňuje požadavky. Například použijete malé písmeno pro sériové makro, jako je například% sériové% místo% SÉRIOVÉho%.

#### <a name="resolution"></a>Rozlišení

Ujistěte se, že formát názvů splňuje následující požadavky:

- Vytvořte jedinečný název pro vaše zařízení. Název musí mít maximálně 15 znaků a může obsahovat písmena (a-z, A – Z), číslice (0-9) a spojovníky (k).
- Nemohou být ale tvořené jen číslicemi.
- Názvy nesmí obsahovat prázdné znaky.
- K přidání sériového čísla specifického pro hardware použijte makro% SERIAL%. Nebo použijte makro% RAND: < # číslice >% pro přidání náhodného řetězce čísel, řetězec obsahuje < # číslice > číslic. Například MYPC-% RAND: 6% generuje název, jako je například MYPC-123456.

### <a name="something-went-wrong-oobeidps"></a>Něco se pokazilo. OOBEIDPS.

**Příčina:** K tomuto problému dochází, pokud máte proxy, bránu firewall nebo jiné síťové zařízení blokující přístup k poskytovateli identity (IdP).

#### <a name="resolution"></a>Rozlišení
Ujistěte se, že požadovaný přístup k internetovým službám pro autopilota není blokovaný. Další informace najdete v tématu [požadavky na síť Windows autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements-network).


### <a name="registering-your-device-for-mobile-management-failed3-0x801c03ea"></a>Registrace zařízení pro správu mobilních zařízení (Chyba: 3, 0x801C03EA).

**Příčina:** Zařízení má čip TPM, který podporuje verzi 2,0, ale ještě nebyla upgradována na verzi 2,0.

#### <a name="resolution"></a>Rozlišení
Upgradujte čip TPM na verzi 2,0.

Pokud se problém opakuje, ověřte, jestli je stejné zařízení ve dvou přiřazených skupinách, přičemž každé skupině se přiřadí jiný profil pro autopilot. Pokud se nachází ve dvou skupinách, určete, který profil pro autopilot by se měl na zařízení použít, a pak odeberte přiřazení druhého profilu.

Další informace o tom, jak nasadit zařízení s Windows v celoobrazovkovém režimu pomocí funkce autopilot, najdete v tématu [nasazení veřejného terminálu pomocí funkce Windows autopilot](https://blogs.technet.microsoft.com/mniehaus/2018/06/07/deploying-a-kiosk-using-windows-autopilot/).


### <a name="securing-your-hardware-failed-0x800705b4"></a>Zabezpečení hardwaru (Chyba: 0x800705b4).

Chyba 800705b4: 
```
Securing your hardware (Failed: 0x800705b4)
Joining your organization's network (Previous step failed)
Registering your device for mobile management (Previous step failed)
```

**Příčina:** Cílové zařízení s Windows nesplňuje některé z následujících požadavků:

- Zařízení musí mít fyzický čip TPM 2,0. Zařízení s Virtual čipy TPM (například virtuální počítače Hyper-V) nebo čipy TPM 1,2 nefungují s režimem automatického nasazení.
- V zařízení musí běžet jedna z následujících verzí Windows:
    - Windows 10 Build 1703 nebo novější verze.
    - Pokud se používá hybridní připojení k Azure AD, Windows 10 Build 1809 nebo novější verze.


#### <a name="resolution"></a>Rozlišení
Ujistěte se, že cílové zařízení splňuje obě požadavky popsané v části **Příčina** .

Další informace o tom, jak nasadit zařízení s Windows v celoobrazovkovém režimu pomocí funkce autopilot, najdete v tématu [nasazení veřejného terminálu pomocí funkce Windows autopilot](https://blogs.technet.microsoft.com/mniehaus/2018/06/07/deploying-a-kiosk-using-windows-autopilot/).


### <a name="something-went-wrong-error-code-80070774"></a>Něco se pokazilo. Kód chyby 80070774.

Chyba 0x80070774: došlo k nějaké chybě. Potvrďte, že používáte správné přihlašovací údaje a že vaše organizace tuto funkci používá. Můžete to zkusit znovu nebo se obraťte na správce systému a sdělte mu kód chyby 80070774.

K tomuto problému obvykle dochází předtím, než se zařízení restartuje v hybridním scénáři autopilotu služby Azure AD, když vyprší časový limit zařízení během úvodní obrazovky pro přihlášení. Znamená to, že řadič domény se nedá najít nebo se k němu úspěšně nedostal kvůli problémům s připojením. Nebo že zařízení zadalo stav, který se nemůže připojit k doméně.

**Příčina:** Nejběžnější příčinou je, že se používá připojení k hybridní službě Azure AD a v profilu autopilotu je nakonfigurovaná funkce přiřadit uživatele. Při použití funkce přiřadit uživatele se v zařízení během úvodní obrazovky pro přihlášení provede připojení Azure AD, které zařízení umístí do stavu, ve kterém se nemůže připojit k místní doméně. Funkce přiřadit uživatele by proto měla být použita pouze ve standardních scénářích pro automatické pilotní připojení služby Azure AD.  Tato funkce by se neměla používat ve scénářích připojení k hybridní službě Azure AD.

Další možnou příčinou této chyby je, že zařízení AzureAD přidružené k objektu autopilotu bylo odstraněno. Chcete-li tento problém vyřešit, odstraňte objekt autopilot a znovu importujte hodnotu hash, čímž vygenerujete novou.

#### <a name="resolution"></a>Rozlišení

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte > **zařízení** > **Windows** > **Windows**.
2. Vyberte zařízení, u kterého dochází k problému > klikněte na tlačítko se třemi tečkami (...) na pravé straně.
3. Vyberte zrušit **přiřazení uživatele** a počkejte na dokončení procesu.
4. Před opakovaným pokusem o spuštění instalace ověřte, že je profil Azure AD autopilotu pro hybridní nasazení přiřazen.

#### <a name="second-resolution"></a>Druhé řešení
Pokud se problém opakuje, na serveru, který je hostitelem offline služby Intune, přejděte na server, na kterém je zaprotokolována událost s ID 30312 v protokolu služby konektoru ODJ. Událost 30312 vypadá takto:

```
Log Name:      ODJ Connector Service
Source:        ODJ Connector Service Source
Event ID:      30132
Level:         Error
Description:
{
          "Metric":{
                   "Dimensions":{
                             "RequestId":"<RequestId>",
                             "DeviceId":"<DeviceId>",
                             "DomainName":"contoso.com",
                             "ErrorCode":"5",
                             "RetryCount":"1",
                              "ErrorDescription":"Failed to get the ODJ Blob. The ODJ connector does not have sufficient privileges to complete the operation",
                              "InstanceId":"<InstanceId>",
                              "DiagnosticCode":"0x00000800",
                              "DiagnosticText":"Failed to get the ODJ Blob. The ODJ connector does not have sufficient privileges to complete the operation [Exception Message: \"DiagnosticException: 0x00000800. Failed to get the ODJ Blob. The ODJ connector does not have sufficient privileges to complete the operation\"] [Exception Message: \"Failed to call NetProvisionComputerAccount machineName=<ComputerName>\"]"
                   },
                   "Name":"RequestOfflineDomainJoinBlob_Failure",
                   "Value":0
          }
}
```

K tomuto problému obvykle dochází, když nesprávně delegujete oprávnění k organizační jednotce, kde se vytváří zařízení Windows autopilotu. Další informace najdete v tématu [zvýšení limitu účtu počítače v organizační jednotce](windows-autopilot-hybrid.md#increase-the-computer-account-limit-in-the-organizational-unit).

1. Otevřete položku **Uživatelé a počítače služby Active Directory (DSA. msc)** .
2. Klikněte pravým tlačítkem na organizační jednotku, kterou použijete k vytvoření hybridních počítačů připojených k Azure AD > **delegování ovládacího prvku**.
3. V průvodci **delegováním řízení** vyberte **další** > **Přidat** > **typy objektů**.
4. V podokně **typy objektů** zaškrtněte políčko **počítače** > **OK**.
5. V podokně **Vybrat uživatele**, **počítače**nebo **skupiny** v poli **Zadejte názvy objektů k výběru** zadejte název počítače, ve kterém je konektor nainstalovaný.
6. Vyberte možnost **Kontrola názvů** a ověřte zadání > **OK** > **Další**.
7. Vyberte **vytvořit vlastní úlohu pro delegování** > **Další**.
8. Zaškrtněte políčko **pouze následující objekty ve složce** a potom vyberte **objekty počítače**, **vytvořte vybrané objekty v této složce**a zrušte zaškrtnutí políček **Odstranit vybrané objekty v této** složce.
9. Vyberte **Další**.
10. V části **oprávnění**zaškrtněte políčko **Úplné řízení** . Tato akce vybere všechny ostatní možnosti.
11. Vyberte **další** > **Dokončit**.

### <a name="the-enrollment-status-page-times-out-before-the-sign-in-screen"></a>Časový limit stránky stavu registrace vypršel před přihlašovací obrazovkou.

**Příčina:** K tomuto problému může dojít, pokud jsou splněné všechny následující podmínky:
- Ke sledování Microsoft Store pro obchodní aplikace používáte stránku stavu registrace.
- Máte zásady podmíněného přístupu Azure AD, které používají nastavení vyžadovat, aby zařízení bylo označené jako vyhovující.
- Zásady se vztahují na všechny cloudové aplikace a Windows.

#### <a name="resolution"></a>Řešení::
Zkuste jednu z těchto možností:
- Zaměřte zásady dodržování předpisů Intune na zařízení. Ujistěte se, že je možné určit dodržování předpisů před přihlášením uživatele.
- Používejte offline licencování pro aplikace ze Storu. V takovém případě nemusí klient Windows před určením dodržování předpisů pro zařízení kontrolovat Microsoft Store.

## <a name="next-steps"></a>Další kroky

- [Řešení potíží s registrací zařízení v Intune](troubleshoot-device-enrollment-in-intune.md)
- [Zeptejte se fóra služby Intune](https://social.technet.microsoft.com/Forums/%7Blang-locale%7D/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc)
- [Podívejte se na blog týmu podpory Microsoft Intune.](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess)
- [Podívejte se na blog Microsoft Enterprise mobility and Security.](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Announcing-the-public-preview-of-Azure-AD-group-based-license/ba-p/245210)
- [Získat podporu pro Microsoft Intune](../fundamentals/get-support.md)
- [Najít chyby při registraci spolusprávy](https://docs.microsoft.com/configmgr/comanage/how-to-monitor#enrollment-errors)
