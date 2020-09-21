---
title: Použití analýzy zásad skupiny pro import objektů zásad skupiny v Microsoft Intune – Azure | Microsoft Docs
description: Importujte a analyzujte objekty zásad skupiny v Microsoft Intune a ve Správci koncových bodů. Podívejte se na zásady, které mají v cloudu stejné nastavení poskytovatele konfiguračních služeb (CSP), a přiřaďte je uživatelům a zařízením s Windows 10.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 09d54a942bdd745cebd0a2c16dd77f74f0e718e7
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/19/2020
ms.locfileid: "90816610"
---
# <a name="analyze-your-on-premises-group-policy-objects-gpo-using-group-policy-analytics-in-microsoft-endpoint-manager---preview"></a>Analýza místních objektů zásad skupiny (GPO) pomocí analýzy Zásady skupiny ve službě Microsoft Endpoint Manager – Preview

Objekty zásad skupiny (GPO) se používají místně ke konfiguraci nastavení na osobních počítačích a dalších místních zařízeních. V části Správa zařízení můžou objekty zásad skupiny pomáhat s řízením zabezpečení a funkcí v operačních systémech Windows, Internet Exploreru, aplikacích Office a dalších.

Mnoho organizací si hledá cloudová řešení, aby podporovala rostoucí vzdálenou pracovní síly. **Zásady skupiny Analytics** je nástroj a funkce ve službě Microsoft Endpoint Manager, která analyzuje vaše místní objekty zásad skupiny. Pomůže vám určit, jak se objekty zásad skupiny převádějí v cloudu. Výstup ukazuje, která nastavení jsou podporovaná pro poskytovatele MDM, včetně Microsoft Intune. Zobrazuje také všechna zastaralá nastavení nebo nastavení, která nejsou k dispozici pro poskytovatele MDM.

Pokud vaše organizace používá objekty zásad skupiny a chcete přesunout některé úlohy do služby Microsoft Endpoint Manager a Intune, Zásady skupiny Analytics vám pomůže.

Tato funkce platí pro:

- Windows 10 a novější

V tomto článku se dozvíte, jak exportovat objekty zásad skupiny, jak je importovat do správce koncových bodů, a Prohlédněte si analýzu a výsledky.

## <a name="export-gpos-as-an-xml-file"></a>Export objektů zásad skupiny jako souboru XML

1. V místním počítači otevřete `Group Policy Management` aplikaci (GPMC. msc).
2. Rozbalením domény zobrazíte všechny objekty zásad skupiny.
3. Klikněte pravým tlačítkem na libovolný objekt zásad skupiny > **Uložit sestavu**:

    :::image type="content" source="./media/group-policy-analytics/sample-group-policy-object-save-report.png" alt-text="Otevřete Zásady skupiny Management a uložte objekt zásad skupiny jako sestavu souboru XML.":::

4. Uložte soubor do snadno přístupné složky a uložte ho jako soubor XML. Tento soubor přidáte ve Správci koncových bodů.

Ujistěte se, že soubor je menší než 4 MB. Pokud je větší než 4 MB, při uložení sestavy uveďte méně objektů zásad skupiny.

## <a name="use-group-policy-analytics"></a>Použití Zásady skupiny Analytics

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **zařízení**  >  **Zásady skupiny Analytics (Preview)**.
2. Vyberte **importovat**a potom vyberte uložený soubor XML. Když vyberete soubor XML, Intune automaticky analyzuje objekt zásad skupiny v souboru XML.

    Ověřte velikosti individuálních souborů XML objektů zásad skupiny. Jeden objekt zásad skupiny nemůže být větší než 1 MB. Pokud je jeden objekt zásad skupiny větší než 1 MB, import se nezdaří.

