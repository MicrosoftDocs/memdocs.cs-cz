---
title: Konfigurace zásad aktualizace softwaru pro iOS/iPadOS v Microsoft Intune – Azure | Microsoft Docs
description: V Microsoft Intune vytvořte nebo přidejte zásady konfigurace, které budou omezovat, kdy se aktualizace softwaru automaticky instalují na zařízení s iOS/iPadOS. Můžete zvolit datum a čas, kdy se aktualizace nemají instalovat. Můžete tyto zásady také přiřadit skupinám, uživatelům nebo zařízením a vyhledat případné chyby instalace.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0a81e0e59eca03c9c15d7553376ea0c524251a18
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914850"
---
# <a name="add-iosipados-software-update-policies-in-intune"></a>Přidání zásad aktualizace softwaru pro iOS/iPadOS v Intune

Zásady aktualizace softwaru umožňují vynutit zařízení s iOS/iPadOS pod dohledem, aby automaticky instalovala aktualizace operačního systému. Zařízení pod dohledem jsou ta, která se zaregistrovala pomocí Apple Business Manageru nebo Apple School Manageru. Když konfigurujete zásadu pro nasazení aktualizací, můžete:

- Vyberte, zda chcete nasadit *nejnovější aktualizaci* , která je k dispozici, nebo vyberte možnost nasazení starší aktualizace podle čísla verze aktualizace, pokud nechcete nasadit nejnovější aktualizaci. Pokud se rozhodnete nasadit starší aktualizaci, musíte taky nastavit zásady konfigurace zařízení, aby se omezila viditelnost aktualizací softwaru.
- Zadejte plán, který určuje, kdy se má aktualizace instalovat. Plány můžou být tak jednoduché jako při instalaci aktualizací při příštím ověření zařízení nebo při vytváření rozsahů data a času, během kterých se aktualizace můžou instalovat nebo se zablokuje instalace.

Tato funkce platí pro:

- iOS 10,3 a novější (pod dohledem)
- iPadOS 13,0 a novější (pod dohledem)

Ve výchozím nastavení se zařízení zaregistrují v Intune každých 8 hodin. Pokud je aktualizace dostupná prostřednictvím zásad aktualizace, zařízení tuto aktualizaci stáhne. Zařízení pak nainstaluje aktualizaci při dalším vrácení se změnami v rámci konfigurace plánu. I když proces aktualizace obvykle nezahrnuje interakci s uživatelem, pokud má zařízení heslo, musí ho uživatel zadat, aby mohl spustit aktualizaci softwaru. Profily nebrání uživatelům v ruční aktualizaci operačního systému. Uživatelům se dá zabránit v ruční aktualizaci operačního systému pomocí zásad konfigurace zařízení, aby se omezila viditelnost aktualizací softwaru.

