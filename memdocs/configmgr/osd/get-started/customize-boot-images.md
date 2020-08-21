---
title: Přizpůsobení spouštěcích imagí
titleSuffix: Configuration Manager
description: Přečtěte si několik způsobů použití Configuration Manager nebo nástroje příkazového řádku Obsluha a správa bitových kopií (DISM) k přizpůsobení spouštěcí bitové kopie.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e4fc5b019de25234ae964137f6b374ecbbca7d8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697785"
---
# <a name="customize-boot-images-with-configuration-manager"></a>Přizpůsobení spouštěcích bitových kopií pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Každá verze Configuration Manager podporuje určitou verzi sady Windows Assessment and Deployment Kit (Windows ADK). Spouštěcí bitové kopie lze obsluhovat, neboli přizpůsobit, z konzoly Configuration Manager, pokud jsou založeny na verzi prostředí Windows PE z podporované verze sady Windows ADK. Ostatní spouštěcí bitové kopie je nutné přizpůsobit jiným způsobem, například pomocí nástroje příkazového řádku Obsluha a správa bitových kopií (DISM), který je součástí sad Windows AIK a Windows ADK.  

 Následující článek uvádí podporovanou verzi sady Windows ADK, verzi prostředí Windows PE, na které je založena spouštěcí bitová kopie, kterou lze přizpůsobit z konzoly Configuration Manager, a verze prostředí Windows PE, na kterých je založena spouštěcí image, kterou lze přizpůsobit pomocí nástroje DISM a potom přidat do Configuration Manager.  

- **Verze sady Windows ADK**  

   Sada Windows ADK pro Windows 10  

- **Verze prostředí Windows PE pro spouštěcí bitové kopie přizpůsobitelné z konzoly Configuration Manager**  

   Windows PE 10  

- **Podporované verze prostředí Windows PE pro spouštěcí bitové kopie, které nelze přizpůsobit z konzoly Configuration Manager**  

   Windows PE 3.1<sup>1</sup> a Windows PE 5  

   <sup>1</sup> Pokud je založená na prostředí Windows PE 3,1, můžete do Configuration Manager přidat pouze spouštěcí bitovou kopii. Instalováním doplňku Windows AIK Supplement pro Windows 7 SP1 upgradujte sadu Windows AIK pro Windows 7 (na platformě Windows PE 3) s doplňkem Windows AIK Supplement pro Windows 7 SP1 (na platformě Windows PE 3.1). Doplněk Windows AIK Supplement pro Windows 7 SP1 lze stáhnout z webu [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=5188).  

   Pokud máte například Configuration Manager, můžete v konzole Configuration Manager přizpůsobit spouštěcí bitové kopie ze sady Windows ADK pro Windows 10 (na platformě Windows PE 10). Nicméně i když jsou podporované image na platformě Windows PE 5, je potřeba je přizpůsobit z jiného počítače pomocí verze nástroje DISM, která se instaluje se sadou Windows ADK pro Windows 8. Potom můžete přidat spouštěcí bitovou kopii do konzoly Configuration Manager.  

  Postupy v tomto tématu ukazují, jak přidat volitelné součásti požadované nástrojem Configuration Manager do spouštěcí bitové kopie pomocí následujících balíčků systému Windows PE:  

- **WinPE-WMI**: Přidává podporu rozhraní WMI (Windows Management Instrumentation).  

- **WinPE-Scripting**: Přidává podporu prostředí WSH (Windows Script Host).  