3. Po spuštění analýzy se importovaný objekt GPO zobrazí s následujícími informacemi:

    - **Zásady skupiny název**: název se automaticky vygeneruje pomocí informací v objektu zásad skupiny.
    - **Cíl služby Active Directory**: cíl je automaticky vygenerován pomocí informací o cíli organizační jednotky (OU) v objektu zásad skupiny.
    - **Podpora MDM**: zobrazuje procentuální hodnotu nastavení zásad skupiny v objektu zásad skupiny, která má stejné nastavení v Intune.
    - **Cílená na službu AD**: **Ano** znamená, že objekt zásad skupiny je propojený s organizační jednotkou v místních zásadách skupiny. **Ne** znamená, že objekt zásad skupiny není propojený s místní organizační jednotkou.
    - **Poslední import**: zobrazuje datum posledního importu.

    Můžete **importovat** více objektů zásad skupiny pro účely analýzy, **aktualizovat** stránku a **vyfiltrovat** výstup. Toto zobrazení můžete také **exportovat** do `.csv` souboru:

    :::image type="content" source="./media/group-policy-analytics/import-refresh-filter-options.png" alt-text="Import, aktualizace, filtrování nebo Export objektu zásad skupiny (GPO) do souboru CSV v Microsoft Intune a centru pro správu Správce koncových bodů.":::

4. Vyberte procento **podpory MDM** pro uvedený objekt zásad skupiny. Zobrazí se podrobnější informace o objektu zásad skupiny:

    - **Název nastavení**: název se automaticky vygeneruje pomocí informací v nastavení objektu zásad skupiny.
    - **Zásady skupiny kategorie nastavení**: Zobrazuje kategorii nastavení pro nastavení ADMX, například Internet Explorer a Microsoft Edge. Ne všechna nastavení mají kategorii nastavení.
    - **Podpora ADMX**: **Ano** znamená, že pro toto nastavení je k dispozici šablona ADMX. **Ne** znamená, že pro konkrétní nastavení není k dispozici šablona ADMX.

      Další informace o šablonách ADMX najdete [v tématu šablony pro správu v Microsoft Intune](administrative-templates-windows.md).

    - **Podpora MDM**: **Ano** znamená, že ve Správci koncových bodů je dostupné stejné nastavení. Toto nastavení můžete nakonfigurovat v profilu konfigurace zařízení. Nastavení v konfiguračních profilech zařízení jsou namapovaná na zprostředkovatele CSP v systému Windows.

      **Ne** znamená, že nejsou k dispozici žádná shodná nastavení pro poskytovatele MDM, včetně Intune.

      Další informace o profilech konfigurace zařízení najdete v tématu [použití funkcí a nastavení v zařízeních pomocí profilů zařízení](device-profiles.md).      

    - **Hodnota**: zobrazuje hodnotu importovanou z objektu zásad skupiny. Zobrazuje různé hodnoty, jako například,,, `true` `900` `Enabled` `false` a tak dále.
    - **Scope**: ukazuje, jestli importovaný objekt zásad skupiny cílí na zařízení uživatelů nebo cílů.
    - **Minimální verze operačního**systému: zobrazuje minimální čísla sestavení verze operačního systému Windows, která platí pro nastavení objektu zásad skupiny. Může se zobrazit `18362` (1903), `17130` (1803) a další verze Windows 10.

      Například pokud nastavení zásady zobrazí `18362` , pak nastavení podporuje sestavení `18362` a novější sestavení.

    - **Název CSP**: poskytovatel konfiguračních služeb (CSP) zveřejňuje nastavení konfigurace zařízení ve Windows 10. V tomto sloupci se zobrazuje zprostředkovatel CSP, který obsahuje nastavení. Můžete například zobrazit zásady, BitLocker, PassportforWork a tak dále.

      Další informace o CSP najdete v [referenčních](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference)informacích k CSP.

    - **Mapování CSP**: zobrazuje cestu OMA-URI pro místní zásady. OMA-URI můžete použít ve [vlastním profilu konfigurace zařízení](custom-settings-configure.md). Může se například zobrazit `./Device/Vendor/MSFT/BitLocker/RequireDeviceEnryption` .

## <a name="supported-csps"></a>Podporovaná CSP

Zásady skupiny Analytics může analyzovat následující zprostředkovatele CSP:

