---
title: Jak hromadně registrovat zařízení
titleSuffix: Configuration Manager
description: Hromadná registrace zařízení s využitím místní správy mobilních zařízení (MDM) v Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 474d59ec22d1edaf8e662298e90555e6772d302b
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698792"
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Jak hromadně registrovat zařízení pomocí místní správy mobilních zařízení (MDM) v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Hromadná registrace v Configuration Manager místní správě mobilních zařízení (MDM) je automatizovaná metoda registrace zařízení. Druhou metodou je registrace uživatele, která vyžaduje, aby uživatelé zadali své přihlašovací údaje k registraci zařízení. Při hromadné registraci se registrované zařízení ověřuje pomocí registračního balíčku. Balíček je soubor. ppkg, který může také obsahovat profily certifikátů a Wi-Fi pro podporu registrace.

## <a name="create-a-certificate-profile"></a><a name="bkmk_createCert"></a> Vytvoření profilu certifikátu

Přidejte profil certifikátu pro automatickou instalaci důvěryhodného kořenového certifikátu do zařízení. Tento kořenový certifikát je nutný pro důvěryhodnou komunikaci mezi zařízeními a rolemi systému lokality, které jsou potřeba pro místní správu mobilních zařízení (MDM).

Když připravíte lokalitu pro místní správu mobilních zařízení (MDM), exportujete důvěryhodný kořenový certifikát. Tento certifikát použijte v profilu certifikátu registračního balíčku. Další informace o tom, jak získat důvěryhodný kořenový certifikát, najdete v tématu [Export důvěryhodného kořenového certifikátu](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).

