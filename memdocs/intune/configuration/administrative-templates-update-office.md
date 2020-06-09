---
title: Aktualizace Office 365 pomocí šablon pro správu v Microsoft Intune – Azure | Microsoft Docs
description: Pomocí šablon pro správu v nástroji Microsoft Intune aktualizujte aplikace Office 365 na nejnovější verzi a vyberte, jak často sada Office kontroluje aktualizace. Podívejte se na klíče registru zařízení, které se aktualizují při použití zásad Intune pro Office Update.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 72b0ef53f0451314ef121f82524697ddfdc38cd3
ms.sourcegitcommit: 48ec5cdc5898625319aed2893a5aafa402d297fc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/08/2020
ms.locfileid: "84531719"
---
# <a name="use-update-channel-and-target-version-settings-to-update-office-365-with-microsoft-intune-administrative-templates"></a>Pomocí nastavení aktualizace kanálu a cílové verze aktualizujte Office 365 pomocí Microsoft Intune Šablony pro správu

V Intune můžete [ke konfiguraci nastavení zásad skupiny použít šablony Windows 10](administrative-templates-windows.md). V tomto článku se dozvíte, jak aktualizovat Office 365 pomocí šablony pro správu v Intune. Poskytuje taky pokyny k tomu, abyste potvrdili, že se zásady úspěšně použijí. Tyto informace také pomáhají při řešení problémů.

V tomto scénáři vytvoříte v Intune šablonu pro správu, která aktualizuje Office 365 na vašich zařízeních.

Další informace o šablonách pro správu najdete v tématu [šablony Windows 10 pro konfiguraci nastavení zásad skupiny](administrative-templates-windows.md).

Platí pro:

- Windows 10 a novější
- Office 365

## <a name="prerequisites"></a>Požadavky

