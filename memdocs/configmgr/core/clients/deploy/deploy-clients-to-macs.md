---
title: Nasazení klientů se systémem Mac
titleSuffix: Configuration Manager
description: Naučte se, jak nasadit klienty do počítačů Mac v Configuration Manager.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8993f4c05b7156f3aecf6fcc9c8ea3790e49e98d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81713440"
---
# <a name="how-to-deploy-clients-to-macs"></a>Postup nasazení klientů na počítače Mac

*Platí pro: Configuration Manager (Current Branch)*

Tento článek popisuje, jak nasadit a udržovat klienta Configuration Manager v počítačích Mac. Informace o tom, co je třeba nakonfigurovat před nasazením klientů do počítačů Mac, najdete v tématu [Příprava nasazení klientského softwaru na](prepare-to-deploy-mac-clients.md)počítač Mac.

Když instalujete nového klienta pro počítače se systémem Mac, bude pravděpodobně nutné nainstalovat Configuration Manager aktualizace, aby odrážely nové informace o klientovi v konzole Configuration Manager.

V těchto postupech máte dvě možnosti instalace klientských certifikátů. Přečtěte si další informace o klientských certifikátech pro počítače Mac v tématu [Příprava na nasazení klientského softwaru na počítače Mac](prepare-to-deploy-mac-clients.md#certificate-requirements).  

- Použijte Configuration Manager registraci pomocí [nástroje CMEnroll](#bkmk_enroll). Proces registrace nepodporuje automatické obnovení certifikátu. Před vypršením platnosti nainstalovaného certifikátu znovu zaregistrujte počítač Mac.    

- [Použijte žádost o certifikát a metodu instalace, která je nezávislá na Configuration Manager](#bkmk_external).  

> [!IMPORTANT]  
> Chcete-li nasadit klienta nástroje do zařízení se systémem macOS Sierra, správně nakonfigurujte **název subjektu** certifikátu bodu správy. Použijte například plně kvalifikovaný název domény serveru bodu správy.



## <a name="configure-client-settings"></a>Konfigurace nastavení klientů  

Pro konfiguraci registrace pro počítače Mac použijte [výchozí nastavení klienta](about-client-settings.md) . Nemůžete použít vlastní nastavení klienta. Pro vyžádání a instalaci certifikátu vyžaduje klient Configuration Manager pro Mac výchozí nastavení klienta.  

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Vyberte uzel **nastavení klienta** a pak vyberte **výchozí nastavení klienta**.  

2. Na kartě **Domů** na pásu karet ve skupině **vlastnosti** klikněte na možnost **vlastnosti**.  

3. Vyberte část **registrace** a pak nakonfigurujte následující nastavení:  

    1. **Dovolit uživatelům zapsat mobilní zařízení a počítače Mac**: **Ano**  

    2. **Registrační profil:** Vyberte **nastavit profil**.  

4. V dialogovém okně **profil zápisu mobilního zařízení** klikněte na **vytvořit**.  

5. V dialogovém okně **vytvořit profil zápisu** zadejte název pro tento registrační profil. Pak nakonfigurujte **kód lokality pro správu**. Vyberte Configuration Manager primární lokalitu, která obsahuje body správy pro tyto počítače Mac.  

    > [!NOTE]  
    >  Pokud nemůžete vybrat lokalitu, ujistěte se, že v lokalitě nakonfigurujete alespoň jeden bod správy pro podporu mobilních zařízení.  

6. Klikněte na tlačítko **Přidat**.  

7. V okně **Přidat certifikační autoritu pro mobilní zařízení** vyberte server certifikační autority, který vydává certifikáty počítačům Mac.  

8. V dialogovém okně **vytvořit profil zápisu** vyberte šablonu certifikátu počítače Mac, kterou jste předtím vytvořili.  

9. Kliknutím na **tlačítko OK** zavřete dialogové okno **profil zápisu** a pak na výchozí dialogové okno **nastavení klienta** .  

    > [!TIP]  
    > Pokud chcete změnit interval zásad klienta, použijte **interval dotazování zásad klienta** ve skupině nastavení klienta **zásady klienta** .  

Až zařízení nastahují zásady klienta, Configuration Manager použijí tato nastavení pro všechny uživatele. Pokud chcete iniciovat načtení zásad pro jednoho klienta, přečtěte si téma [spuštění načtení zásad pro klienta Configuration Manager](../manage/manage-clients.md#BKMK_PolicyRetrieval).  

Kromě nastavení klienta registrace se ujistěte, že jste nakonfigurovali následující nastavení klientského zařízení:  

- **Inventář hardwaru**: tuto funkci povolte a nakonfigurujte, pokud chcete shromáždit inventář hardwaru z klientských počítačů se systémem Mac a Windows. Další informace najdete v tématu [postup rozšiřování inventáře hardwaru](../manage/inventory/extend-hardware-inventory.md).  

- **Nastavení dodržování předpisů**: tuto funkci povolte a nakonfigurujte, pokud chcete vyhodnotit a opravovat nastavení na klientských počítačích se systémem Mac a Windows. Další informace najdete v tématu [plánování a konfigurace nastavení dodržování předpisů](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

Další informace najdete v tématu [Konfigurace nastavení klienta](configure-client-settings.md).  



## <a name="download-the-client-for-macos"></a><a name="bkmk_download"></a>Stažení klienta pro macOS

1. Stáhněte si balíček klientského souboru macOS, [klienta Microsoft Endpoint Configuration Manager-MacOS (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850). Uložte **ConfigmgrMacClient. msi** do počítače, na kterém běží systém Windows. Tento soubor není na instalačním médiu Configuration Manager.  

2. Spusťte instalační program na počítači se systémem Windows. Extrahujte balíček klienta pro systém Mac, **Macclient. dmg**, do složky na místním disku. Výchozí cesta je `C:\Program Files\Microsoft\System Center Configuration Manager for Mac client`.  

3. Zkopírujte soubor **Macclient. dmg** do složky v počítači Mac.  

4. Na počítači Mac spusťte **Macclient. dmg** a extrahujte soubory do složky na místním disku.  

5. Ve složce se ujistěte, že obsahuje následující soubory: 

    - **CCMSetup**: nainstaluje klienta Configuration Manager do počítačů Mac pomocí **CMClient. pkg.**  

    - **CMDiagnostics**: shromažďuje diagnostické informace týkající se Configuration Manager klienta na počítačích Mac.  

    - **CMUninstall**: odinstaluje klienta z počítačů Mac.  

    - **CMAppUtil**: převede balíčky aplikací Apple do formátu, který můžete nasadit jako aplikaci Configuration Manager.  

    - **CMEnroll**: vyžádá a nainstaluje klientský certifikát pro počítač Mac, abyste mohli nainstalovat klienta Configuration Manager.  



## <a name="enroll-the-mac-client"></a><a name="bkmk_enroll"></a>Registrace klienta se systémem Mac  

Zaregistrujte jednotlivé klienty pomocí [Průvodce zápisem počítače Mac](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

K automatizaci registrace pro mnoho klientů použijte [Nástroj CMEnroll](#client-and-certificate-automation-with-cmenroll).   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Registrace klienta pomocí Průvodce registrací počítače Mac  

1. Po instalaci klienta se otevře Průvodce registrací počítače. Chcete-li průvodce spustit ručně, vyberte možnost **Registrovat** na stránce předvoleb **Configuration Manager** .  

2. Na druhé stránce průvodce zadejte následující informace:  

   - **Uživatelské jméno**: uživatelské jméno může být v následujících formátech:  

     - `domain\name`. Příklad: `contoso\mnorth`  

     - `user@domain`. Příklad: `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  Když použijete e-mailovou adresu k vyplnění pole **uživatelské jméno** , Configuration Manager automaticky vyplní pole **název serveru** . Používá výchozí název serveru zprostředkujícího bodu registrace a název domény e-mailové adresy. Pokud se tyto názvy neshodují s názvem serveru zprostředkujícího bodu registrace, opravte **název serveru** během registrace.  

       Uživatelské jméno a odpovídající heslo se musí shodovat s uživatelským účtem služby Active Directory, který má oprávnění **ke čtení** a **zápisu** v šabloně certifikátu klienta se systémem Mac.  

   - **Název serveru**: název serveru zprostředkujícího bodu registrace.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automatizace klientů a certifikátů pomocí CMEnroll  

Tento postup použijte pro automatizaci instalace klienta a vyžádání a registraci klientských certifikátů nástrojem CMEnroll. Chcete-li spustit nástroj, musíte mít uživatelský účet služby Active Directory.

1. V počítači Mac přejděte do složky, do které jste extrahovali obsah souboru **Macclient. dmg** .  

2. Zadejte následující příkaz:`sudo ./ccmsetup`  

3. Počkejte, dokud neuvidíte zprávu **Instalace dokončena** . I když instalační program zobrazí zprávu, že je nutné restartovat nyní, nerestartovat a pokračovat k dalšímu kroku.  

4. Ve složce **Tools** v počítači Mac zadejte následující příkaz:`sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    Po instalaci klienta se otevře průvodce registrací počítače Mac, který vám pomůže počítač Mac zaregistrovat. Další informace najdete v tématu [registrace klienta pomocí Průvodce zápisem počítače Mac](#bkmk_enroll).  

     Příklad: Pokud má zprostředkující bod registrace serveru název **Server02.contoso.com**a udělujete **contoso\mnorth** oprávnění pro šablonu certifikátu klienta se systémem Mac, zadejte následující příkaz:`sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > Pokud uživatelské jméno obsahuje některý z následujících znaků, registrace se nezdařila `<>"+=,`:. Použijte certifikát mimo IP síť s uživatelským jménem, které tyto znaky nezahrnuje.  
    >  
    > Pro lepší činnost koncového uživatele skriptujte kroky instalace. Uživatelé pak musí zadávat své uživatelské jméno a heslo.  

5. Zadejte heslo pro uživatelský účet služby Active Directory. Při zadání tohoto příkazu se zobrazí výzva k zadání dvou hesel. První heslo je pro účet super uživatele pro spuštění příkazu. Druhá výzva je určena pro uživatelský účet služby Active Directory. Výzvy vypadají stejně, takže nezapomeňte ověřit, jestli je zadáváte ve správném pořadí.  

6. Počkejte, dokud neuvidíte zprávu **Úspěšně zaregistrováno** .  

7. Pokud chcete omezit zaregistrovaný certifikát na Configuration Manager, otevřete na počítači Mac okno terminálu a proveďte následující změny:  

    1. Zadejte příkaz.`sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`  

    2. V okně pro **přístup k řetězci klíčů** v části **řetězy** klíčů vyberte možnost **systém**. Pak v části **Category (kategorie** ) zvolte **klíče**.  

    3. Rozbalte klíče a zobrazte certifikáty klientů. Vyhledejte certifikát s privátním klíčem, který jste nainstalovali, a otevřete klíč.  

    4. Na kartě **Access Control** pro **Povolení přístupu vyberte potvrdit**.  

    5. Přejděte na **/Library/Application Support Support/Microsoft/ccm**, vyberte **ccmclient**a pak zvolte **Přidat**.  

    6. Vyberte **Uložit změny** a zavřete dialogové okno **přístup do řetězce klíčů** .  

8. Restartujte počítač Mac.  

Chcete-li ověřit, zda je instalace klienta úspěšná, otevřete **Configuration Manager** položku v části **Předvolby systému** v počítači Mac. V konzole Configuration Manager taky aktualizovat a zobrazit kolekci **všechny systémy** . Potvrďte, že se počítač Mac zobrazuje v této kolekci jako spravovaný klient.  

> [!TIP]  
> Chcete-li pomoct s řešením klienta se systémem Mac, použijte nástroj **CMDiagnostics** , který je součástí balíčku klienta pro systém Mac. Použijte ho ke shromáždění následujících diagnostických informací:  
>   
> - Seznam spuštěných procesů  
> - Verze operačního systému Mac OS X  
> - Zprávy o chybách Mac OS X týkající se Configuration Manager klienta včetně **ccm\*. crash** a **System preference. crash**.  
> - Soubor kusovníku (BOM) a seznam vlastností (. plist) vytvořený instalací klienta Configuration Manager.  
> - Obsah složky **/Library/Application Support Support/Microsoft/ccm/logs**.  
>   
> Informace shromažďované nástrojem CmDiagnostics jsou přidány do souboru zip, který je uložen na plochu počítače a má název`cmdiag-<hostname>-<datetime>.zip`



## <a name="manage-certificates-external-to-configuration-manager"></a><a name="bkmk_external"></a>Správa certifikátů mimo Configuration Manager

Můžete použít žádost o certifikát a metodu instalace nezávisle na Configuration Manager. Použijte stejný obecný proces, ale zahrňte následující další kroky: 

- Při instalaci klienta Configuration Manager použijte možnosti příkazového řádku **MP** a **Subject** . Zadejte následující příkaz: `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`. Název subjektu certifikátu rozlišuje velká a malá písmena, proto ho zadejte přesně tak, jak se zobrazuje v podrobnostech certifikátu.  

     Příklad: internetový plně kvalifikovaný název domény bodu správy je **Server03.contoso.com**. Certifikát klienta pro počítač Mac má jako běžný název v předmětu certifikátu plně kvalifikovaný název domény ( **mac12.contoso.com** ). Použijte následující příkaz:`sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- Pokud máte více než jeden certifikát, který obsahuje stejnou hodnotu předmětu, zadejte sériové číslo certifikátu, které se má použít pro klienta Configuration Manager. Použijte následující příkaz: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`  

     Příklad: `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Obnovení certifikátu klienta pro počítač Mac  

Tento postup odebere SMSID. Configuration Manager klient pro Mac vyžaduje nové ID pro použití nového nebo obnoveného certifikátu.  

> [!IMPORTANT]  
> Po nahrazení SMSID klienta při odstranění starého prostředku v konzole Configuration Manager odstraníte také veškerou uloženou historii klienta. Například historii inventáře hardwaru pro daného klienta.  


1. Vytvořte a naplňte kolekci zařízení pro počítače Mac, které musí obnovit certifikáty počítače.  

2. V pracovním prostoru **Prostředky a kompatibilita** spusťte **Průvodce vytvořením položky konfigurace**.  

3. Na stránce **Obecné** v průvodci zadejte následující informace:  

    - **Název**: **Odeberte SMSID pro Mac** .  

    - **Zadejte**: **Mac OS X**  

4. Na stránce **podporované platformy** vyberte všechny verze Mac OS X.  

5. Na stránce **Nastavení** vyberte **Nové**. V okně **vytvořit nastavení** zadejte následující informace:  

    - **Název**: **Odeberte SMSID pro Mac** .  

    - **Typ nastavení**: **skript**  

    - **Datový typ**: **řetězec**  

6. V okně **vytvořit nastavení** pro **skript zjišťování**vyberte **Přidat skript**. Tato akce určuje skript pro zjišťování počítačů se systémem Mac nakonfigurovaných pomocí SMSID.  

7. V okně **Úpravy skriptu zjišťování** zadejte následující skript prostředí:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. Kliknutím na **tlačítko OK** zavřete okno **Úpravy skriptu zjišťování** .  

9. V okně **vytvořit nastavení** pro skript napravení **(volitelné)** vyberte **Přidat skript**. Tato akce určuje skript, který odebere SMSID, když se najde na počítačích Mac.  

10. V okně **vytvořit skript** napravení zadejte následující skript prostředí:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Kliknutím na **tlačítko OK** zavřete okno **vytvořit skript nápravy** .  

12. Na stránce **pravidla dodržování předpisů** vyberte možnost **nové**. Pak v okně **vytvořit pravidlo** zadejte následující informace:  

    - **Název**: **Odeberte SMSID pro Mac** .  

    - **Vybrané nastavení**: zvolte **Procházet** a potom vyberte skript zjišťování, který jste předtím zadali.  

    - V **následujících** polích: hodnota " **doména/výchozí dvojice" (com. Microsoft. ccmclient, SMSID) neexistuje**.  

    - Povolte možnost **spustit zadaný skript pro nápravu, když toto nastavení nedodržuje předpisy**.  

13. Dokončete průvodce.  

14. Vytvořte standardní hodnoty konfigurace, které obsahují tuto položku konfigurace. Nasaďte směrný plán do cílové kolekce.  

     Další informace najdete v tématu [Vytvoření standardních hodnot konfigurace](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Po instalaci nového certifikátu na počítače Mac s odebraným SMSID spusťte následující příkaz, který nakonfiguruje klienta na použití nového certifikátu:  

    ``` Shell
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>Viz také

[Příprava na nasazení klientů na počítače Mac](prepare-to-deploy-mac-clients.md)

[Údržba klientů Mac](../manage/maintain-mac-clients.md)
