---
title: nastavení rozšíření macOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidání, konfigurace nebo vytvoření nastavení na zařízeních macOS, aby se používala systémová rozšíření a rozšíření jádra. Umožňuje také uživatelům přepsat schválená rozšíření, umožnit všechna rozšíření z identifikátoru týmu nebo v Microsoft Intune umožnit specifická rozšíření nebo aplikace.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b716a7e85f817e95a9f1fec992458e052570d81
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429519"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-and-system-extensions-in-intune"></a>macOS nastavení zařízení pro konfiguraci a používání jádra a rozšíření systému v Intune

> [!NOTE]
> rozšíření jádra macOS se nahrazují systémovými rozšířeními. Další informace najdete v tématu [Podpora tipů: Použití systémových rozšíření místo rozšíření jádra pro MacOS Catalina 10,15 v Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

Tento článek obsahuje seznam a popis různých nastavení jádra a rozšíření systému, která můžete řídit na zařízeních macOS. Jako součást řešení správy mobilních zařízení (MDM) můžete pomocí těchto nastavení přidat a spravovat rozšíření na zařízeních.

Další informace o rozšířeních v Intune a všech požadavcích najdete v tématu [Přidání rozšíření MacOS](kernel-extensions-overview-macos.md).

Tato nastavení se přidají do konfiguračního profilu zařízení v Intune a pak se přiřadí nebo nasadí do zařízení macOS.

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte konfigurační profil rozšíření MacOS](kernel-extensions-overview-macos.md).

> [!NOTE]
> Tato nastavení platí pro různé typy registrace. Další informace o různých typech registrace najdete v tématu [registrace MacOS](../enrollment/macos-enroll.md).

## <a name="kernel-extensions"></a>Rozšíření jádra

Tato funkce platí pro:

- macOS 10.13.2 a novější
- Vyžaduje se registrace zařízení schváleného uživatelem. 

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení schválená uživatelem, automatický zápis zařízení