Nezapomeňte pro aplikace Office [Povolit automatické aktualizace aplikací pro Microsoft 365](https://docs.microsoft.com/deployoffice/configure-update-settings-for-office-365-proplus) . Můžete to provést pomocí zásad skupiny nebo šablony Intune Office 2016 ADMX:

> [!div class="mx-imgBorder"]
> ![V šabloně pro správu Intune nastavte nastavení povolit automatické aktualizace pro Office.](./media/administrative-templates-update-office/admx-enable-automatic-updates.png)

## <a name="set-the-update-channel-in-the-intune-administrative-template"></a>Nastavení kanálu aktualizací v šabloně pro správu Intune

1. V [šabloně pro správu Intune](administrative-templates-windows.md#create-the-template)přejděte na nastavení **kanál aktualizací** a zadejte požadovaný kanál. Například vyberte `Semi-Annual Channel` :

    > [!div class="mx-imgBorder"]
    > ![V šabloně pro správu Intune nastavte nastavení kanálu pro aktualizace pro Office.](./media/administrative-templates-update-office/admx-enable-update-channel-setting.png)

    > [!NOTE]
    > Doporučuje se aktualizovat častěji. Částečně ročně se používá pouze jako příklad.

2. Nezapomeňte [tuto zásadu přiřadit](device-profile-assign.md) k zařízením s Windows 10. Pokud chcete zásady testovat dřív, můžete taky tuto zásadu synchronizovat:

    - [Synchronizace zásad v Intune](../remote-actions/device-sync.md)
    - [Ruční synchronizace zásad na zařízení](https://docs.microsoft.com/mem/intune/user-help/sync-your-device-manually-windows#sync-from-settings-app)

## <a name="check-the-intune-registry-keys"></a>Podívejte se na klíče registru Intune.

Po přiřazení zásad a synchronizace zařízení můžete potvrdit použití zásady:

1. V zařízení otevřete aplikaci **Editor registru** .
2. Přejít na cestu k zásadám Intune: `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\Providers\<Provider ID>\default\Device\office16~Policy~L_MicrosoftOfficemachine~L_Updates` .

    > [!TIP]
    > `<Provider ID>`V klíči registru se změní. Pokud chcete najít ID poskytovatele pro vaše zařízení, otevřete aplikaci **Editor registru** a pokračujte na `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\AdmxInstalled` . Zobrazí se ID zprostředkovatele.

    Při použití zásady se zobrazí následující klíče registru:

    - `L_UpdateBranch`
    - `L_UpdateTargetVersion`

    V následujícím příkladu se zobrazí `L_UpdateBranch` hodnota podobná `<enabled /><data id="L_UpdateBranchID" value="Deferred" />` . Tato hodnota znamená, že je nastavená na půlroční kanál:

    > [!div class="mx-imgBorder"]
    > ![Příklad šablony pro správu L_Updatebranch klíče registru](./media/administrative-templates-update-office/admx-update-branch-registry-key.png)

    > [!TIP]
    > [Spravujte Microsoft 365 aplikace pomocí Configuration Manager](https://docs.microsoft.com/configmgr/sum/deploy-use/manage-office-365-proplus-updates#bkmk_channel) vypíše hodnoty a jejich význam. Hodnoty registru jsou založené na vybraném distribučním kanálu:
    >
    >- Měsíční kanál-hodnota = "aktuální"
    >- Měsíční kanál (cílený) – hodnota = "aktuální"
    >- Půlroční kanál-hodnota = "Current"
    >- Půlroční kanál (cílený)-value = "FirstReleaseDeferred"
    >- Insider Fast-value = "InsiderFast"

V tomto okamžiku se zásady Intune na zařízení úspěšně nastavily.

## <a name="check-the-office-registry-keys"></a>Podívejte se na klíče registru Office.

1. V zařízení otevřete aplikaci **Editor registru** .
2. Přejít na cestu k zásadám Office: `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration` .

    Zobrazí se následující klíče registru:

    - `UpdateChannel`: Dynamický klíč, který se mění v závislosti na nakonfigurovaných nastaveních.
    - `CDNBaseUrl`: Nastaví se, když se na zařízení nainstaluje Office 365.

3. Podívejte se na `UpdateChannel` hodnotu. Hodnota určuje, jak často se Office aktualizuje. [Spravujte Microsoft 365 aplikace pomocí Configuration Manager](https://docs.microsoft.com/configmgr/sum/deploy-use/manage-office-365-proplus-updates#bkmk_channel) zobrazí seznam hodnot a jejich nastavení.

    V následujícím příkladu vidíte `UpdateChannel` , že je nastavena na hodnotu `http://officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60` , která je **měsíčně**:

    > [!div class="mx-imgBorder"]
    > ![Příklad klíče registru UpdateChannel Office šablony pro správu](./media/administrative-templates-update-office/admx-update-channel-office-registry-key.png)

    Tento příklad znamená, že zásady se ještě nepoužily, protože je pořád nastavená na **měsíční**místo **roční**.

Tento klíč registru se aktualizuje, když se spustí **Plánovač úloh**  >  **Automatické aktualizace Office 2,0** nebo když se uživatel přihlásí k zařízení. Pokud to chcete ověřit, otevřete > **triggery**úlohy **automatické aktualizace Office 2,0** . V závislosti na aktivačních událostech může trvat aspoň jeden den, než `UpdateChannel` se aktualizuje klíč registru.

## <a name="force-office-automatic-updates-to-run"></a>Vynutit spuštění automatických aktualizací Office

K otestování zásad můžete na zařízení vynutit nastavení zásad. Následující kroky aktualizují registr. Jako vždy buďte opatrní při aktualizaci registru.

1. Vymažte klíč registru:

    1. Přejděte do části `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Updates` (Soubor > Nový > Jiné).
    2. Poklikejte na `UpdateDetectionLastRunTime` klíč, odstraňte data hodnoty > **OK**.

2. Spusťte úlohu automatické aktualizace Office:

    1. Otevřete **Plánovač úloh** aplikaci na zařízení.
    2. Rozbalte **Plánovač úloh Library**  >  **Microsoft**  >  **Office**.
    3. Vyberte možnost **Automatické aktualizace Office 2,0**  >  **Spustit**:

        > [!div class="mx-imgBorder"]
        > ![Otevření plánu úloh a spuštění automatických aktualizací pro Office](./media/administrative-templates-update-office/admx-task-scheduler-office-automatic-updates.png)

        Počkejte, než se úloha dokončí, což může trvat několik minut.

3. V aplikaci **Editor registru** , přejít na `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration` . Ověřte `UpdateChannel` hodnotu.

    Měla by se aktualizovat hodnotou nastavenou v zásadě. V našem příkladu by měla být hodnota nastavena na `http://officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114` .

V tuto chvíli se kanál aktualizací Office v zařízení úspěšně změnil. Můžete otevřít aplikaci Office 365 pro uživatele, který obdrží tuto aktualizaci, aby zkontroloval stav.

## <a name="force-the-office-synchronization-to-update-account-information"></a>Vynutit aktualizaci informací o účtu v synchronizaci sady Office  

Pokud chcete, můžete vynutit, aby Office získal nejnovější aktualizaci verze. Následující kroky by se měly provádět jenom jako potvrzení, nebo pokud potřebujete, aby zařízení získalo nejnovější aktualizaci verze z tohoto kanálu rychle. V opačném případě Office provede svoji úlohu a automaticky se aktualizuje.

### <a name="step-1-force-the-office-version-to-update"></a>Krok 1: vynutit aktualizaci verze Office

1. Potvrďte, že verze Office podporuje kanál pro aktualizaci, který si zvolíte. [Historie aktualizací pro aplikace Microsoft 365](https://docs.microsoft.com/officeupdates/update-history-office365-proplus-by-date) obsahuje čísla sestavení, která podporují různé kanály aktualizace.

2. V [šabloně pro správu Intune](administrative-templates-windows.md#create-the-template)přejděte na nastavení **cílová verze** a zadejte požadovanou verzi.

    Nastavení **cílové verze** vypadá podobně jako u následujícího nastavení:

    > [!div class="mx-imgBorder"]
    > ![V šabloně pro správu Intune nastavte nastavení cílové verze pro Office.](./media/administrative-templates-update-office/admx-enable-target-version-setting.png)

> [!IMPORTANT]
>
> - Nezapomeňte tuto zásadu přiřadit.
> - Pokud změníte existující zásady, ovlivní vaše změny všechny přiřazené uživatele.
> - Pokud testujete tuto funkci, doporučujeme vytvořit zásadu testování a přiřadit ji k testovací skupině uživatelů.

### <a name="step-2-check-the-office-version"></a>Krok 2: ověření verze Office

Zvažte použití těchto kroků k otestování zásad před nasazením zásad všem uživatelům.

1. V aplikaci **Editor registru** , přejít na`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PolicyManager\Providers\<Provider ID>\default\Device\office16~Policy~L_MicrosoftOfficemachine~L_Updates`

2. Podívejte se na `L_UpdateTargetVersion` hodnotu. Po použití těchto zásad je hodnota nastavena na zadanou verzi, například `<enabled /><data id="L_UpdateTargetVersionID" value="16.0.10730.20344" />` .

    V tomto okamžiku se zásady Intune na zařízení úspěšně nastavily.

3. V dalším kroku můžete vynutit aktualizaci Office. Otevřete aplikaci Office, například Excel. Vyberte možnost aktualizovat nyní (případně v nabídce **účet** ).

    Tato aktualizace trvá několik minut. Můžete potvrdit, že se Office pokusí získat verzi, kterou zadáte:

      1. V zařízení přejít na `C:\Program Files (x86)\Microsoft Office\Updates\Detection\Version` .
      2. Otevřete `VersionDescriptor.xml` soubor a pokračujte v `<Version>` části. Dostupná verze by měla být stejná jako verze, kterou jste zadali v zásadách Intune, například:

          > [!div class="mx-imgBorder"]
          > ![Podívejte se na část verze v souboru XML s popisovačem verzí.](./media/administrative-templates-update-office/office-version-descriptor-xml-example.png)

4. Po instalaci aktualizace by měla aplikace Office zobrazovat novou verzi (například v nabídce **účet** ).

## <a name="next-steps"></a>Další kroky

[Aktualizace hodnot kanálu pro klienty Office 365](https://docs.microsoft.com/configmgr/sum/deploy-use/manage-office-365-proplus-updates#bkmk_channel)

[Přehled služby cloudové zásady Office pro aplikace Microsoft 365](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)

[Pomocí šablon Windows 10 můžete nakonfigurovat nastavení zásad skupiny (šablony ADMX) v Microsoft Intune](administrative-templates-windows.md)