> [!NOTE]
> Pokud používáte [autonomní režim jedné aplikace (Asam)](../configuration/device-restrictions-ios.md#autonomous-single-app-mode-asam), měli byste zvážit dopad aktualizací operačního systému, protože výsledné chování může být nežádoucí.
Zvažte testování, abyste posoudili dopad aktualizací operačního systému na aplikaci, kterou používáte v ASAM.

## <a name="configure-the-policy"></a>Konfigurace zásad

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení**  >  **Aktualizace zásady pro iOS/iPadOS**  >  **vytvořit profil**.
3. Na kartě **základy** zadejte název této zásady, zadejte popis (volitelné) a pak vyberte **Další**.

   ![Karta základy](./media/software-updates-ios/basics-tab.png)

4. Na kartě **aktualizovat nastavení zásad** proveďte následující konfiguraci:

   1. **Vyberte verzi, kterou chcete nainstalovat**. Na výběr máte tyto:

      - *Nejnovější aktualizace*: Tato akce nasadí poslední vydanou aktualizaci pro iOS/iPadOS.
      - Všechny předchozí verze, které jsou k dispozici v rozevíracím seznamu. Pokud vyberete předchozí verzi, musíte taky nasadit zásady konfigurace zařízení, abyste mohli zpozdit přehlednost aktualizací softwaru.

   2. **Typ plánu**: Nakonfigurujte plán pro tyto zásady:

      - *Aktualizovat při dalším vrácení se změnami*: aktualizace se na zařízení nainstaluje při příštím ověření v Intune. Toto je nejjednodušší možnost a nemá žádné další konfigurace.
      - *Aktualizovat během naplánovaného času*: nakonfigurujete jednu nebo více oken času, během kterých se aktualizace nainstaluje při vrácení se změnami.
      - *Aktualizace mimo plánovaný čas*: nakonfigurujete jednu nebo více časových oken, během kterých se aktualizace nebudou instalovat při vrácení se změnami.

   3. **Týdenní plán**: Pokud při *dalším vrácení se změnami*zvolíte jiný typ plánu než aktualizace, nakonfigurujte následující možnosti:

      ![Příklad výběru, který se má aktualizovat během naplánovaného času](./media/software-updates-ios/scheduled-time.png)

      - **Časové pásmo**: Vyberte časové pásmo.
      - **Časový interval**: definujte jeden nebo více bloků času, které omezují, kdy se aktualizace nainstalují. Účinek následujících možností závisí na typu plánu, který jste vybrali. Pomocí počátečního a koncového dne se podporují přenocování kamenných bloků. Vaše možnosti jsou:

        - **Počáteční den**: vyberte den, ve kterém se spustí okno plán.
        - **Čas spuštění**: vyberte časový den, kdy se má okno plánování začít. Pokud například vyberete hodnotu 5 AM a naplánujete typ plánu *aktualizace během naplánovaného času*, bude 5 am čas, kdy aktualizace může začít instalovat. Pokud jste zvolili typ plánu *aktualizace mimo naplánovaný čas*, bude čas od 5. až do doby, kdy aktualizace nebude možné instalovat, bude začínat.
        - **Koncový den**: vyberte den, ve kterém skončí časové období.
        - **Koncový čas**: vyberte denní dobu, kdy se okno plánu zastaví. Pokud například vyberete 1 dop. a naplánujete typ plánu *aktualizace během naplánovaného času*, stane se 1. čas, kdy aktualizace již nebude možné instalovat. Pokud jste zvolili typ plánu *aktualizace mimo plánovaný čas*, bude 1. až do doby, kdy může aktualizace instalovat.

       Pokud nekonfigurujete čas ke spuštění nebo ukončení, nebude mít konfigurace žádné omezení a aktualizace se můžou nainstalovat kdykoli.  

       > [!NOTE]
       > Můžete nakonfigurovat nastavení v [omezeních zařízení](../configuration/device-restrictions-ios.md#general) a skrýt tak aktualizaci od uživatelů zařízení po určitou dobu na zařízeních s iOS/iPadOS, která jsou pod dohledem. Doba omezení vám může poskytnout čas na otestování aktualizace, než ji uvidí uživatelé k instalaci. Po vypršení platnosti omezení zařízení bude aktualizace viditelná pro uživatele. Uživatelé si pak můžou zvolit, že se mají nainstalovat, nebo se zásady aktualizace softwaru můžou hned po dokončení automaticky nainstalovat.
       >
       > Pokud k skrytí aktualizace použijete omezení zařízení, zkontrolujte zásady aktualizace softwaru, abyste se ujistili, že neplánují instalaci aktualizace před uplynutím této doby omezení. Zásady aktualizace softwaru instalují aktualizace podle vlastního plánu, bez ohledu na to, která aktualizace je skrytá nebo viditelná pro uživatele zařízení.

   Po nakonfigurování *nastavení zásad aktualizace*vyberte **Další**.

5. Na kartě **značky oboru** vyberte **+ Vybrat rozsah značky** a otevřete tak podokno *Vybrat značky* , pokud je chcete použít pro zásady aktualizace.

   - V podokně **Vybrat značky** vyberte jednu nebo více značek a kliknutím na tlačítko **Vybrat** je přidejte do zásad a vraťte se do podokna *značky oboru* .

   Až budete připraveni, vyberte **Další** a pokračujte v *přiřazení*.

6. Na kartě **přiřazení** zvolte **+ Vybrat skupiny, které se mají zahrnout** , a potom přiřaďte zásadu aktualizace k jedné nebo více skupinám. Pomocí **+ Vyberte skupiny, které se vyloučí** , abyste mohli přiřazení vyladit. Až budete připraveni, klikněte na tlačítko **Další** a pokračujte.

   U zařízení používaných uživateli, na které zásady cílí, se vyhodnotí dodržování předpisů pro aktualizace. Tyto zásady podporují také zařízení bez uživatelů.

7. Na kartě **Revize + vytvořit** zkontrolujte nastavení a potom vyberte **vytvořit** , jakmile budete připraveni Uložit zásady aktualizace pro iOS/iPadOS. Vaše nová zásada se zobrazí v seznamu zásad aktualizace pro iOS/iPadOS.

Pokyny z týmu podpory pro Intune najdete v tématu [zpoždění viditelnosti aktualizací softwaru v Intune pro zařízení pod dohledem](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Delaying-visibility-of-software-updates-in-Intune-for-supervised/ba-p/345753).

> [!NOTE]
> Apple MDM neumožňuje vynutit, aby se aktualizace nainstalovaly na zařízení do určitého času nebo data. Pomocí zásad aktualizace softwaru Intune nemůžete downgradovat verzi operačního systému v zařízení.

## <a name="edit-a-policy"></a>Upravit zásadu

Můžete upravit existující zásadu, včetně změny časových omezení:

1. Vyberte **zařízení**  >  **zásady aktualizace pro iOS**. Vyberte zásadu, kterou chcete upravit.

2. Při prohlížení **vlastností**zásad vyberte **Upravit** pro stránku zásady, kterou chcete upravit.

   ![Upravit zásadu](./media/software-updates-ios/edit-policy.png)

3. Po zavedení změny vyberte zkontrolovat a **Uložit**  >  **Uložit** a uložte provedené úpravy a vraťte se do *vlastností*zásad.

> [!NOTE]
> Pokud je **čas spuštění** i **čas ukončení** nastavený na 12 DOP, Intune nekontroluje při instalaci aktualizací omezení. To znamená, že všechny konfigurace, které máte k dispozici pro **dobu výběru** , se budou ignorovat a aktualizace se můžou nainstalovat kdykoli.

## <a name="monitor-device-installation-failures"></a>Monitorování chyb instalace na zařízeních

<!-- 1352223 -->
**Aktualizace softwaru**  >  **Při selhání instalace pro zařízení s iOS** se zobrazuje seznam zařízení s iOS/iPadOS, která cílí na zásady aktualizace, se pokusilo o aktualizaci a nešlo je aktualizovat. U každého zařízení můžete zobrazit, proč se automaticky neaktualizovalo. Zařízení, která jsou v pořádku a aktuální, se v seznamu nezobrazují. „Aktuální“ zařízení obsahují nejnovější aktualizaci, kterou samotné zařízení podporuje.

## <a name="next-steps"></a>Další kroky

[Monitorujte svůj stav](../configuration/device-profile-monitor.md).