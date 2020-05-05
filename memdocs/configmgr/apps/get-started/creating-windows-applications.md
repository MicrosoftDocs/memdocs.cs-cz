---
title: Vytváření aplikací pro Windows
titleSuffix: Configuration Manager
description: Přečtěte si další informace o vytváření a nasazování aplikací pro Windows v Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3af6f2883ebf17ab19f57762b8b3bf26e3716262
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075723"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Vytváření aplikací pro Windows v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Kromě dalších Configuration Manager požadavků a postupů pro [vytváření aplikací](../deploy-use/create-applications.md)Vezměte v úvahu při vytváření a nasazování aplikací pro zařízení s Windows taky následující skutečnosti.  

## <a name="general-considerations"></a><a name="bkmk_general"></a>Obecné požadavky  

Configuration Manager podporuje nasazování formátů balíčku aplikace systému Windows (. appx) a sady prostředků aplikace (. appxbundle) pro Windows 8.1 a zařízení s Windows 10.

Když vytváříte aplikaci v konzole Configuration Manager, vyberte **typ** instalačního souboru aplikace jako **\*balíček aplikace systému Windows (. appx, \*. appxbundle, \*. msix, \*. msixbundle)**. Další informace o tom, jak vytvářet aplikace obecně, najdete v tématu věnovaném [vytváření aplikací](../deploy-use/create-applications.md). Další informace o formátu MSIX najdete v tématu [Podpora formátu MSIX](#bkmk_msix).

> [!Note]  
> Pokud chcete využívat nové funkce Configuration Manager, nejdřív aktualizujte klienty na nejnovější verzi. I když se nové funkce zobrazí v konzole Configuration Manager, když aktualizujete lokalitu a konzolu, kompletní scénář nebude funkční, dokud nebude verze klienta zároveň nejnovější.<!--SCCMDocs issue 646-->  

## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a><a name="bkmk_provision"></a>Zřídit balíčky aplikací pro Windows pro všechny uživatele na zařízení
<!--1358310-->
Zřídit aplikaci s balíčkem aplikace pro Windows pro všechny uživatele v zařízení. Jedním z běžných příkladů tohoto scénáře je zřízení aplikace od Microsoft Store pro firmy a vzdělávání, jako je Minecraftu: školství Edition, pro všechna zařízení používaná studenty ve škole. Dřív Configuration Manager podporuje jenom instalaci těchto aplikací na uživatele. Po přihlášení k novému zařízení musí student čekat na přístup k aplikaci. Když teď aplikaci zřídíte pro všechny uživatele, můžou se rychleji zvýšit.

> [!Important]  
> Buďte opatrní při instalaci, zřizování a aktualizaci různých verzí stejného balíčku aplikace pro Windows na zařízení, což může vést k neočekávaným výsledkům. K tomuto chování může dojít při použití Configuration Manager k zřízení aplikace, ale pak uživatelům umožnit aktualizaci aplikace z Microsoft Store. Další informace najdete v pokynech k dalšímu kroku při [správě aplikací z Microsoft Store pro firmy](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps).  

Při zřizování offline licencované aplikace Configuration Manager Nedovolí, aby ho Windows automaticky aktualizoval z Microsoft Store.  

Configuration Manager podporuje zřizování aplikací ve všech podporovaných verzích Windows 10.<!--SCCMDocs-pr issue 2762-->

<!--
- Install action: Windows 10, version 1607 and later
- Uninstall action: Windows 10, version 1703 and later
-->

Chcete-li pro tuto funkci nakonfigurovat typ nasazení aplikace pro systém Windows, povolte možnost **zřízení této aplikace pro všechny uživatele v zařízení**. Další informace najdete v tématu věnovaném [vytváření aplikací](../deploy-use/create-applications.md).

> [!Note]  
> Pokud potřebujete odinstalovat zřízenou aplikaci ze zařízení, ke kterým se uživatelé už přihlásili, musíte vytvořit dvě odinstalační nasazení. Zaměřte se na první nasazení odinstalace do kolekce zařízení, která obsahuje zařízení. Zajistěte druhé odinstalaci nasazení na kolekci uživatelů, která obsahuje uživatele, kteří se už přihlásili k zařízením s zřízenou aplikací. Při odinstalaci zřízené aplikace na zařízení Windows v tuto chvíli neprovádí odinstalaci této aplikace pro uživatele.

## <a name="support-for-msix-format"></a><a name="bkmk_msix"></a>Podpora formátu MSIX
<!--1357427-->

Configuration Manager podporuje balíčky aplikací pro Windows 10 (. msix) a sady prostředků aplikace (. msixbundle). Windows 10 verze 1809 nebo novější tyto formáty podporují.

- Přehled MSIX najdete v tématu o tom, jak se [podíváte na MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).  

- Informace o tom, jak vytvořit novou aplikaci MSIX, najdete [v článku podpora MSIX představená v programu Insider build 17682](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  

### <a name="convert-applications-to-msix"></a>Převést aplikace na MSIX
<!--3607729, fka 1359029-->

Převeďte stávající aplikace Instalační služba systému Windows (. msi) na formát MSIX.

#### <a name="prerequisites-for-msix"></a>Předpoklady pro MSIX

- Referenční zařízení s Windows 10 verze 1809 nebo novější  

- Přihlaste se k Windows na tomto zařízení jako uživatel s právy místního správce.  

- Na toto zařízení nainstalujte tyto aplikace:  

  - Konzola nástroje Configuration Manager  

  - Instalace nástroje pro vytváření [balíčků MSIX](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) z Microsoft Store  

  - Instalace [ovladače nástroje pro vytváření balíčků MSIX](/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers)<!--SCCMDocs-pr issue #3091-->  

Na toto zařízení neinstalujte žádné další aplikace ani služby. Je to váš referenční systém.

#### <a name="process-to-convert-applications-to-msix-format"></a>Postup převodu aplikací na formát MSIX

1. Zvyšte úroveň konzoly Configuration Manager, v pracovním prostoru **softwarová knihovna** rozbalte položku **Správa aplikací**a vyberte uzel **aplikace** .  

2. Vyberte aplikaci, která má typ nasazení Instalační služba systému Windows (. msi).  

    > [!Note]  
    > Musíte být schopni získat přístup ke zdrojovému obsahu aplikace z referenčního zařízení.  
    >
    > Název aplikace nemůže obsahovat žádné speciální znaky. Configuration Manager používá název aplikace jako název výstupního souboru.  
    >
    > Tuto aplikaci do referenčního zařízení neinstalujte předem.  

3. Vyberte **převést na. MSIX** na pásu karet.

Po dokončení Průvodce vytvoří nástroj pro vytváření balíčků MSIX soubor MSIX v umístění, které jste zadali v průvodci. Během tohoto procesu Configuration Manager v případě tiché instalace aplikace do referenčního zařízení.

Pokud se proces nezdařil, stránka souhrnu odkazuje na soubor protokolu s více informacemi. Pokud dojde k chybě při zachytávání stavu uživatele, odhlaste se z Windows. Tento problém může vyřešit opětovné přihlášení.

Pokud chcete tuto aplikaci MSIX použít, musíte ji nejdřív digitálně podepsat, aby ji klienti důvěřovali. Další informace o tomto procesu najdete v následujících článcích:

- [MSIX – Nástroj pro balení MSIX – podepsání balíčku MSIX](https://blogs.msdn.microsoft.com/sgern/2018/09/06/msix-the-msix-packaging-tool-signing-the-msix-package/)
- [Jak podepsat balíček aplikace pomocí SignTool](https://docs.microsoft.com/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

Po podepsání aplikace vytvořte v aplikaci Configuration Manager nový typ nasazení. Další informace najdete v tématu [Vytvoření typů nasazení pro aplikaci](../deploy-use/create-applications.md#bkmk_create-dt).

## <a name="task-sequence-deployment-type"></a><a name="bkmk_tsdt"></a>Typ nasazení pořadí úloh

<!--3555953-->

> [!Note]  
> V této verzi Configuration Manager je typ nasazení pořadí úloh předběžná verze funkce. Pokud ho chcete povolit, přečtěte si téma [předběžné verze funkcí](../../core/servers/manage/pre-release-features.md).  

Počínaje verzí 2002 můžete komplexní aplikace nainstalovat pomocí pořadí úkolů prostřednictvím aplikačního modelu. Pokud chcete aplikaci nainstalovat nebo odinstalovat, přidejte do aplikace typ nasazení pořadí úloh. Tento typ nasazení poskytuje následující chování:

<!-- - Deploy an app task sequence to a user collection -->

- Zobrazí pořadí úkolů aplikace s ikonou v centru softwaru. Ikona usnadňuje uživatelům hledání a identifikaci pořadí úkolů aplikace.

- Definujte další metadata pro pořadí úkolů aplikace, včetně lokalizovaných informací.

V aplikaci můžete přidat pořadí úloh nasazení mimo OS jako typ nasazení. Pořadí úkolů s vysokým dopadem na nasazení operačního systému nebo upgrade operačního systému se nepodporuje. <!--A user-targeted deployment still runs in the user context of the local System account.-->

Když přidáte tento typ nasazení do aplikace, nakonfigurujte jeho vlastnosti na stránce **pořadí úkolů** . Další informace najdete v tématu [Možnosti pro typ nasazení **pořadí úkolů** ](../deploy-use/create-applications.md#bkmk_dt-ts).

### <a name="prerequisites-for-a-task-sequence-deployment-type"></a>Předpoklady pro typ nasazení pořadí úloh

Vytvoření vlastního pořadí úloh:

- Používejte jenom kroky nasazení, které nepatří do operačního systému, například **nainstalujte balíček**, **Spusťte příkazový řádek**nebo **Spusťte skript prostředí PowerShell**. Další informace, včetně úplného seznamu podporovaných kroků, najdete v tématu [Vytvoření pořadí úkolů pro nasazení bez OS](../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md).

- Na kartě Vlastnosti pořadí úloh, **oznámení uživateli** nevybírejte možnost pro pořadí úkolů s vysokým dopadem.

<!-- - If you use the **Install Application** step in the task sequence, don't add an app to that step that has a task sequence deployment type. -->

Když vytváříte aplikaci, chcete-li přidat typ nasazení pořadí úloh, váš uživatelský účet potřebuje oprávnění ke čtení pořadí úkolů.<!-- 6348976 --> Ke konfiguraci těchto oprávnění použijte jednu z následujících možností:

- Přidejte uživatelský účet správce aplikace do předdefinované role **analytika jen pro čtení** . Tato role umožňuje zobrazení všech objektů Configuration Manager.

- Zkopírováním předdefinované role **Správce aplikací** vytvořte vlastní roli. Přidejte do objektu **balíčku pořadí úloh** oprávnění **ke čtení** .

### <a name="known-issues-for-a-task-sequence-deployment-type"></a>Známé problémy typu nasazení pořadí úloh

- Pořadí úloh aplikace se ještě nedá nasadit do kolekce uživatelů.

- Nepoužívejte krok **instalovat aplikaci** v tomto pořadí úkolů. K instalaci aplikací použijte krok [instalovat balíček](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) .

## <a name="support-for-universal-windows-platform-uwp-apps"></a><a name="bkmk_uwp"></a>Podpora aplikací Univerzální platforma Windows (UWP)  

Zařízení s Windows 10 nevyžadují k instalaci obchodních aplikací klíč pro zkušební načtení. Pokud ale chcete povolit zkušební načtení ve Windows, musí mít `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` klíč registru hodnotu **1**.  

Pokud tento klíč registru nenakonfigurujete, Configuration Manager při prvním nasazení aplikace do zařízení automaticky nastaví hodnotu **1** . Pokud jste tuto hodnotu nastavili na **0**, Configuration Manager nemůže automaticky změnit hodnotu a nasazení podnikové aplikace se nepodaří.  

Digitálně podepisuje obchodní aplikace UWP. Použijte certifikát pro podpis kódu, který je důvěryhodný pro každé zařízení, do kterého nasazujete aplikaci. Použijte certifikáty z PKI vaší organizace nebo si kupte certifikát od poskytovatele třetí strany, jehož veřejný kořenový certifikát už je důvěryhodný pro Windows.  

Chcete-li podepisovat balíčky mobilních aplikací, použijte následující tabulku k určení typu certifikátu pro podpis kódu, který se má použít:

| Balíček  | Symantec  | Jiné než Symantec  |
|---------|---------|---------|
| Balíčky Universal **. appx** na zařízeních s Windows 10 Mobile | Ano | Ano |
| balíčky **. xap** | Ano | Ne |
| balíčky **. appx** sestavené pro Windows Phone 8,1 pro instalaci na zařízeních s Windows 10 Mobile | Ano | Ne |

## <a name="deploy-windows-installer-apps-to-mdm-enrolled-windows-10-devices"></a><a name="bkmk_mdm-msi"></a>Nasazení aplikací Instalační služba systému Windows do zařízení s Windows 10 zaregistrovaných v MDM  

Typ nasazení **Instalační služba systému Windows až MDM\*(. msi)** umožňuje vytvářet a nasazovat aplikace založené na instalační služba systému Windows na zařízeních zaregistrovaných v MDM s Windows 10.  

Při použití tohoto typu nasazení Vezměte v úvahu následující body:

- Nahrajte jenom jeden soubor s příponou MSI.  

- Configuration Manager používá kód produktu a verzi produktu v souboru pro detekci aplikací.  

- Systém Windows používá výchozí chování aplikace při restartování. Configuration Manager neřídí chování při restartování aplikace.  

- Balíčky MSI na uživatele se nainstalují pro jednoho uživatele.  

- Balíčky MSI vázané na počítač se nainstalují pro všechny uživatele zařízení.  

- Configuration Manager podporuje aktualizace aplikací. Kód produktu MSI každé verze se musí shodovat.  
