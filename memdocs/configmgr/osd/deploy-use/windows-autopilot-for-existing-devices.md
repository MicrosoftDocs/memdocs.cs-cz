---
title: Windows Autopilot pro existující zařízení
titleSuffix: Configuration Manager
description: Použití pořadí úloh Configuration Manager k obnovení image a zřízení zařízení se systémem Windows 7 pro režim založený na uživatelském programu Windows autopilot
ms.date: 03/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9f2ddf106c641c4433ddd1d09a2457900f670e8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724206"
---
# <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot pro existující zařízení
<!--3607717, fka 1358333-->

*Platí pro: Configuration Manager (Current Branch)*

[Windows autopilot pro Windows](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) poskytuje organizacím možnost dodávat čerstvá, neovládaná zařízení s Windows 10 přímo koncovému uživateli a definovat tok zřizování, který uživatel projde, aby získal zabezpečené a produktivní zařízení s Windows 10. Zařízení je zaregistrované ve službě Windows autopilot, takže můžete přiřadit potřebný profil Windows autopilotu. Tento profil definuje spouštěné prostředí (OOBE) pro toto zařízení. 

[Windows autopilot pro stávající zařízení](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) je k dispozici ve Windows 10 verze 1809 nebo novější. Tato funkce umožňuje obnovení image a zřízení zařízení se systémem Windows 7 pro [uživatele se systémem Windows autopilot na základě](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) jednoho nativního Configuration Managerho pořadí úloh. 



## <a name="prerequisites"></a>Požadavky

- Získejte instalační médium pro Windows 10 verze 1809 nebo novější. Pak vytvořte bitovou kopii operačního systému Configuration Manager. Další informace najdete v tématu [Správa imagí operačního systému](../get-started/manage-operating-system-images.md).

