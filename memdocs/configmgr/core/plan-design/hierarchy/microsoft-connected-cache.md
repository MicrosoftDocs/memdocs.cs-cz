---
title: Microsoft Connected Cache
titleSuffix: Configuration Manager
description: Použití distribučního bodu Configuration Manager jako serveru místní mezipaměti pro optimalizaci doručení
ms.date: 05/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0103ba8923698a31b86e7d34119caaeb54d54c90
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88128524"
---
# <a name="microsoft-connected-cache-in-configuration-manager"></a>Mezipaměť propojená Microsoftem v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

<!--3555764-->

Počínaje verzí 1906 můžete nainstalovat server Microsoft Connected cache do distribučních bodů. Uložením tohoto obsahu do mezipaměti v místním prostředí můžou vaši klienti těžit z funkce Optimalizace doručení, ale můžete přispět k ochraně WAN Links.

> [!NOTE]
> Počínaje verzí 1910 je tato funkce nyní označována jako **propojená s mezipamětí Microsoft**. Dříve byla známá jako Optimalizace doručení v síťové mezipaměti.

Tento server mezipaměti funguje jako transparentní mezipaměť na vyžádání pro obsah stažený optimalizací doručení. Pomocí nastavení klienta se ujistěte, že je tento server nabízen pouze členům místní skupiny hranic Configuration Manager.

Tato mezipaměť je oddělená od obsahu distribučního bodu Configuration Manager. Pokud zvolíte stejnou jednotku jako role distribučního bodu, uloží se obsah samostatně.

> [!Note]  
> Server připojené mezipaměti je aplikace nainstalovaná na Windows serveru. Tato aplikace je stále ve vývoji.

## <a name="how-it-works"></a>Jak to funguje

Když nakonfigurujete klienty tak, aby používali Server připojené mezipaměti, už nepožadují obsah spravovaný přes Microsoft Cloud. Klienti požadují tento obsah ze serveru mezipaměti nainstalovaného v distribučním bodě. Místní server ukládá tento obsah do mezipaměti pomocí funkce služby IIS pro směrování žádostí na aplikace (ARR). Server mezipaměti pak může rychle reagovat na jakékoli budoucí požadavky na stejný obsah. Pokud server připojené mezipaměti není k dispozici nebo obsah ještě není uložen do mezipaměti, klienti stáhnou obsah z Internetu. Klienti také využívají optimalizaci doručování ke stahování částí obsahu od partnerských uzlů v jejich síti.

![Diagram fungování připojené mezipaměti](media/3555764-microsoft-connected-cache.png)

1. Klient zkontroluje aktualizace a získá adresu služby Content Delivery Network (CDN).

2. Configuration Manager nakonfiguruje nastavení optimalizace doručování (DO) na klientovi, včetně názvu serveru mezipaměti.

3. Klient A požaduje obsah ze serveru do mezipaměti.

4. Pokud mezipaměť neobsahuje obsah, pak ho Server do mezipaměti načte z CDN.

5. Pokud server mezipaměti přestane reagovat, stáhne obsah z CDN.

6. Klienti používají k získání částí obsahu od partnerských uzlů.

## <a name="prerequisites-and-limitations"></a>Požadavky a omezení

- *Místní* distribuční bod s následujícími konfiguracemi:

  - Systémy Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 nebo Windows Server 2019

  - Výchozí web povolený na portu 80

  - Neinstalujte funkci [směrování požadavků aplikace](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) IIS (ARR). Připojená mezipaměť nainstaluje ARR a nakonfiguruje její nastavení. Společnost Microsoft nemůže zaručit, že konfigurace ARR v mezipaměti není v konfliktu s jinými aplikacemi na serveru, které tuto funkci využívají i.

  - Distribuční bod vyžaduje internetový přístup ke cloudu Microsoftu. Konkrétní adresy URL se můžou lišit v závislosti na konkrétním obsahu s povoleným cloudem. Ujistěte se také, že jste povolili koncové body pro optimalizaci doručení. Další informace najdete v tématu [požadavky na přístup k Internetu](../network/internet-endpoints.md).

  - Od verze 2002 může aplikace připojené mezipaměti používat neověřené proxy server pro přístup k Internetu. Další informace najdete v tématu [konfigurace proxy serveru pro server systému lokality](../network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server).<!-- 5856396 -->

- Klienti se systémem Windows 10 verze 1709 nebo novější

## <a name="enable-connected-cache"></a>Povolit připojenou mezipaměť

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** a vyberte uzel **distribuční body** .

1. Vyberte místní *distribuční bod a pak na pásu* karet vyberte **vlastnosti**.

