---
title: nastavení rozšíření jádra macOS v Microsoft Intune – Azure | Microsoft Docs
titleSuffix: ''
description: Přidání, konfigurace nebo vytvoření nastavení na zařízeních macOS pro použití rozšíření jádra. Umožňuje také uživatelům přepsat schválená rozšíření, umožnit všechna rozšíření z identifikátoru týmu nebo v Microsoft Intune umožnit specifická rozšíření nebo aplikace.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/24/2020
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
ms.openlocfilehash: 2e18fad8f1112681a62bcdacd63c652cfd4ad3ac
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359296"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-extensions-in-intune"></a>nastavení zařízení macOS pro konfiguraci a používání rozšíření jádra v Intune

Tento článek obsahuje seznam a popis různých nastavení rozšíření jádra, která můžete řídit na zařízeních macOS. Jako součást řešení správy mobilních zařízení (MDM) můžete pomocí těchto nastavení přidat a spravovat rozšíření jádra na svých zařízeních.

Další informace o rozšíření jádra v Intune a všech požadavcích najdete v tématu [Přidání rozšíření jádra MacOS](kernel-extensions-overview-macos.md).

Tato nastavení se přidají do konfiguračního profilu zařízení v Intune a pak se přiřadí nebo nasadí do zařízení macOS.

## <a name="before-you-begin"></a>Před zahájením

[Vytvořte konfigurační profil rozšíření jádra zařízení](kernel-extensions-overview-macos.md).

> [!NOTE]
> Tato nastavení platí pro různé typy registrace. Další informace o různých typech registrace najdete v tématu [registrace MacOS](../enrollment/macos-enroll.md).

## <a name="kernel-extensions"></a>Rozšíření jádra

### <a name="settings-apply-to-user-approved-automated-device-enrollment"></a>Nastavení platí pro: schváleno uživatelem, automatický zápis zařízení

- **Povolit přepsání uživatelem**: **Povolit** umožní uživatelům schvalovat rozšíření jádra, která nejsou součástí konfiguračního profilu. Pokud je nastavené na **Nenakonfigurováno** (výchozí nastavení), Intune se nezmění ani neaktualizuje toto nastavení. Ve výchozím nastavení může operační systém zabránit uživatelům v povolení rozšíření, která nejsou součástí konfiguračního profilu. To znamená, že jsou povoleny pouze rozšíření, která jsou součástí konfiguračního profilu.

  Další informace o této funkci najdete v tématu [načítání rozšíření jádra pro uživatele](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (otevření webu společnosti Apple).

- **Povolené identifikátory týmu**: Toto nastavení použijte, pokud chcete povolit jedno nebo několik ID týmu. Všechna rozšíření jádra podepsaná pomocí vámi zadaných ID týmu jsou povolena a důvěryhodná. Jinými slovy, pomocí této možnosti povolíte všechna rozšíření jádra v rámci stejného ID týmu, což může být konkrétní vývojář nebo partner.

  **Přidejte** identifikátor týmu platných a podepsaných rozšíření jádra, která chcete načíst. Můžete přidat více identifikátorů týmu. Identifikátor týmu musí být alfanumerický (písmena a číslice) a musí obsahovat 10 znaků. Zadejte například `ABCDE12345`.

  Po přidání identifikátoru týmu je možné jej také odstranit.

  [Najděte své ID týmu](https://help.apple.com/developer-account/#/dev55c3c710c) (otevře web společnosti Apple) obsahuje další informace.

- **Povolená rozšíření jádra**: pomocí tohoto nastavení můžete povolit specifická rozšíření jádra. Jsou povolená nebo důvěryhodná jenom rozšíření jádra, která zadáte.

  **Přidejte** identifikátor sady prostředků a identifikátor týmu rozšíření jádra, které chcete načíst. U nepodepsaných starších rozšíření jádra použijte prázdný identifikátor týmu. Můžete přidat více rozšíření jádra. Identifikátor týmu musí být alfanumerický (písmena a číslice) a musí obsahovat 10 znaků. Zadejte například `com.contoso.appname.macos` pro **ID sady prostředků**a `ABCDE12345` pro **identifikátor týmu**.

  > [!TIP]
  > Pokud chcete získat ID sady rozšíření jádra (kext) na zařízení macOS, můžete:
  >
  > 1. V terminálu spusťte `kextstat | grep -v com.apple`a poznamenejte si výstup. Nainstalujte software nebo KEXT, který chcete. Znovu spusťte `kextstat | grep -v com.apple` a vyhledejte změny.
  >
  >    V terminálu `kextstat` zobrazí seznam všech rozšíření jádra v operačním systému. 
  >
  > 2. V zařízení otevřete seznam vlastností informace (info. plist) pro KEXT. Zobrazí se ID sady prostředků. Každý KEXT má soubor info. plist uložený v rámci.

> [!NOTE]
> Nemusíte přidávat identifikátory týmu a rozšíření jádra. Můžete nakonfigurovat jednu nebo druhou.

## <a name="next-steps"></a>Další kroky

[Přiřaďte profil](device-profile-assign.md) a [monitorujte jeho stav](device-profile-monitor.md).