- **WinPE-WDS-Tools**: Instaluje nástroje služby pro nasazení systému Windows.  

  Dostupné jsou i další balíčky prostředí Windows PE, které lze přidat. Další informace o volitelných součástech, které lze přidat do spouštěcí bitové kopie, naleznete v tématu [WinPE: Přidání balíčků (odkazy na volitelné součásti)](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

> [!NOTE]
>Při spuštění prostředí WinPE z vlastní spouštěcí image, která obsahuje nástroje, které jste přidali, můžete otevřít příkazový řádek z prostředí WinPE a zadáním názvu souboru nástroje ho spustit. Umístění těchto nástrojů se automaticky přidá do proměnné PATH. Příkazový řádek lze přidat pouze v případě, že je vybráno nastavení **Povolit podporu příkazů (pouze testování)** na kartě **vlastní nastavení** ve vlastnostech spouštěcí bitové kopie.

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>Přizpůsobení spouštěcí image používající prostředí Windows PE 5  
 Chcete-li přizpůsobit spouštěcí image používající Windows PE 5, je nutné nainstalovat sadu Windows ADK a pomocí nástroje příkazového řádku DISM připojit spouštěcí image, přidat volitelné komponenty a ovladače, a provést změny ve spouštěcí imagi. K přizpůsobení spouštěcí bitové kopie použijte následující postup.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>Přizpůsobení spouštěcí image používající prostředí Windows PE 5  

1. Nainstalujte sadu Windows ADK na počítač, který nemá jinou verzi sady Windows AIK nebo Windows ADK, a neobsahuje žádné nainstalované součásti Configuration Manager.  

2. Stáhněte si sadu Windows ADK pro Windows 8.1 z webu [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39982).  

3. Zkopírujte spouštěcí image (wimpe. wim) z instalační složky systému Windows ADK (například <*cesta instalace*> \Windows Kit \\ < *version*> \Assessment a nasazení Kit\Windows předinstalační prostředí \\ < *x86 nebo amd64* > \\ < *locale*>) do cílové složky v počítači, ze kterého budete přizpůsobovat spouštěcí bitovou kopii. V tomto postupu slouží označení C:\WinPEWAIK jako název cílové složky.  

4. Pomocí nástroje DISM připojte spouštěcí image k místní složce prostředí Windows PE. Zadejte například následující příkazový řádek:  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    Kde C:\WinPEWAIK představuje složku obsahující spouštěcí bitovou kopii a C:\WinPEMount představuje připojenou složku.  

   > [!NOTE]
   >  Další informace najdete v referenčních informacích o [nástroji DISM (Údržba a správa bitových kopií nasazení)](/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management).

5. Po připojení spouštěcí bitové kopie do ní pomocí nástroje Obsluha a správa bitových kopií přidejte volitelné součásti. V prostředí Windows PE 5 jsou 64bitové volitelné komponenty umístěny ve složce <*Instalační_cesta*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs.  

   > [!NOTE]
   >  Tento postup pro volitelné součásti používá toto umístění: C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs. Použitá cesta se může lišit v závislosti na verzi a možnostech instalace vybraných pro sadu Windows ADK.  

    Volitelné součásti instalujete zadáním následujících řádků:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<národní prostředí\>* **\WinPE-SecureStartup_** *<národní prostředí\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<národní prostředí\>* **\WinPE-WMI_** *<národní prostředí\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<národní prostředí\>* **\WinPE-Scripting** *<národní prostředí\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<národní prostředí\>* **\WinPE-WDS-Tools_** *<národní prostředí\>* **.cab"**  

    Kde C:\WinPEMount je připojená složka a národní prostředí je národní prostředí pro komponenty. Pro národní prostředí **en-us** například zadejte:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

   > [!TIP]
   >  Další informace o volitelných součástech, které můžete přidat do spouštěcí image, najdete v referenčních informacích k [volitelným součástem prostředí Windows PE](/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).

6. Pomocí nástroje Obsluha a správa bitových kopií (DISM) přidejte do spouštěcí bitové kopie konkrétní ovladače, pokud je to třeba. Ovladače přidáte do spouštěcí bitové kopie zadáním následujícího řádku:  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *cesta k souboru .inf ovladače* **>**  

    Kde C:\WinPEMount představuje připojenou složku.  

7. Zadáním následujícího řádku odpojte spouštěcí bitovou kopii a proveďte změny.  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Kde C:\WinPEMount představuje připojenou složku.  

8. Přidejte aktualizovanou spouštěcí bitovou kopii pro Configuration Manager, aby ji bylo možné použít v pořadí úloh. K importu aktualizované spouštěcí bitové kopie použijte následující postup:  

   1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

   2. V pracovním prostoru **Softwarová knihovna** rozbalte možnost **Operační systémy** a klikněte na položku **Spouštěcí bitové kopie**.  

   3. Kliknutím na možnost **Přidat spouštěcí bitovou kopii** na kartě **Domů** ve skupině **Vytvořit** spusťte Průvodce přidáním bitové spouštěcí kopie.  

   4. Na stránce **Zdroj dat** určete následující možnosti a klikněte na tlačítko **Další**.  

      - V poli **Cesta** určete cestu k souboru aktualizované spouštěcí bitové kopie. Zadaná cesta musí být platná síťová cesta ve formátu UNC. Příklad: **\\\\<** <em>servername</em> **>\\<** <em>WinPEWAIK Share</em> **> \Winpe.wim**.  

      - Vyberte spouštěcí bitovou kopii z rozevíracího seznamu **Spouštěcí bitová kopie**. Jestliže soubor WIM obsahuje více spouštěcích bitových kopií, budou v seznamu uvedeny všechny.  

   5. Na stránce **Obecné** určete následující možnosti klikněte na tlačítko **Další**.  

      -   V poli **Název** zadejte unikátní název spouštěcí bitové kopie.  

      -   V poli **Verze** zadejte číslo verze spouštěcí bitové kopie.  

      -   V poli **Komentář** zadejte stručný popis, jak bude spouštěcí bitová kopie používána.  

   6. Dokončete průvodce.  

9. Ve spouštěcí imagi lze povolit příkazové okno umožňující její ladění a odstraňování potíží v prostředí Windows PE. Příkazové prostředí povolíte pomocí následujícího postupu.  

   1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

   2. V pracovním prostoru **Softwarová knihovna** rozbalte možnost **Operační systémy** a klikněte na položku **Spouštěcí bitové kopie**.  

   3. V seznamu vyhledejte novou spouštěcí bitovou kopii a určete ID balíčku této bitové kopie. ID balíčku naleznete ve sloupci **ID bitové kopie** této spouštěcí bitové kopie.  

   4. Do příkazového řádku zadejte **wbemtest** a otevřete nástroj Testování služby WMI.  

   5. **\\\\<** Do** \root\sms\ site_<** <em>SiteCode</em> v oboru názvů zadejte <em>počítač poskytovatele SMS</em>> **>** a pak klikněte na **připojit**. **Namespace**  

   6. Klikněte na **Otevřít instanci**, zadejte **sms_bootimagepackage.packageID="<ID_balíčku\>"**, a poté klikněte na **OK**. Místo ID_balíčku zadejte hodnotu určenou v kroku 3.  

   7. Klikněte na tlačítko **Aktualizovat objekt** a poté v okně **Vlastnosti** klikněte na vlastnost **EnableLabShell**.  

   8. Klikněte na **Upravit vlastnost**, změňte hodnotu na **TRUE** a klikněte na **Uložit vlastnost**.  

   9. Klikněte na **Uložit objekt** a pak Testování služby WMI ukončete.  

10. Spouštěcí bitovou kopii je nutné nejprve distribuovat do distribučních bodů, do skupin distribučních bodů nebo do kolekcí přidružených ke skupinám distribučních bodů, aby ji bylo možné použít v pořadí úloh. K distribuci spouštěcí bitové kopie použijte následující postup.  

    1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

    2.  V pracovním prostoru **Softwarová knihovna** rozbalte možnost **Operační systémy** a klikněte na položku **Spouštěcí bitové kopie**.  

    3.  Klikněte na spouštěcí image určenou v kroku 3.  

    4.  Na kartě **Domů** ve skupině **Nasazení** klikněte na možnost **Aktualizovat distribuční body**.  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>Přizpůsobení spouštěcí image používající prostředí Windows PE 3.1  
 Chcete-li přizpůsobit spouštěcí image používající prostředí WinPE 3.1, je nutné nainstalovat sadu Windows AIK, nainstalovat doplněk Windows AIK Supplement pro Windows 7 SP1, a pomocí nástroje příkazového řádku DISM připojit spouštěcí image, přidat volitelné komponenty a ovladače, a provést změny ve spouštěcí imagi. K přizpůsobení spouštěcí bitové kopie použijte následující postup.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>Přizpůsobení spouštěcí image používající prostředí Windows PE 3.1  

1. Nainstalujte sadu Windows AIK na počítač, který nemá jinou verzi sady Windows AIK nebo Windows ADK a neobsahuje žádné nainstalované součásti Configuration Manager. Sadu Windows AIK si můžete stáhnout z webu [Stažení softwaru](https://www.microsoft.com/download/details.aspx?id=5753).  

2. Nainstalujte doplněk Windows AIK Supplement pro Windows 7 s aktualizací SP1 do počítače z kroku 1. Doplněk Windows AIK Supplement for Windows 7 SP1 si můžete stáhnout z webu [Stažení softwaru](https://www.microsoft.com/download/details.aspx?id=5188).  

3. Zkopírujte spouštěcí bitovou kopii (wimpe. wim) z instalační složky sady Windows AIK (například <*InstallationPath*> \Windows AIK\Tools\PETools\amd64 \\ ) do složky v počítači, ze kterého budete přizpůsobovat spouštěcí bitovou kopii. V tomto postupu slouží označení C:\WinPEWAIK jako název složky.  

4. Pomocí nástroje DISM připojte spouštěcí image k místní složce prostředí Windows PE. Zadejte například následující příkazový řádek:  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    Kde C:\WinPEWAIK představuje složku obsahující spouštěcí bitovou kopii a C:\WinPEMount představuje připojenou složku.  

   > [!NOTE]
   > Další informace najdete v referenčních informacích o [nástroji DISM (Údržba a správa bitových kopií nasazení)](/windows-hardware/manufacture/desktop/dism-reference--deployment-image-servicing-and-management).

5. Po připojení spouštěcí bitové kopie do ní pomocí nástroje Obsluha a správa bitových kopií přidejte volitelné součásti. V systému Windows PE 3,1 jsou například volitelné součásti umístěny ve složce <*InstallationPath*> \windows AIK\Tools\PETools\amd64\ WinPE_FPs \\ .  

   > [!NOTE]
   >  V tomto postupu se pro volitelné součásti používá toto umístění: C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs. Použitá cesta se může lišit v závislosti na verzi a možnostech instalace vybraných pro sadu Windows AIK.  

    Volitelné součásti instalujete zadáním následujících řádků:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<národní prostředí\>* **\winpe-wmi_** *<národní prostředí\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<národní prostředí\>* **\winpe-scripting_** *<národní prostředí\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<národní prostředí\>* **\winpe-wds-tools_** *<národní prostředí\>* **.cab"**  

    Kde C:\WinPEMount je připojená složka a národní prostředí je národní prostředí pro komponenty. Pro národní prostředí **en-us** například zadejte:  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

   > [!TIP]
   >  Další informace o různých balíčcích, které můžete přidat do spouštěcí image, najdete v tématu [Přidání balíčku do image prostředí Windows PE](/previous-versions/windows/it-pro/windows-7/dd799312(v=ws.10)).

6. Pomocí nástroje Obsluha a správa bitových kopií (DISM) přidejte do spouštěcí bitové kopie konkrétní ovladače, pokud je to třeba. Ovladače přidáte do spouštěcí bitové kopie zadáním následujícího řádku, pokud je to třeba:  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:<** *cesta k souboru .inf ovladače* **>**  

    Kde C:\WinPEMount představuje připojenou složku.  

7. Zadáním následujícího řádku odpojte spouštěcí bitovou kopii a proveďte změny.  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Kde C:\WinPEMount představuje připojenou složku.  

8. Přidejte aktualizovanou spouštěcí bitovou kopii pro Configuration Manager, aby ji bylo možné použít v pořadí úloh. K importu aktualizované spouštěcí bitové kopie použijte následující postup:  

   1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

   2. V pracovním prostoru **Softwarová knihovna** rozbalte možnost **Operační systémy** a klikněte na položku **Spouštěcí bitové kopie**.  

   3. Kliknutím na možnost **Přidat spouštěcí bitovou kopii** na kartě **Domů** ve skupině **Vytvořit** spusťte Průvodce přidáním bitové spouštěcí kopie.  

   4. Na stránce **Zdroj dat** určete následující možnosti a klikněte na tlačítko **Další**.  

      - V poli **Cesta** určete cestu k souboru aktualizované spouštěcí bitové kopie. Zadaná cesta musí být platná síťová cesta ve formátu UNC. Příklad: **\\\\<** <em>servername</em> **>\\<** <em>WinPEWAIK Share</em> **> \Winpe.wim**.  

      - Vyberte spouštěcí bitovou kopii z rozevíracího seznamu **Spouštěcí bitová kopie**. Jestliže soubor WIM obsahuje více spouštěcích bitových kopií, budou v seznamu uvedeny všechny.  

   5. Na stránce **Obecné** určete následující možnosti klikněte na tlačítko **Další**.  

      -   V poli **Název** zadejte unikátní název spouštěcí bitové kopie.  

      -   V poli **Verze** zadejte číslo verze spouštěcí bitové kopie.  

      -   V poli **Komentář** zadejte stručný popis, jak bude spouštěcí bitová kopie používána.  

   6. Dokončete průvodce.  

9. Ve spouštěcí imagi lze povolit příkazové okno umožňující její ladění a odstraňování potíží v prostředí Windows PE. Příkazové prostředí povolíte pomocí následujícího postupu.  

   1. V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

   2. V pracovním prostoru **Softwarová knihovna** rozbalte možnost **Operační systémy** a klikněte na položku **Spouštěcí bitové kopie**.  

   3. V seznamu vyhledejte novou spouštěcí bitovou kopii a určete ID balíčku této bitové kopie. ID balíčku naleznete ve sloupci **ID bitové kopie** této spouštěcí bitové kopie.  

   4. Do příkazového řádku zadejte **wbemtest** a otevřete nástroj Testování služby WMI.  

   5. **\\\\<** Do** \root\sms\ site_<** <em>SiteCode</em> v oboru názvů zadejte <em>počítač poskytovatele SMS</em>> **>** a pak klikněte na **připojit**. **Namespace**  

   6. Klikněte na **Otevřít instanci**, zadejte **sms_bootimagepackage.packageID="<ID_balíčku\>"**, a poté klikněte na **OK**. Místo ID_balíčku zadejte hodnotu určenou v kroku 3.  

   7. Klikněte na tlačítko **Aktualizovat objekt** a poté v okně **Vlastnosti** klikněte na vlastnost **EnableLabShell**.  

   8. Klikněte na **Upravit vlastnost**, změňte hodnotu na **TRUE** a klikněte na **Uložit vlastnost**.  

   9. Klikněte na **Uložit objekt** a pak Testování služby WMI ukončete.  

10. Spouštěcí bitovou kopii je nutné nejprve distribuovat do distribučních bodů, do skupin distribučních bodů nebo do kolekcí přidružených ke skupinám distribučních bodů, aby ji bylo možné použít v pořadí úloh. K distribuci spouštěcí bitové kopie použijte následující postup.  

    1.  V konzole Správce konfigurace klikněte na možnost **Knihovna softwarů**.  

    2.  V pracovním prostoru **Softwarová knihovna** rozbalte možnost **Operační systémy** a klikněte na položku **Spouštěcí bitové kopie**.  

    3.  Klikněte na spouštěcí image určenou v kroku 3.  

    4.  Na kartě **Domů** ve skupině **Nasazení** klikněte na možnost **Aktualizovat distribuční body**.