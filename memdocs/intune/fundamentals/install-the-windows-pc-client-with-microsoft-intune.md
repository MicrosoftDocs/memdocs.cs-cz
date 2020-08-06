---
title: Instalace klientského softwaru na počítači
description: Tento průvodce vám pomůže se správou počítače s Windows klientským softwarem Microsoft Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
ms.date: 07/13/2017
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 99dcf916-d80f-42c5-863b-a4595e1ec67a
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: d9e6806e8d755163d5ae1701ca49ad2daeff464f
ms.sourcegitcommit: 2ee50bfc416182362ae0b8070b096e1cc792bf68
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865869"
---
# <a name="install-the-intune-software-client-on-windows-pcs"></a>Instalace klientského softwaru Intune na počítače se systémem Windows

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

> [!NOTE]
> V Microsoft Intune můžete spravovat počítače s Windows buď [jako mobilní zařízení prostřednictvím správy mobilních zařízení (MDM)](../enrollment/windows-enroll.md), nebo jako počítače se softwarovým klientem Intune, jak je popsáno níže. Microsoft však zákazníkům doporučuje, aby pokud možno [používali řešení pro správu MDM](../enrollment/windows-enroll.md). Další informace najdete v tématu [porovnání správy počítačů s Windows jako počítačů nebo mobilních zařízení](pc-management-comparison.md) . 


Počítače se systémem Windows se dají zaregistrovat přes klientský software Intune. Klientský software Intune je možné nainstalovat následujícími způsoby:

- Může ho nainstalovat správce IT pomocí jednoho z následujících způsobů: ruční instalace, zásady skupiny nebo instalace zahrnutá v bitové kopii disku.

- Můžou ho nainstalovat koncoví uživatelé, kteří ručně nainstalují klientský software.

Klientský software Intune obsahuje minimální software nutný k registraci počítače v systému správy Intune. Po registraci počítače klientský software Intune stáhne kompletní klientský software potřebný ke správě počítače.

Toto postupné stahování snižuje vliv na šířku pásma sítě a zkracuje čas potřebný k počáteční registraci počítače v Intune na minimum. Zajistí také to, že po dokončení druhého stahování bude mít klient k dispozici nejnovější dostupný software.

Jedna licence služby Intune umožňuje instalovat klientský software Intune až na pět počítačů.

## <a name="download-the-intune-client-software"></a>Stažení klientského softwaru Intune

Všechny způsoby (s výjimkou toho, kdy si uživatelé instalují klientský software Intune sami) vyžadují, aby správci IT tento software napřed stáhli, než je možné ho nasadit koncovým uživatelům.

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/)klikněte na **správce** &gt; **stažení klientského softwaru**.

   ![Stažení počítačového klienta Intune](./media/install-the-windows-pc-client-with-microsoft-intune/pc-sa-client-download.png)

2. Na stránce **Stažení klientského softwaru** klikněte na **Stáhnout klientský software**. Uložte balíček **Microsoft_Intune_Setup.zip**, který obsahuje software, do zabezpečeného umístění v síti.

   Instalační balíček klientského softwaru Intune obsahuje jedinečné a specifické informace o vašem účtu, které jsou dostupné prostřednictvím vloženého certifikátu. Pokud k instalačnímu balíčku získají přístup neoprávnění uživatelé, můžou zaregistrovat počítače k účtu, který je reprezentovaný vloženým certifikátem, a můžou tak získat přístup k podnikovým prostředkům.

3. Extrahujte obsah instalačního balíčku do zabezpečeného umístění v síti.

    > [!IMPORTANT]
    > Neodstraňujte ani neodstraňujte extrahovaný soubor **accountcert** nebo instalace klientského softwaru se nezdaří.

## <a name="deploy-the-client-software-manually"></a>Ruční nasazení klientského softwaru

Na počítačích, kam se bude klientský software instalovat, přejděte do složky, kde jsou uložené instalační soubory klientského softwaru. Spusťte **Microsoft_Intune_Setup.exe** a klientský software tak nainstalujte.

> [!NOTE]
> Když přesunete ukazatel myši na ikonu v oznamovací oblasti v klientském počítači, zobrazí se stav instalace.

## <a name="deploy-the-client-software-by-using-group-policy"></a>Nasazení klientského softwaru pomocí zásad skupiny

1. Ve složce, která obsahuje soubory **Microsoft_Intune_Setup.exe** a **MicrosoftIntune.accountcert**, spusťte následující příkaz k extrakci instalačních programů založených na Instalační službě systému Windows pro 32bitové a 64bitové počítače:

    ```cmd
    Microsoft_Intune_Setup.exe/Extract <destination folder>
    ```