- **Povolit přepsání uživatelem**: **Ano** umožní uživatelům schvalovat rozšíření jádra, která nejsou součástí konfiguračního profilu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit uživatelům v povolení rozšíření, která nejsou součástí konfiguračního profilu. To znamená, že jsou povoleny pouze rozšíření, která jsou součástí konfiguračního profilu.

  Další informace o této funkci najdete v tématu [načítání rozšíření jádra pro uživatele](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (otevře se webová stránka společnosti Apple).

- **Povolené identifikátory týmu**: Toto nastavení použijte, pokud chcete povolit jedno nebo několik ID týmu. Všechna rozšíření jádra podepsaná pomocí vámi zadaných ID týmu jsou povolena a důvěryhodná. Jinými slovy, pomocí této možnosti povolíte všechna rozšíření jádra v rámci stejného ID týmu, což může být konkrétní vývojář nebo partner.

  **Přidejte** identifikátor týmu platných a podepsaných rozšíření jádra, která se mají načíst. Můžete přidat více identifikátorů týmu. Identifikátor týmu musí být alfanumerický (písmena a číslice) a musí obsahovat 10 znaků. Zadejte například `ABCDE12345`.

  Po přidání identifikátoru týmu je možné jej také odstranit.

  [Najděte své ID týmu](https://help.apple.com/developer-account/#/dev55c3c710c) (otevře web společnosti Apple) obsahuje další informace.

- **Povolená rozšíření jádra**: pomocí tohoto nastavení můžete povolit specifická rozšíření jádra. Jsou povolená nebo důvěryhodná jenom rozšíření jádra, která zadáte.

  **Přidejte** identifikátor sady prostředků a identifikátor týmu rozšíření jádra, které se má načíst. U nepodepsaných starších rozšíření jádra použijte prázdný identifikátor týmu. Můžete přidat více rozšíření jádra. Identifikátor týmu musí být alfanumerický (písmena a číslice) a musí obsahovat 10 znaků. Například zadejte `com.contoso.appname.macos` pro **ID sady prostředků**a `ABCDE12345` pro **identifikátor týmu**.

  > [!TIP]
  > Pokud chcete získat ID sady rozšíření jádra (kext) na zařízení macOS, můžete:
  >
  > 1. V terminálu spusťte `kextstat | grep -v com.apple` a poznamenejte si výstup. Nainstalujte software nebo KEXT, který chcete. Spusťte `kextstat | grep -v com.apple` akci znovu a vyhledejte změny.
  >
  >    V terminálu `kextstat` obsahuje seznam všech rozšíření jádra v operačním systému. 
  >
  > 2. V zařízení otevřete seznam vlastností informace (info. plist) pro KEXT. Zobrazí se ID sady prostředků. Každý KEXT má soubor info. plist uložený v rámci.

> [!NOTE]
> Nemusíte přidávat identifikátory týmu a rozšíření jádra. Můžete nakonfigurovat jednu nebo druhou.

## <a name="system-extensions"></a>Rozšíření systému

Tato funkce platí pro:

- macOS 10,15 a novější
- Vyžaduje se registrace zařízení schváleného uživatelem.

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Nastavení platí pro: registrace zařízení schválená uživatelem, automatický zápis zařízení

- **Blokovat přepsání uživatelů**: možnost **Ano** zabrání uživatelům v schvalování systémových rozšíření, která nejsou v seznamu povolených. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém uživatelům povolit schválení neznámých rozšíření, která nejsou součástí konfiguračního profilu. To znamená, že rozšíření nezahrnutá do konfiguračního profilu jsou povolená.

- **Povolené identifikátory týmu**: Toto nastavení použijte, pokud chcete povolit jedno nebo několik ID týmu. Všechna rozšíření systému podepsaná pomocí vámi zadaných ID týmu jsou vždy povolena a důvěryhodná. Jinými slovy, pomocí této možnosti povolíte všechna systémová rozšíření v rámci stejného ID týmu, což může být konkrétní vývojář nebo partner.

  **Přidejte** **identifikátor týmu** platných a podepsaných systémových rozšíření, která se mají načíst. Můžete přidat více identifikátorů týmu. Identifikátor týmu musí být alfanumerický (písmena a číslice) a musí obsahovat 10 znaků. Zadejte například `ABCDE12345`.

  Po přidání identifikátoru týmu je možné jej také odstranit.

  [Najděte své ID týmu](https://help.apple.com/developer-account/#/dev55c3c710c) (otevře web společnosti Apple) obsahuje další informace.

- **Povolená rozšíření systému**: pomocí tohoto nastavení můžete vždycky povolit specifická systémová rozšíření. Pouze vámi zadaná rozšíření systému jsou povolena nebo důvěryhodná.

  **Přidejte** **identifikátor sady prostředků** a **identifikátor týmu** rozšíření systému, který se má načíst. Pro nepodepsaná starší verze systému použijte prázdný identifikátor týmu. Můžete přidat několik rozšíření systému. Identifikátor týmu musí být alfanumerický (písmena a číslice) a musí obsahovat 10 znaků. Například zadejte `com.contoso.appname.macos` pro **ID sady prostředků**a `ABCDE12345` pro **identifikátor týmu**.

- **Povolené typy rozšíření systému**: Zadejte ID týmu a typy rozšíření systému, které chcete povolit pro toto ID týmu:
  - **Identifikátor týmu**: Zadejte ID týmu jiného rozšíření systému, které chcete použít pro určité typy rozšíření. Případně zadejte ID týmu, které jste přidali k **povoleným rozšířením systému**.
  - **Povolené typy rozšíření systému**: Vyberte typy rozšíření systému, které chcete povolit pro každé ID týmu. Možnosti:
    - Vybrat vše
    - Rozšíření ovladačů
    - Rozšíření sítě
    - Rozšíření zabezpečení koncového bodu

    Další informace o těchto typech rozšíření najdete v tématu [systémová rozšíření](https://developer.apple.com/system-extensions/) (otevře web společnosti Apple).

    Můžete přidat ID týmu ze seznamu **povolených systémových rozšíření** a povolit konkrétní typ rozšíření. Pokud je přípona typu, který není povolen, rozšíření se nemusí spustit.

    Pokud chcete povolit všechny typy rozšíření pro ID týmu, přidejte ID týmu do seznamu **povolených systémových rozšíření** . Nepřidávejte ID týmu do seznamu **povolených typů systémových rozšíření** . Jinými slovy, pokud je ID týmu v seznamu **povolených rozšíření systému** , a ne v seznamu **povolených typů rozšíření systému** , jsou pro toto ID týmu povoleny všechny typy rozšíření.

> [!NOTE]
> Přidání stejného ID týmu pro **povolená rozšíření systému** a **povolené identifikátory týmu** může mít za následek chybu a profil se nezdařil. Nepřidáte do obou nastavení stejný přesný identifikátor týmu. 

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).
