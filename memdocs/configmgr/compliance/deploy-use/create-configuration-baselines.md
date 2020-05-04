---
title: Vytváření standardních hodnot konfigurace
titleSuffix: Configuration Manager
description: V Configuration Manager vytvořte standardní hodnoty konfigurace, které můžete nasadit do kolekce.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2028974c166e060f445b255db6c5af707725a3f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712922"
---
# <a name="create-configuration-baselines-in-configuration-manager"></a>Vytvoření standardních hodnot konfigurace v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*


Standardní hodnoty konfigurace v Configuration Manager obsahují předdefinované položky konfigurace a volitelně i další standardní hodnoty konfigurace. Po vytvoření standardních hodnot konfigurace je můžete nasadit do kolekce tak, aby zařízení v dané kolekci stáhla dané standardní hodnoty konfigurace a vyhodnotila svůj soulad s nimi.  

## <a name="configuration-baselines"></a>Standardní hodnoty konfigurace

 Standardní hodnoty konfigurace v Configuration Manager mohou obsahovat konkrétní revize položek konfigurace nebo je lze nakonfigurovat tak, aby vždy používaly nejnovější verzi položky konfigurace. Další informace o revizích položek konfigurace najdete v tématu [úlohy správy pro konfigurační data](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Existují dvě metody, které můžete použít k vytvoření standardních hodnot konfigurace:  

- Import konfiguračních dat ze souboru. **Průvodce importem dat konfigurace**spustíte tak, že v uzlu **Položky konfigurace** nebo **Standardní hodnoty konfigurace** v pracovním prostoru **Prostředky a kompatibilita** kliknete na tlačítko **Import konfiguračních dat**. Další informace najdete v tématu [import konfiguračních dat](import-configuration-data.md).

- Použití dialogového okna **Vytvoření standardních hodnot konfigurace** k vytvoření nových standardních hodnot konfigurace.  

## <a name="create-a-configuration-baseline"></a>Vytvoření standardních hodnot konfigurace

Pokud chcete vytvořit standardní hodnoty konfigurace pomocí dialogového okna **Vytvoření standardních hodnot konfigurace** , použijte následující postup:  

1. V konzole Configuration Manager klikněte na **prostředky a dodržování předpisů** > **Nastavení** > dodržování předpisů**standardní hodnoty konfigurace**.  

2. Na kartě **Domů** ve skupině **Vytvořit** klikněte na **Vytvořit standardní hodnoty konfigurace**.  

3. V dialogovém okně **Vytvoření standardních hodnot konfigurace** zadejte jedinečný název a popis standardních hodnot konfigurace. Můžete použít maximálně 255 znaků pro název a 512 znaků pro popis.  

4. V seznamu **Konfigurační data** jsou zobrazené všechny položky konfigurace nebo standardní hodnoty konfigurace, které jsou součástí těchto standardních hodnot konfigurace. Kliknutím na tlačítko **Přidat** přidáte do seznamu novou položku konfigurace nebo standardní hodnoty konfigurace. Můžete si vybrat z následujících položek:  

   - **Položky konfigurace**  

   - **Aktualizace softwaru**  

   - **Standardní hodnoty konfigurace**  
     > [!IMPORTANT]
     > Jednotlivé standardní hodnoty konfigurace musíte omezit na maximálně 1000 aktualizací softwaru.
5. Pomocí seznamu **Změna účelu** můžete určit chování položky konfigurace, kterou jste vybrali v seznamu **konfigurační data** . Můžete vybrat z následujících položek:  

   -   **Požadováno**: standardní hodnoty konfigurace se vyhodnotí jako nesplňující požadavky, pokud položka konfigurace není zjištěná na klientském zařízení. Pokud se zjistí, vyhodnotí se dodržování předpisů.  

   -   **Volitelné**: položka konfigurace se vyhodnocuje jenom v případě, že se aplikace, na kterou odkazuje, nachází v klientských počítačích. Pokud se aplikace nenajde, standardní hodnoty konfigurace se neoznačí jako nedodržující předpisy (platí jenom pro položky konfigurace aplikace).  

   -   **Zakázáno**: standardní hodnoty konfigurace se vyhodnotí jako nesplňující požadavky, pokud je v klientských počítačích zjištěna položka konfigurace (platí jenom pro položky konfigurace aplikace).  

   > [!NOTE]
   >  Seznam **Změna účelu** je dostupný jenom v případě, že kliknete na možnost **Tato položka konfigurace obsahuje nastavení aplikace** na stránce **Obecné** v **Průvodci vytvořením položky konfigurace**.  

6. Pomocí seznamu **Změna revize** vyberte konkrétní nebo nejnovější revizi položky konfigurace k vyhodnocení shody na klientských zařízeních nebo vyberte **Vždy použít nejnovější** , když chcete vždy použít nejnovější verzi. Další informace o revizích položek konfigurace najdete v tématu [úlohy správy pro konfigurační data](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

7. Chcete-li odebrat položku konfigurace ze standardních hodnot konfigurace, vyberte položku konfigurace a klikněte na tlačítko **Odebrat**.  

8. Počínaje verzí 1806 vyberte, pokud chcete **vždy použít tuto základnu pro spoluspravované klienty**. Pokud je tato možnost zaškrtnutá, bude se tato standardní hodnota vztahovat i na klienty, kteří jsou spravováni službou Intune.  Tato výjimka se dá použít ke konfiguraci nastavení, která vaše organizace vyžaduje, ale ještě není v Intune dostupná.

9. Volitelně můžete kliknutím na **kategorie** přiřadit kategorie ke směrnému plánu pro vyhledávání a filtrování. 

10. Kliknutím na tlačítko **OK** dialogové okno **Vytvoření standardních hodnot konfigurace** zavřete a vytvoříte nové standardní hodnoty konfigurace.  

>[!NOTE]
> Úprava existujícího směrného plánu, například nastavení **vždy použít tuto standardní hodnotu pro spoluspravované klienty**, zvýší verzi obsahu směrného plánu. Klienti budou muset vyhodnotit novou verzi, aby bylo možné aktualizovat základní sestavy.

## <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a><a name="bkmk_CAbaselines"></a>Zahrnout vlastní standardní hodnoty konfigurace jako součást posouzení zásad dodržování předpisů
<!--3608345-->
*(Představené ve verzi 1910)*

Počínaje verzí 1910 můžete přidat hodnocení vlastních standardních hodnot konfigurace jako pravidla pro vyhodnocení zásad dodržování předpisů. Když vytváříte nebo upravujete standardní hodnoty konfigurace, máte možnost **vyhodnotit tyto standardní hodnoty jako součást hodnocení zásad dodržování předpisů**. Když přidáváte nebo upravujete pravidlo zásad dodržování předpisů, máte podmínku s názvem **Zahrnout nakonfigurované směrné plány v vyhodnocení zásad dodržování předpisů**. Pro spoluspravovaná zařízení a při konfiguraci Intune tak, aby byly výsledky vyhodnocení dodržování předpisů Configuration Manager v rámci celkového stavu dodržování předpisů, se tyto informace odesílají do Azure AD. Pak ji můžete použít pro podmíněný přístup k prostředkům sady Office 365. Další informace najdete v tématu [podmíněný přístup s spolusprávou](../../comanage/quickstart-conditional-access.md).

Pokud chcete jako součást vyhodnocení zásad dodržování předpisů zahrnout vlastní standardní hodnoty konfigurace, udělejte toto:

- Vytvořte a nasaďte zásady dodržování předpisů pro kolekci uživatelů s pravidlem, které [**zahrnuje nakonfigurované směrné plány v vyhodnocení zásad dodržování předpisů**](#bkmk_CA).
- Vyberte možnost [**vyhodnotit tuto základnu jako součást vyhodnocení zásad dodržování předpisů**](#bkmk_eval-baseline) ve standardních hodnotách konfigurace nasazených do kolekce zařízení.

> [!IMPORTANT]
> Když cílíte na zařízení, která jsou spoluspravovaná, ujistěte se, že splňujete [požadavky spolusprávy](../../comanage/overview.md#prerequisites).

### <a name="example-evaluation-scenario"></a>Ukázkový scénář pro vyhodnocení

Když je uživatel součástí kolekce, která je cílem zásady dodržování předpisů, která zahrnuje podmínku pravidla, **zahrnuje nakonfigurované směrné plány v hodnocení zásad dodržování předpisů**. všechny směrné plány s vyhodnocením této standardní hodnoty v rámci vybrané možnosti **vyhodnocení zásad dodržování předpisů** , které jsou nasazené pro uživatele nebo zařízení uživatele, se vyhodnocují pro dodržování předpisů. Příklad:

- `User1`je součástí `User Collection 1`.
- `User1`používá `Device1`, který je v `Device Collection 1` a `Device Collection 2`.
- `Compliance Policy 1`má **zahrnuté nakonfigurované směrné plány v podmínkách pravidla vyhodnocení zásad dodržování předpisů** a nasadí se do `User Collection 1`.
- `Configuration Baseline 1`**vyhodnotí tento směrný plán jako součást vyhodnocování zásad dodržování předpisů** a nasadí se do `Device Collection 1`.
- `Configuration Baseline 2`**vyhodnotí tento směrný plán jako součást vyhodnocování zásad dodržování předpisů** a nasadí se do `Device Collection 2`.

V tomto scénáři, při `Compliance Policy 1` vyhodnocování `User1` použití `Device1`, `Configuration Baseline 1` `Configuration Baseline 2` jsou vyhodnoceny i.

- `User1`někdy používá `Device2`.
- `Device2`je členem `Device Collection 2` a `Device Collection 3`.
- `Device Collection 3`byl `Configuration Baseline 3` do něj nasazen, ale **vyhodnotí tento směrný plán jako součást hodnocení zásad dodržování předpisů** není vybrána.

Při `User1` použití `Device2`se vyhodnotí `Configuration Baseline 2` jenom `Compliance Policy 1` při vyhodnocování.

> [!NOTE]
><!--5582516-->
> Pokud zásada dodržování předpisů vyhodnotí nový směrný plán, který se v klientovi nikdy nevyhodnotil, může hlásit neshodu. K tomu dojde, pokud je vyhodnocení standardních hodnot pořád spuštěné při vyhodnocení dodržování předpisů. Pokud chcete tento problém vyřešit, klikněte na **ověřit dodržování předpisů** v **centru softwaru**.

### <a name="create-and-deploy-a-compliance-policy-with-a-rule-for-baseline-compliance-policy-assessment"></a><a name="bkmk_CA"></a>Vytvoření a nasazení zásad dodržování předpisů pomocí pravidla pro vyhodnocení zásad dodržování předpisů podle směrného plánu

1. V pracovním prostoru **prostředky a kompatibilita** rozbalte **Nastavení dodržování předpisů**a potom vyberte uzel **Policies (zásady dodržování předpisů** ).
1. Kliknutím na **vytvořit zásadu dodržování předpisů** na pásu karet zobrazíte **Průvodce vytvořením zásad dodržování předpisů**. 
1. Na stránce **Obecné** vyberte **pravidla dodržování předpisů pro zařízení spravovaná pomocí klienta Configuration Manager**.
   - Zařízení musí být spravovaná pomocí klienta Configuration Manager, aby jako součást hodnocení zásad dodržování předpisů zahrnovala vlastní standardní hodnoty konfigurace.
1. Na stránkách **podporované platformy** vyberte platformy.
1. Na stránce **pravidla** vyberte **Nový**a potom v podmínce **vyhodnocení zásad dodržování předpisů zaškrtněte políčko Zahrnout nakonfigurované směrné plány** .

   ![Zahrnout nakonfigurované směrné plány v podmínkách vyhodnocení zásad dodržování předpisů](./media/3608345-create-compliance-policy-rule.png)

1. Klikněte na **OK**a potom na tlačítko **Další** , abyste se dostali na stránku **souhrnu** .
1. Ověřte výběr a klikněte na tlačítko **Další** a potom na tlačítko **Zavřít**.
1. V uzlu **zásady dodržování předpisů** klikněte pravým tlačítkem na zásadu, kterou jste vytvořili, a vyberte **nasadit**.
1. Vyberte svou kolekci, nastavení generování výstrah a plán vyhodnocení dodržování předpisů pro tyto zásady.
1. Kliknutím na **OK** nasaďte zásady dodržování předpisů.

### <a name="select-a-configuration-baseline-and-check-evaluate-this-baseline-as-part-of-compliance-policy-assessment"></a><a name="bkmk_eval-baseline"></a>Vyberte standardní hodnoty konfigurace a zaškrtněte políčko vyhodnotit tuto základní hodnotu jako součást hodnocení zásad dodržování předpisů.

1. V pracovním prostoru **prostředky a kompatibilita** rozbalte **Nastavení dodržování předpisů**a potom vyberte uzel **standardní hodnoty konfigurace** .
1. Klikněte pravým tlačítkem na existující standardní hodnoty nasazené do kolekce zařízení a pak vyberte **vlastnosti**. V případě potřeby můžete vytvořit nový směrný plán.
   - Standardní hodnoty musí být nasazeny do kolekce zařízení, nikoli z uživatelské kolekce.
1. Povolí **vyhodnotit tuto standardní hodnotu jako součást nastavení vyhodnocení zásad dodržování předpisů** .
   - Pro spoluspravovaná zařízení, která mají Intune jako autoritu pro **konfiguraci zařízení** , zajistěte, aby se i **pro spoluspravované klienty vždy použili tato standardní** hodnota.
1. Kliknutím na tlačítko **OK** uložte změny do standardních hodnot konfigurace.

   ![Dialogové okno Vlastnosti standardních hodnot konfigurace](./media/3608345-configuration-baseline-properties.png)

### <a name="log-files-for-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Soubory protokolu pro vlastní standardní hodnoty konfigurace v rámci vyhodnocení zásad dodržování předpisů

- ComplianceHandler. log
- SettingsAgent. log
- DCMAgent.log
- CIAgent.log

## <a name="next-steps"></a>Další kroky

[Import konfiguračních dat](import-configuration-data.md)