Pomocí exportovaného certifikátu vytvořte profil certifikátu. Další informace najdete v tématu [Vytvoření profilů certifikátů](../../protect/deploy-use/create-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a><a name="CreateWifi"></a> Vytvoření profilu sítě Wi-Fi

Další komponentou balíčku hromadného zápisu je profil sítě Wi-Fi. Tento profil může zajistit, že zařízení má síťové připojení, aby podporovalo registraci.

Další informace o tom, jak vytvořit profil sítě Wi-Fi v Configuration Manager, najdete v tématu [Postup vytvoření profilů sítě Wi-Fi](../../protect/deploy-use/create-wifi-profiles.md).

### <a name="wi-fi-profile-limitations"></a>Omezení profilů sítě Wi-Fi

Když vytváříte profil sítě Wi-Fi pro místní registraci MDM, prostudujte si následující omezení.

#### <a name="wi-fi-security-configurations-for-on-premises-mdm"></a>Konfigurace zabezpečení Wi-Fi pro místní správu mobilních zařízení (MDM)

Aktuální větev Configuration Manager podporuje jenom tyto konfigurace zabezpečení Wi-Fi pro místní správu mobilních zařízení (MDM):

- Typy zabezpečení: **WPA2-podnikové** nebo **WPA2-osobní**

- Typy šifrování: **AES** nebo **TKIP**

- Typy protokolu EAP: **Čipová karta nebo jiný certifikát** nebo **PEAP**

#### <a name="proxy-server"></a>Proxy server

I když Configuration Manager obsahuje nastavení proxy server informace v profilu Wi-Fi, nekonfiguruje proxy server, když se zařízení zaregistruje. Pokud potřebujete nastavit proxy server na hromadně zaregistrovaná zařízení:

- Po registraci zařízení nasaďte nastavení pomocí položek konfigurace.

- Vytvořte druhý balíček pomocí nástroje Windows Image and Configuration Designer (ICD) a pak ho nasaďte společně s balíčkem hromadného zápisu.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a> Vytvoření profilu zápisu

Registrační profil umožňuje zadat nastavení požadovaná pro registraci zařízení. Tato nastavení zahrnují [Profil certifikátu](#bkmk_createCert) a profil sítě [Wi-Fi](#CreateWifi).

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte **všechna zařízení vlastněná společností**, rozbalte **Windows**a vyberte uzel **registrační profily** .

1. Na pásu karet vyberte **vytvořit profil zápisu**.

1. Na stránce **Obecné** v Průvodci vytvořením profilu zápisu zadejte následující informace:

    - **Název**: jedinečný název pro identifikaci profilu

    - **Popis**: volitelné pole, které vám popíše profil.

    - **Autorita pro správu**: jenom **místní výběr**

1. Na stránce **přiřazení lokality** vyberte **kód lokality pro správu** s bodem správy zařízení.

1. Na stránce **Vybrat zprostředkující bod registrace** vyberte **jenom intranet**a pak vyberte jeden nebo víc zprostředkujících bodů registrace. Zařízení bude tyto servery používat ke spuštění procesu registrace.

1. Na stránce **Vybrat důvěryhodný kořenový certifikát** vyberte profil certifikátu, který obsahuje důvěryhodný kořenový certifikát.

1. Na stránce **Profily sítě Wi-Fi** vyberte profil sítě Wi-Fi, který obsahuje potřebná nastavení sítě pro připojení zařízení.

    > [!TIP]
    > Pokud pro registrační balíček nepoužíváte profil sítě Wi-Fi, tento krok přeskočte.

1. Dokončete průvodce.

## <a name="create-an-enrollment-package"></a><a name="bkmk_createPpkg"></a> Vytvoření registračního balíčku

Registrační balíček (ppkg) je soubor, který slouží k hromadné registraci zařízení pro místní správu mobilních zařízení (MDM). Vytvořte tento soubor s Configuration Manager. I když můžete vytvořit podobné typy balíčků s Windows ICD, k registraci zařízení pro místní správu mobilních zařízení (MDM) se dají použít jenom balíčky vytvořené v Configuration Manager. Balíček, který vytvoříte pomocí programu Windows ICD, může zadat jenom hlavní název uživatele (UPN), který je potřebný pro registraci, nemůže spustit samotný proces registrace.

Proces vytvoření registračního balíčku vyžaduje sadu Windows ADK (Windows Assessment and Deployment Toolkit) pro Windows 10. Na počítači, na kterém je spuštěná konzola Configuration Manager, nainstalujte nejnovější verzi sady Windows ADK. Vyberte funkci **Imaging and Configuration Designer (ICD)** a všechny závislosti. (Tato verze nemusí odpovídat verzi používané pro nasazení operačního systému pomocí Configuration Manager lokality.) Další informace najdete v tématu [Stažení sady Windows ADK pro Windows 10](/windows-hardware/get-started/adk-install).

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte **všechna zařízení vlastněná společností**, rozbalte **Windows**a vyberte uzel **registrační profily** .

1. Vyberte existující profil zápisu. Na pásu karet vyberte **exportovat**.

1. V okně Exportovat registrační balíček zadejte následující informace:

    - **Doba platnosti (dny)**: ve výchozím nastavení Configuration Manager nastaví vypršení platnosti registračního balíčku za dva týdny (14 dní). Po vypršení platnosti tohoto balíčku nemůžete použít balíček pro registraci zařízení. Zadejte celé číslo od 1 do 30.

    - **Soubor balíčku**: zadejte cestu k místnímu nebo síťovému souboru a název souboru. ppkg.

    - **Šifrovat balíček**: tuto možnost povolte, pokud chcete balíček chránit heslem. Po exportu balíčku Configuration Manager zobrazí vygenerované heslo. Zkopírujte heslo a uložte ho na bezpečném místě. Nemůžete použít exportovaný registrační balíček bez hesla.

        > [!IMPORTANT]
        > Configuration Manager neuloží heslo a nemůžete ho přizpůsobit ani změnit. Po zavření okna, které zobrazuje heslo, neexistuje způsob, jak heslo načíst.

1. Vyberte **Exportovat**. Configuration Manager k vytvoření registračního balíčku používá Windows ADK.

Configuration Manager sleduje platné registrační balíčky. V konzole rozbalte uzel **registrační profil** a vyberte **exportované balíčky**.

> [!TIP]
> Pokud odeberete registrační balíček z konzoly Configuration Manager, nemůžete ho použít k registraci zařízení. Tuto metodu použijte ke správě registračních balíčků, které nechcete, aby jiní uživatelé používali pro hromadnou registraci.

## <a name="bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a> Hromadné registrace zařízení

Balíček můžete použít k registraci zařízení před nebo po procesu počátečního prostředí (OOBE) zařízení. Registrační balíček může být také součástí zřizovacího balíčku OEM (Original Equipment Manufacturer).

Pokud chcete balíček použít k hromadné registraci, je potřeba ho fyzicky doručit do zařízení. V závislosti na vašich potřebách máte různé metody, například:

- Kopírování ze systému souborů

- Připojit k e-mailu

- Kopírování prostřednictvím připojení NFC (Near Field Communication)

- Kopírování z paměťové karty

- Skenování čárového kódu

- Kopírování z připojeného zařízení

- Zahrnutí do zřizovacího balíčku výrobce OEM

### <a name="enroll-a-device-with-bulk-enrollment-package"></a>Registrace zařízení pomocí balíčku hromadného zápisu

1. V zařízení otevřete soubor. ppkg. V případě potřeby spusťte jako správce.

1. Systém Windows zobrazí dotaz, zda je balíček z důvěryhodného zdroje, vyberte možnost **Ano**.

Spustí se proces registrace.

## <a name="verify-enrollment"></a><a name="bkmk_verifyEnroll"></a> Ověřit registraci

### <a name="verify-bulk-enrollment-on-the-device"></a>Ověření hromadné registrace zařízení

1. V zařízení otevřete **Nastavení**.

1. Vyberte **účty**a vyberte **přístup do práce nebo do školy**. Po úspěšné registraci se pod **companyapps.** zobrazí účet.

1. Vyberte účet a pak vyberte **synchronizovat**. Tato akce spustí správu pomocí Configuration Manager.

### <a name="verify-enrollment-in-the-console"></a>Ověření registrace v konzole

Pomocí konzoly Configuration Manager ověřte, že se zařízení úspěšně zaregistrovala. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** a vyberte možnost **zařízení**. V seznamu zařízení vyhledejte nebo vyhledejte zaregistrované zařízení.