2. Zkopírujte soubory **Microsoft_Intune_x86.msi**, **Microsoft_Intune_x64.msi** a **MicrosoftIntune.accountcert** do umístění v síti, ke kterému mají přístup všechny počítače, na které se klientský software nainstaluje.

    > [!IMPORTANT]
    > Soubory od sebe neoddělujte ani nepřejmenovávejte, jinak se instalace klientského softwaru nezdaří.

3. Pomocí zásad skupiny nasaďte software do počítačů v síti.

    Další informace o tom, jak automaticky nasadit software pomocí zásad skupiny, najdete v článku [Zásady skupiny pro začátečníky](https://technet.microsoft.com/library/hh147307.aspx).

## <a name="deploy-the-client-software-as-part-of-an-image"></a>Nasazení klientského softwaru jako součásti image
Klientský software Intune můžete do počítače nasadit jako součást image operačního systému. Jako příklad poslouží tento postup:

1. Zkopírujte instalační soubory klienta **Microsoft_Intune_Setup.exe** a **MicrosoftIntune. accountcert**do složky **%systemdrive%\temp\ Microsoft_Intune_Setup** na referenčním počítači.

2. Vytvořte položku registru **WindowsIntuneEnrollPending** přidáním následujícího příkazu do skriptu **SetupComplete.cmd** :

    ```cmd
    %windir%\system32\reg.exe add HKEY_LOCAL_MACHINE\Software\Microsoft\Onlinemanagement\Deployment /v
    WindowsIntuneEnrollPending /t REG_DWORD /d 1
    ```

3. Přidáním následujícího příkazu do skriptu **setupcomplete.cmd** spusťte registrační balíček s argumentem příkazového řádku /PrepareEnroll:

    ```cmd
    %systemdrive%\temp\Microsoft_Intune_Setup\Microsoft_Intune_Setup.exe /PrepareEnroll
    ```

    > [!TIP]
    > Skript **SetupComplete.cmd** umožňuje, aby instalační program systému Windows provedl změny systému před přihlášením uživatele. Argument příkazového řádku **/PrepareEnroll** připraví cílový počítač, aby se po dokončení instalačního programu systému Windows automaticky zaregistroval v Intune.

4. Skript **SetupComplete.cmd** umístěte do složky **%Windir%\Setup\Scripts** na referenčním počítači.

5. Vytvořte bitovou kopii referenčního počítače a pak ji nasaďte do cílových počítačů.

    Když se cílový počítač po dokončení instalačního programu systému Windows restartuje, vytvoří se klíč registru **WindowsIntuneEnrollPending** . Registrační balíček ověří, jestli je počítač zaregistrovaný. Pokud je počítač zaregistrovaný, neprovede se žádná další akce. Pokud není počítač registrovaný, registrační balíček vytvoří úlohu automatické registrace Microsoft Intune.

    Když je úloha automatické registrace spuštěná v příští naplánovanou dobu, zkontroluje existenci hodnoty registru **WindowsIntuneEnrollPending** a pokusí se registrovat cílový počítač v Intune. Pokud se registrace z jakéhokoli důvodu nezdaří, při dalším spuštění úlohy se pokus o registraci opakuje. Opakované pokusy pokračují po dobu jednoho měsíce.

    Úloha automatické registrace Intune, hodnota registru **WindowsIntuneEnrollPending** a certifikát účtu se po úspěšné registraci nebo po jednom měsíci vymažou z cílového počítače (podle toho, která z těchto situací nastane první).

## <a name="instruct-users-to-self-enroll"></a>Pokyny pro uživatele, jak se zaregistrovat sami

Uživatelé nainstalují klientský software Intune tak, že přejdou na [web Portál společnosti](https://portal.manage.microsoft.com). Přesné informace, které uživatelé vidí na webovém portálu, se liší podle autority MDM vašeho účtu a platformy nebo verze operačního systému uživatelských počítačů.

Pokud nemají uživatelé přiřazenou licenci k Intune nebo nebyla na Intune nastavena autorita MDM, nezobrazí se uživatelům žádné možnosti registrace.

Pokud byla uživatelům přiřazena licence k Intune a na Intune byla nastavena autorita MDM organizace:

- Uživatelům počítačů s Windows 7 nebo Windows 8 se zobrazí JENOM možnost registrace do Intune na základě stažení a instalace klientského softwaru pro PC, který je pro svou organizaci jedinečný.

- Uživatelé počítačů s Windows 8.1 a Windows 10 mají dvě možnosti registrace:

  - **Zaregistrovat počítač jako mobilní zařízení**: Poté, co uživatelé zvolí tlačítko **Zjistěte, jak můžete zaregistrovat svoje zařízení s Windows**, přejdou na pokyny týkající se způsobu registrace počítače jako mobilního zařízení. Toto tlačítko se zobrazí v dobře viditelném umístění, protože registrace MDM se považuje za výchozí a preferovanou možnost registrace. Možnost MDM ale neplatí pro toto téma, protože to se týká jenom instalace klientského softwaru.
  - **Zaregistrovat počítač pomocí klientského softwaru Intune**: Bude potřeba říct uživatelům, že mají vybrat odkaz **Kliknutím sem ho můžete stáhnout** a přejít tak k pokynům pro instalaci klientského softwaru.

V následující tabulce najdete souhrnný přehled možností.

  ![Výchozí možnosti registrace pro jednotlivé platformy](./media/install-the-windows-pc-client-with-microsoft-intune/default-enrollment-options-table.png)

Na následujících snímcích obrazovek vidíte, co se zobrazuje uživatelům, kteří registrují svoje zařízení používající klientský software.

Uživatelům se nejdřív zobrazí výzva k identifikaci nebo registraci zařízení.

  ![identifikace nebo registrace zařízení](./media/install-the-windows-pc-client-with-microsoft-intune/identify-device-or-enroll.png)

Pokud chcete, aby si vaši uživatelé nainstalovali na počítač klientský software, je potřeba jim říct, aby použili odkaz **Kliknutím sem ho můžete stáhnout**, který umožňuje uživatelům stáhnout klientský software pro počítač a provede je procesem instalace. Po zvolení tlačítka **Zjistěte, jak můžete zaregistrovat svoje zařízení s Windows** přejdou uživatelé k dokumentaci s informacemi, jak zaregistrovat zařízení pomocí registrace MDM, což se ale netýká těchto pokynů pro klientský software.

  ![klikněte na odkaz Kliknutím sem ho můžete stáhnout](./media/install-the-windows-pc-client-with-microsoft-intune/enroll-your-windows-device.png)

Když uživatelé kliknou na odkaz, zobrazí se tlačítko **Stáhnout software**, po jehož výběru se spustí instalace klientského softwaru pro počítač.

  ![zvolte tlačítko Stáhnout software](./media/install-the-windows-pc-client-with-microsoft-intune/download-pc-client-software.png)

Uživatelé jsou pak požádáni, aby se přihlásili s použitím firemních přihlašovacích údajů.

  ![Přihlaste se pomocí svých přihlašovacích údajů.](./media/install-the-windows-pc-client-with-microsoft-intune/sign-in-to-intune.png)

Uživatelé přejdou na úvodní stránku instalace.

  ![Úvodní stránka instalace klienta na počítač](./media/install-the-windows-pc-client-with-microsoft-intune/welcome-to-pc-agent-install-wizard.png)

Uživatelé zvolí možnost **Další** a spustí se instalace.

  ![Úvodní stránka instalace klienta na počítač](./media/install-the-windows-pc-client-with-microsoft-intune/welcome-to-pc-agent-install-wizard.png)

Po dokončení instalace, zvolí uživatelé možnost **Dokončit**.

  ![Dokončení instalace klienta na počítač](./media/install-the-windows-pc-client-with-microsoft-intune/completed-the-setup-wizard.png)

Pokud se uživatelé po registraci za použití klientského softwaru Intune pro počítač pokusí svůj počítač zaregistrovat jako mobilní zařízení, zobrazí se jim následující chybová obrazovka.

  ![Obrazovka, která se zobrazí, když už je počítač zaregistrovaný](./media/install-the-windows-pc-client-with-microsoft-intune/page-shown-if-pc-already-enrolled.png)

## <a name="monitor-and-validate-successful-client-deployment"></a>Sledování a ověření úspěšného nasazení klienta
Pomocí některého z následujících postupů můžete sledovat a ověřit úspěšné nasazení klienta.

### <a name="to-verify-the-installation-of-the-client-software-from-the-microsoft-intune-administrator-console"></a>Ověření instalace klientského softwaru v konzole správce Microsoft Intune

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/) klikněte na **Skupiny** &gt; **Všechna zařízení** &gt; **Všechny počítače**.

2. V seznamu vyhledejte počítače, které komunikují s Intune, nebo vyhledejte konkrétní spravovaný počítač po zadání názvu počítače (nebo libovolné části názvu) do pole **Hledat zařízení**.

3. V dolním podokně konzoly zkontrolujte stav počítače. Vyřešte všechny chyby.

### <a name="to-create-a-computer-inventory-report-to-display-all-enrolled-computers"></a>Vytvoření sestavy inventáře počítače pro zobrazení všech zaregistrovaných počítačů

1. V [konzole pro správu Microsoft Intune](https://manage.microsoft.com/) klikněte na **Sestavy** &gt; **Sestavy inventáře počítače**.

2. Na stránce **Vytvořit novou sestavu** nechejte ve všech polích výchozí hodnoty (pokud nechcete použít filtry) a klikněte na **Zobrazit sestavu**.

3. Stránka **Sestava inventáře počítače** se otevře v novém okně s uvedením všech počítačů, které jsou úspěšně zaregistrované v Intune.

    > [!TIP]
    > Kliknutím na záhlaví libovolného sloupce v sestavě seřadíte seznam podle obsahu sloupce.

## <a name="uninstall-the-windows-client-software"></a>Odinstalace klientského softwaru Windows

Existují dva způsoby, jak zrušit registraci klientského softwaru Windows:

- Z konzoly pro správu Intune (doporučená metoda)
- Z příkazového řádku v klientovi

### <a name="unenroll-by-using-the-intune-admin-console"></a>Zrušení registrace pomocí konzoly pro správu Intune

Pokud chcete zrušit registraci softwarového klienta pomocí konzoly pro správu Intune, klikněte na **skupiny**  >  **všechny počítače**  >  **zařízení**. Klikněte pravým tlačítkem na klienta a vyberte **Vyřadit/vymazat**.

### <a name="unenroll-by-using-a-command-prompt-on-the-client"></a>Zrušení registrace pomocí příkazového řádku v klientovi

Na příkazovém řádku se zvýšenými oprávněními spusťte jeden z následujících příkazů.

**Metoda 1**:

```cmd
"C:\Program Files\Microsoft\OnlineManagement\Common\ProvisioningUtil.exe" /UninstallAgents /MicrosoftIntune
```

**Metoda 2** (všimněte si, že všichni toto agenti jsou nainstalováni v každé verzi SKU systému Windows):

```cmd
wmic product where name="Microsoft Endpoint Protection Management Components" call uninstall
wmic product where name="Microsoft Intune Notification Service" call uninstall
wmic product where name="System Center 2012 - Operations Manager Agent" call uninstall
wmic product where name="Microsoft Online Management Policy Agent" call uninstall
wmic product where name="Microsoft Policy Platform" call uninstall
wmic product where name="Microsoft Security Client" call uninstall
wmic product where name="Microsoft Online Management Client" call uninstall
wmic product where name="Microsoft Online Management Client Service" call uninstall
wmic product where name="Microsoft Easy Assist v2" call uninstall
wmic product where name="Microsoft Intune Monitoring Agent" call uninstall
wmic product where name="Windows Intune Endpoint Protection Agent" call uninstall
wmic product where name="Windows Firewall Configuration Provider" call uninstall
wmic product where name="Microsoft Intune Center" call uninstall
wmic product where name="Microsoft Online Management Update Manager" call uninstall
wmic product where name="Microsoft Online Management Agent Installer" call uninstall
wmic product where name="Microsoft Intune" call uninstall
wmic product where name="Windows Endpoint Protection Management Components" call uninstall
wmic product where name="Windows Intune Notification Service" call uninstall
wmic product where name="System Center 2012 - Operations Manager Agent" call uninstall
wmic product where name="Windows Online Management Policy Agent" call uninstall
wmic product where name="Windows Policy Platform" call uninstall
wmic product where name="Windows Security Client" call uninstall
wmic product where name="Windows Online Management Client" call uninstall
wmic product where name="Windows Online Management Client Service" call uninstall
wmic product where name="Windows Easy Assist v2" call uninstall
wmic product where name="Windows Intune Monitoring Agent" call uninstall
wmic product where name="Windows Intune Endpoint Protection Agent" call uninstall
wmic product where name="Windows Firewall Configuration Provider" call uninstall
wmic product where name="Windows Intune Center" call uninstall
wmic product where name="Windows Online Management Update Manager" call uninstall
wmic product where name="Windows Online Management Agent Installer" call uninstall
wmic product where name="Windows Intune" call uninstall
```

> [!TIP]
> Zrušení registrace klienta zanechá pro tohoto klienta zastaralý záznam na straně serveru. Proces zrušení registrace je asynchronní a odinstalovává se devět agentů. Dokončení odinstalace tak může trvat až 30 minut.

### <a name="check-the-unenrollment-status"></a>Kontrola stavu zrušení registrace

Zkontrolujte cestu %ProgramFiles%\Microsoft\OnlineManagement a ujistěte se, že jsou na levé straně zobrazeny pouze následující adresáře:

- AgentInstaller
- Protokoly
- Aktualizace
- Společné

### <a name="remove-the-onlinemanagement-folder"></a>Odebrání složky OnlineManagement

Proces zrušení registrace neodebere složku OnlineManagement. Po dokončení odinstalace počkejte 30 minut a spusťte tento příkaz. Pokud byste ho spustili příliš brzy, odinstalace by mohla zůstat v neznámém stavu. Složku odeberte spuštěním příkazového řádku se zvýšenými oprávněními a spuštěním následujícího příkazu:

```cmd
rd /s /q %ProgramFiles%\Microsoft\OnlineManagement
```

## <a name="next-steps"></a>Další kroky
[Běžné úlohy správy počítačů s Windows pomocí klientského softwaru Intune](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