- V Microsoft Intune vytvořte profily pro Windows autopilot. Další informace najdete v tématu [registrace zařízení s Windows v Intune pomocí automatických pilotů Windows](https://docs.microsoft.com/intune/enrollment-autopilot).

- Zařízení, které ještě není zaregistrované ve službě Windows autopilot. Pokud je zařízení už zaregistrované, má přednost přiřazený profil. Profil autopilot pro stávající zařízení se použije jenom v případě, že časový limit pro online profil vypršel.



## <a name="create-the-configuration-file"></a>Vytvoření konfiguračního souboru

1. Na zařízení s Windows s připojením k Internetu otevřete okno příkazového řádku PowerShellu pro správu a spusťte následující příkazy:  

    1. Pokud chcete pokračovat, nainstalujte požadované moduly a potvrďte výzvy.  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Přihlášení k Intune s přihlašovacími údaji správce  
        ``` PowerShell  
        connect-msgraph 
        ```

    3. Načte všechny profily Windows autopilotu přidružené k vašemu tenantovi Intune.  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Vytvořte konfigurační soubor pro každý profil. Soubory jsou pojmenovány pro zobrazovaný název profilu a jsou uloženy na ploše aktuálního uživatele.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > Konfigurační soubor může obsahovat pouze jeden profil. Každý profil musí být ve složených závorkách `{}`.  

2. Uložte jeden z profilů do souboru s kódováním ANSI s názvem **AutopilotConfigurationFile. JSON**. Uložte ho do umístění vhodného jako zdroj Configuration Manager balíčku.  

    > [!Tip]  
    > Pokud použijete výstupní **soubor** rutiny PowerShellu pro přesměrování výstupu JSON do souboru, ve výchozím nastavení se použije kódování Unicode. Tato rutina může také zkrátit dlouhé řádky. K nastavení správného kódování textu použijte rutinu `-Encoding ASCII` **Set-content** s parametrem.   
    > 
    > Ve výchozím nastavení používá program Windows Notepad kódování ANSI.  

3. Vytvořte balíček Configuration Manager, který obsahuje tento soubor. Nevyžaduje program. Další informace najdete v tématu [Vytvoření balíčku](../../apps/deploy-use/packages-and-programs.md#create-a-package-and-program).  

    > [!NOTE]  
    > Systém Windows vyžaduje, aby byl tento soubor pojmenován **AutopilotConfigurationFile. JSON**. Chcete-li použít více než jeden profil autopilotu, vytvořte samostatné balíčky Configuration Manager.  



## <a name="create-the-task-sequence"></a>Vytvoření pořadí úkolů

1. V konzole Configuration Manager otevřete pracovní prostor **Knihovna softwaru** , rozbalte možnost **operační systémy**a vyberte uzel **pořadí úloh** . Na pásu karet vyberte **vytvořit pořadí úloh** .  

2. Na stránce **vytvořit nové pořadí úloh** vyberte možnost **nasazení Windows autopilot pro existující zařízení**.  

3. Na stránce **informace o pořadí úloh** zadejte název, Volitelně přidejte popis a vyberte spouštěcí bitovou kopii. Další informace o podporovaných verzích spouštěcí bitové kopie najdete v tématu [Podpora pro Windows 10](../../core/plan-design/configs/support-for-windows-10.md#windows-10-adk).  

4. Na stránce **instalovat systém Windows** vyberte **balíček bitové kopie**systému Windows 10. Pak nakonfigurujte následující nastavení:  

    - **Index bitové kopie**: vyberte možnost Enterprise, školství nebo Professional, jak to vyžaduje vaše organizace.  

    - Povolit možnost **rozdělit a naformátovat cílový počítač před instalací operačního systému**  

    - **Konfigurace pořadí úkolů pro použití s nástrojem BitLocker**: Pokud povolíte tuto možnost, pořadí úkolů zahrnuje kroky nutné k povolení nástroje BitLocker.  

    - **Kód Product Key**: Pokud potřebujete zadat kód Product Key pro aktivaci Windows, zadejte ho sem.  

    - Vyberte jednu z následujících možností konfigurace účtu místního správce ve Windows 10:  
        - **Náhodně generovat heslo místního správce a vypnout účet na všech platformách podpory (doporučeno)**
        - **Zapnout účet a zadat heslo místního správce**

5. Na stránce **Konfigurovat síť** vyberte možnost **připojení k pracovní skupině**. Toto pořadí úloh používá nástroj pro přípravu systému Windows (Sysprep). Pokud je zařízení připojené k doméně, Sysprep se nezdařil.  

6. Na stránce **instalovat nástroj Configuration Manager** přidejte všechny nezbytné vlastnosti instalace pro vaše prostředí.  

    > [!Tip]  
    > Pořadí úkolů potřebuje tyto informace pouze v případě, že Configuration Manager klientské komponenty jsou potřeba během pořadí úkolů před spuštěním nástroje Sysprep. Například pro instalaci aktualizací softwaru nebo aplikací. Pokud tyto akce neuděláte, klient není potřeba. Před spuštěním nástroje Sysprep pořadím úloh je odinstalován.  

7. Ve výchozím nastavení se na stránce **Zahrnout aktualizace** vybere možnost **Neinstalovat žádné aktualizace softwaru**.  

    > [!Tip]  
    > Pomocí offline údržby imagí Udržujte image v aktuálním stavu s nejnovějšími aktualizacemi Windows 10 Quality. Další informace najdete v tématu [použití aktualizací softwaru na bitovou kopii operačního systému](../get-started/manage-operating-system-images.md#BKMK_OSImagesApplyUpdates).  

8. Na stránce **instalovat aplikace** můžete vybrat aplikace, které se mají během pořadí úkolů nainstalovat. Společnost Microsoft však doporučuje, abyste v tomto scénáři rozrážejí přístup k imagi podpisů. Jakmile zařízení zřídí s autopilotem, použijte všechny aplikace a konfigurace z Microsoft Intune nebo Configuration Manager spolusprávu. Tento proces nabízí konzistentní prostředí pro uživatele, kteří přijímají nová zařízení a používají pro stávající zařízení Windows autopiloter.  

8. Na stránce **Příprava systému** vyberte balíček, který obsahuje konfigurační soubor autopilotu. Ve výchozím nastavení pořadí úkolů restartuje počítač po spuštění nástroje Windows Sysprep. Můžete také vybrat možnost **vypnutí počítače po dokončení tohoto pořadí úloh**. Tato možnost umožňuje připravit zařízení a pak ho doručit uživateli pro konzistentní prostředí autopilotního pilotu.  

9. Dokončete průvodce.  

Pokud pořadí úkolů upravíte, bude podobné jako výchozí pořadí úkolů pro použití existující image operačního systému. Toto pořadí úkolů zahrnuje následující další kroky:  

- **Použít konfiguraci Windows autopilotu**: Tento krok aplikuje konfigurační soubor autopilotu ze zadaného balíčku. Nejedná se o nový typ kroku, jedná se o krok **spuštění příkazového řádku** pro zkopírování souboru.  

- **Příprava systému Windows pro zaznamenání**: Tento krok spustí nástroj Windows Sysprep a má nastavení pro **vypnutí počítače po spuštění této akce**. Další informace najdete v tématu [Příprava systému Windows pro zachytávání](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

Výsledkem pořadí úloh Windows autopilot for existing pro stávající zařízení je zařízení připojené k Azure Active Directory (Azure AD). 

> [!NOTE]  
> S Windows 10 verze 1903 a verze 1909 má nástroj pro autopilote známý problém, kdy nástroj Sysprep odstraní soubor **AutopilotConfigurationFile. JSON** . Použijete-li tuto metodu k nasazení systému Windows 10 verze 1903 nebo verze 1909, upravte toto pořadí úloh a proveďte následující změny:
>
> 1. Zakažte krok **připravit systém Windows pro zaznamenání** .
> 2. Hned za krokem zakázané **přípravy Windows pro zaznamenání** přidejte nový krok **Spustit příkazový řádek** . Nakonfigurujte ji tak, aby spouštěla následující příkazový řádek:`c:\windows\system32\sysprep\sysprep.exe /oobe /reboot`
>
> Další informace najdete v tématu [Windows autopilot – známé problémy](https://docs.microsoft.com/windows/deployment/windows-autopilot/known-issues).

Pomocí [umístění známé složky](https://docs.microsoft.com/onedrive/redirect-known-folders) na OneDrivu pro firmy se můžete ujistit, že jsou data uživatele před upgradem Windows 10 zálohovaná.



## <a name="next-steps"></a>Další kroky

Využijte spolusprávu a vylepšete funkce správy zařízení s Windows 10. Druhá cesta k spolusprávě je prostřednictvím moderního zřizování s Windows autopilotem. Další informace najdete v těchto článcích:

- [Co je spoluspráva?](../../comanage/overview.md)
- [Cesty ke spolusprávě](../../comanage/quickstart-paths.md)
- [Windows Autopilot se spolusprávou](../../comanage/quickstart-autopilot.md)

## <a name="see-also"></a>Viz také

- [Registrace zařízení s Windows v Intune pomocí automatických pilotů Windows](https://docs.microsoft.com/intune/enrollment-autopilot)