1. Ve vlastnostech role distribučního bodu na kartě **Obecné** nakonfigurujte následující nastavení:  

    1. Povolte možnost **Povolit tento distribuční bod, který se použije jako server s připojenou mezipamětí společnosti Microsoft** .  

        Zobrazte a přijměte licenční podmínky.

    2. **Místní jednotka, která se má použít**: Vyberte disk, který chcete použít pro mezipaměť. **Automaticky** je výchozí hodnota, která používá disk s největším množstvím volného místa. <sup> [Poznámka 1](#bkmk_note1)</sup>  

        > [!Note]  
        > Tuto jednotku můžete později změnit. Veškerý obsah uložený v mezipaměti je ztracen, pokud jej nezkopírujete do nové jednotky.

    3. **Místo na disku**: vyberte velikost místa na disku, které se má rezervovat v GB, nebo procento celkového místa na disku. Ve výchozím nastavení je tato hodnota 100 GB.

        > [!Note]  
        > Výchozí velikost mezipaměti by měla být pro většinu zákazníků dostačující. Velikost mezipaměti můžete upravit později.
        >
        > Pokud velikost mezipaměti na disku překročí přidělené místo, služba ARR vymaže místo odebráním obsahu na základě vestavěných heuristik.<!-- SCCMDocs#2045 -->

    4. **Při zakázání serveru připojené mezipaměti zachovat mezipaměť**: Pokud server mezipaměti odeberete a povolíte tuto možnost, server zachová obsah mezipaměti na disku.  

1. V nastavení klienta ve skupině **optimalizace doručování** nakonfigurujte nastavení tak, aby **povolovalo zařízením spravovaným nástrojem Configuration Manager používat servery mezipaměti připojené od Microsoftu k stažení obsahu**.  

### <a name="note-1-about-drive-selection"></a><a name="bkmk_note1"></a>Poznámka 1: o výběru jednotky

Pokud vyberete možnost **automaticky**, když Configuration Manager nainstaluje součást připojené mezipaměti, bude dodržet soubor **NO_SMS_ON_DRIVE. SMS** . Například distribuční bod má soubor `C:\no_sms_on_drive.sms` . I když má jednotka C: nejvíce volného místa, Configuration Manager konfiguruje připojenou mezipaměť pro použití jiné jednotky pro svou mezipaměť.

Pokud vyberete konkrétní jednotku, která již obsahuje soubor **NO_SMS_ON_DRIVE. SMS** , Configuration Manager soubor ignoruje. Konfigurace připojené mezipaměti pro použití této jednotky je explicitní záměr. Například distribuční bod má soubor `F:\no_sms_on_drive.sms` . Když explicitně nakonfigurujete vlastnosti distribučního bodu tak, aby používaly jednotku **f:** , Configuration Manager nakonfiguruje připojenou mezipaměť tak, aby používala jednotku f: pro svou mezipaměť.

Změna jednotky po instalaci připojené mezipaměti:

- Ručně nakonfigurujte vlastnosti distribučního bodu tak, aby používaly konkrétní písmeno jednotky.

- Pokud je nastavena na hodnotu automaticky, vytvořte nejprve soubor **NO_SMS_ON_DRIVE. SMS** . Pak proveďte nějaké změny vlastností distribučního bodu, aby se aktivovala Změna konfigurace.

### <a name="automation"></a>Automation

<!-- SCCMDocs#1911 -->

Sadu Configuration Manager SDK můžete použít k automatizaci konfigurace nastavení mezipaměti propojeného Microsoftem v distribučním bodě. Stejně jako u všech rolí lokality použijte [SMS_SCI_SysResUse třídy WMI](../../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md). Další informace najdete v tématu [programování rolí lokality](../../../develop/osd/about-operating-system-deployment-site-role-configuration.md#programming-the-site-roles).

Když aktualizujete instanci **SMS_SCI_SysResUse** pro distribuční bod, nastavte následující vlastnosti:

- **AgreeDOINCLicense**: Pokud chcete `1` přijmout licenční podmínky, nastavte na.
- **Příznaky**: Povolit `|= 4` , zakázat`&= ~4`
- **DiskSpaceDOINC**: nastavte na `Percentage` nebo`GB`
- **RetainDOINCCache**: nastavte na `0` nebo`1`
- **LocalDriveDOINC**: nastavte na `Automatic` nebo konkrétní písmeno jednotky, například `C:` nebo.`D:`

## <a name="verify"></a>Ověření

Když klienti stáhnou obsah spravovaný přes Cloud, využívají optimalizaci doručování ze serveru mezipaměti nainstalovaného v distribučním bodě. Obsah spravovaný přes Cloud zahrnuje následující typy:

- Aplikace pro Microsoft Store
- Funkce Windows na vyžádání, jako jsou například jazyky
- Pokud povolíte [zásady web Windows Update pro firmy](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md): aktualizace funkcí a kvality Windows 10
- Pro [úlohy spolusprávy](../../../comanage/workloads.md):
  - Web Windows Update pro firmy: aktualizace funkcí a kvality Windows 10
  - Aplikace pro Office Klikni a spusť: Microsoft 365 aplikace a aktualizace
  - Klientské aplikace: Microsoft Store aplikace a aktualizace
  - Endpoint Protection: aktualizace definic v programu Windows Defender

Ve Windows 10 verze 1809 nebo novější ověřte toto chování pomocí rutiny **Get-DeliveryOptimizationStatus** prostředí Windows PowerShell. Ve výstupu rutiny si prohlédněte hodnotu **BytesFromCacheServer** . Další informace najdete v tématu věnovaném [monitorování Optimalizace doručení](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization).

Pokud server mezipaměti vrátí jakoukoli chybu protokolu HTTP, klient Optimalizace doručení se vrátí k původnímu cloudovém zdroji.

Podrobnější informace najdete v tématu [řešení potíží s propojenou mezipamětí Microsoft v Configuration Manager](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md).

## <a name="support-for-intune-win32-apps"></a><a name="bkmk_intune"></a>Podpora pro aplikace Win32 Intune

<!--5032900-->

Pokud v Configuration Manager distribučních bodech povolíte připojenou mezipaměť, počínaje verzí 1910, mohou aplikace Microsoft Intune Win32 sloužit spoluspravovaným klientům.

### <a name="prerequisites"></a>Požadavky

#### <a name="client"></a>Klient

- Aktualizujte klienta na nejnovější verzi.

- Klientské zařízení musí mít aspoň 4 GB paměti.

    > [!TIP]
    > Použijte následující nastavení zásad skupiny: Konfigurace počítače > Šablony pro správu > součásti systému Windows > optimalizaci doručení > **Minimální kapacita paměti RAM (včetně), která je nutná k povolení použití ukládání do sdílené mezipaměti (v GB)**.

#### <a name="site"></a>Web

- Povolí připojenou mezipaměť v distribučním bodě. Další informace najdete v tématu [mezipaměť Microsoft připojené k síti](microsoft-connected-cache.md).

- Klient a připojený distribuční bod s povolenou mezipamětí musí být ve stejné skupině hranic.

- Ve skupině pro [**optimalizaci doručení**](../../clients/deploy/about-client-settings.md#delivery-optimization) Povolte následující nastavení klienta:

  - **Pro ID skupiny pro optimalizaci doručení použijte Configuration Manager skupiny hranic.**
  - **Povolit zařízením spravovaným pomocí Správce konfigurace používat servery mezipaměti připojené od Microsoftu k stažení obsahu**

- Povolte klientské aplikace funkce předběžné verze **pro spoluspravovaná zařízení**. Další informace najdete v tématu [předběžné verze funkcí](../../servers/manage/pre-release-features.md).

- Povolte spolusprávu a přepněte úlohu **klientské aplikace** na **pilotní nasazení Intune** nebo **Intune**. Další informace najdete v následujících článcích:

  - [Úlohy – klientské aplikace](../../../comanage/workloads.md#client-apps)
  - [Jak povolit spolusprávu](../../../comanage/how-to-enable.md)
  - [Přepnutí úloh do Intune](../../../comanage/how-to-switch-workloads.md)

    Pokud jste v pilotním projektu, přidejte klienta do pilotní kolekce pro klientské aplikace.

#### <a name="intune"></a>Intune

- Tato funkce podporuje jenom typ aplikace Win32 v Intune.

  - Vytvořte a přiřaďte (nasaďte) novou aplikaci v Intune pro tento účel. (Aplikace vytvořené před Intune verze 1811 nefungují.) Další informace najdete v tématu [Správa aplikací Win32 v Intune](https://docs.microsoft.com/intune/apps/apps-win32-app-management).

  - Aplikace musí mít velikost alespoň 100 MB.
  
    > [!TIP]
    > Použijte následující nastavení zásad skupiny: Konfigurace počítače > Šablony pro správu > součásti systému Windows > Optimalizace doručení > **minimální velikost souboru obsahu sdílené mezipaměti (v MB)**.

## <a name="see-also"></a>Viz také

[Optimalizace aktualizací Windows 10 s optimalizací doručení](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)

[Řešení potíží s propojenou mezipamětí Microsoft v Configuration Manager](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)