- [Zprostředkovatel CSP pro zásady](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider)
- [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp)
- [CSP nástroje BitLocker](https://docs.microsoft.com/windows/client-management/mdm/bitlocker-csp)
- [Zprostředkovatel CSP brány firewall](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp)
- [CSP pro AppLocker](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)

## <a name="group-policy-migration-readiness-report"></a>Zásady skupiny sestava připravenosti na migraci

1. V [centru pro správu Microsoft Endpoint Manageru](https://go.microsoft.com/fwlink/?linkid=2109431)vyberte **sestavy**  >  **Analýza zásad skupiny (Preview)**:

    :::image type="content" source="./media/group-policy-analytics/policy-analytics-reports.png" alt-text="Projděte si sestavu a výstup importovaných objektů zásad skupiny pomocí Zásady skupiny Analytics v centru pro správu v Microsoft Intune a v portálu Endpoint Manager.":::

2. Na kartě **Souhrn** se zobrazí souhrn objektu zásad skupiny a jeho zásad. Pomocí těchto informací můžete určit stav zásad v objektu zásad skupiny:

    - **Připraveno k migraci**: zásady mají v Intune stejné nastavení a je připravené k migraci do Intune.
    - **Nepodporováno**: zásada nemá vyhovující nastavení. Nastavení zásad, která zobrazují tento stav, se obvykle nezveřejňují pro poskytovatele MDM, včetně Intune.
    - **Zastaralé**: zásada se může vztahovat na starší verze Windows a už se nepoužívá ve Windows 10 a novějších verzích.

3. Vyberte kartu **sestavy** > **připravenosti na migraci zásad skupiny**. V této sestavě můžete:

    - Podívejte se na počet nastavení v objektu zásad skupiny, která jsou k dispozici v profilu konfigurace zařízení, pokud se mohou nacházet ve vlastním profilu, nejsou podporovány nebo jsou zastaralé.
    - Vyfiltrujte výstup sestavy pomocí **připravenosti migrace**, **typu profilu**a filtru **názvů CSP** .
    - Chcete-li získat aktuální data, vyberte možnost **Generovat sestavu** nebo **vytvořit znovu** .
    - Podívejte se na seznam nastavení v objektu zásad skupiny.
    - K vyhledání konkrétního nastavení použijte panel hledání.
    - Získá časové razítko, kdy se sestava naposledy vygenerovala. 
    
    > [!NOTE]
    > Po přidání nebo odebrání importovaných objektů zásad skupiny může trvat přibližně 20 minut, než se aktualizují data vytváření sestav připravení migrace.

## <a name="privacy-and-security"></a>Ochrana osobních údajů a zabezpečení

Veškerá použití zákaznických dat, jako jsou například objekty zásad skupiny používané ve vaší organizaci, je agregované. Není prodávaný žádné třetí straně. Tato data se můžou použít k rozhodování v obchodních rozhodnutích v rámci Microsoftu. Vaše zákaznická data se ukládají bezpečně.

Importované objekty zásad skupiny můžete kdykoli odstranit:

1. Přejít na **zařízení**  >  **Zásady skupiny Analytics (Preview)**.
2. Vyberte kontextovou nabídku > **Odstranit**:

    :::image type="content" source="./media/group-policy-analytics/delete-imported-gpo.png" alt-text="Odstraňte nebo odeberte objekt zásad skupiny (GPO), který jste importovali v nástroji Zásady skupiny Analyzer v Microsoft Intune a centru pro správu Správce koncových bodů.":::

## <a name="next-steps"></a>Další kroky

- [Použití Šablony pro správu Windows 10 ke konfiguraci nastavení zásad skupiny v Microsoft Endpoint Manageru](administrative-templates-windows.md)

- [Přidání nastavení ochrany koncových bodů v Microsoft Endpoint Manageru](../protect/endpoint-protection-configure.md)

## <a name="see-also"></a>Viz také

Další informace o [poskytovatelích konfiguračních služeb (CSP)](https://docs.microsoft.com/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers).
