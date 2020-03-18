---
title: Zobrazení profilů zařízení v Microsoft Intune – Azure | Microsoft Docs
description: Zobrazte a spravujte podrobnosti konfiguračního profilu zařízení v Microsoft Intune, prohlédněte si graf počtu zařízení přiřazených k profilu a zjistěte, která zařízení mají přiřazené nebo nasazené profily. Můžete také vyřešit problémy s profily, které mají konfliktní nastavení.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 10/21/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9deaed87-fb4b-4689-ba88-067bc61686d7
ms.reviewer: karthib
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 23594bd1e728e20deba6d978fc2a1f678d692ff3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/13/2020
ms.locfileid: "79333135"
---
# <a name="monitor-device-profiles-in-microsoft-intune"></a>Sledování profilů zařízení v Microsoft Intune



Intune obsahuje některé funkce, které vám pomůžou monitorovat a spravovat vaše konfigurační profily zařízení. Můžete třeba kontrolovat stav profilu, zjistit, která zařízení jsou přiřazená, a aktualizovat vlastnosti profilu.

## <a name="view-existing-profiles"></a>Zobrazení existujících profilů

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte **zařízení** > **konfigurační profily**.

Vypíšou se všechny existující profily včetně podrobností jako je platforma, a zobrazí se, jestli je profil přiřazený k nějakým zařízením.

## <a name="view-details-on-a-profile"></a>Zobrazení podrobností profilu

Po vytvoření profilu zařízení Intune nabízí grafy. Tyto grafy zobrazují stav profilu, třeba že je úspěšně přiřazený k zařízením nebo jestli profil vykazuje konflikt.

1. Vyberte existující profil. Můžete třeba vybrat profil macOS.
2. Vyberte kartu **Přehled**.

    Horní grafický graf znázorňuje počet zařízení přiřazených k profilu zařízení. Pokud třeba konfigurační profil zařízení platí pro zařízení s macOS, zobrazí se v grafu počet zařízení s macOS.

    Ukazuje také počet zařízení pro jiné platformy, která jsou přiřazená ke stejnému profilu zařízení. Může třeba ukazovat počet zařízení bez macOS.

    ![Zobrazení počtu zařízení přiřazených k profilu zařízení](./media/device-profile-monitor/device-configuration-profile-graphical-chart.png)

    Dolní graf znázorňuje počet uživatelů přiřazených k profilu zařízení. Pokud třeba konfigurační profil zařízení platí pro uživatele s macOS, zobrazí se v grafu počet uživatelů s macOS.

3. Vyberte kruh v horním grafu. Otevře se **Stav zařízení**.

    Jsou uvedená zařízení přiřazená k profilu a zobrazuje se, jestli je profil úspěšně nasazený. Všimněte si také, že jsou uvedená jenom zařízení s konkrétní platformou (třeba macOS).

    Zavřete podrobné informace **Stav zařízení**.

4. Vyberte kruh v dolním grafu. Otevře se **Stav uživatele**. 

    Jsou uvedení uživatelé přiřazení k profilu a zobrazuje se, jestli je profil úspěšně nasazený. Všimněte si také, že jsou uvedení jenom uživatelé s konkrétní platformou (třeba macOS).

    Zavřete podrobné informace **Stav uživatele**.

5. V seznamu **Profily** vyberte konkrétní profil. Můžete také změnit stávající vlastnosti:
    - **Vlastnosti**: Můžete změnit název nebo aktualizovat libovolné existující nastavení.
    - **Přiřazení**: Můžete zahrnout nebo vyloučit zařízení, pro která mají zásady platit. Pomocí **Vybraných skupin** vyberte konkrétní skupiny.
    - **Stav zařízení**: Jsou uvedená zařízení přiřazená k profilu a zobrazuje se, jestli je profil úspěšně nasazený. Můžete vybrat konkrétní zařízení a zjistit další podrobnosti, včetně nainstalovaných aplikací.
    - **Stav uživatele**: vypíše uživatelská jména se zařízeními ovlivněnými tímto profilem a v případě úspěšného nasazení profilu. Můžete vybrat konkrétního uživatele a zjistit další podrobnosti.
    - **Stav podle nastavení**: Filtruje výstup tím, že zobrazí jednotlivá nastavení v rámci profilu, a zobrazuje, jestli je toto nastavení úspěšně použité.

## <a name="view-conflicts"></a>Zobrazení konfliktů

V **Zařízení** > **Všechna zařízení** se zobrazují všechna nastavení, která způsobují konflikt. V případě konfliktu se zobrazí také všechny konfigurační profily, které obsahují toto nastavení. Správci můžou tuto funkci použít k vyřešení všech nesrovnalostí v profilech.

1. V Intune vyberte **Zařízení** > **Všechna zařízení** > vyberte existující zařízení v seznamu. Koncový uživatel může název zařízení získat z aplikace Portál společnosti.
2. Vyberte **Konfigurace zařízení**. Zobrazí se všechny zásady konfigurace uplatněné na dané zařízení.
3. Vyberte zásadu. Zobrazí se všechna nastavení této zásady, která se uplatňují na dané zařízení. Pokud je zařízení v **konfliktním** stavu, vyberte tento řádek. V novém okně uvidíte všechny profily a názvy profilů obsahujících nastavení, které tento konflikt způsobuje.

Teď, když znáte konfliktní nastavení a zásady, které toto nastavení obsahují, by mělo být snadnější konflikt vyřešit. 

## <a name="device-firmware-configuration-interface-profile-reporting"></a>Vytváření sestav profilu rozhraní pro konfiguraci firmwaru zařízení

> [!WARNING]
> Monitorování profilů DFCI se právě vytváří. I když je DFCI ve verzi Public Preview, data monitorování mohou chybět nebo být neúplná.

Profily DFCI se nastavují na základě nastavení, stejně jako u jiných profilů konfigurace zařízení. V závislosti na podpoře DFCI od výrobce se nemusí některá nastavení vztahovat.

Pomocí nastavení profilu DFCI můžete zobrazit následující stavy:

- **Kompatibilní**: Tento stav ukazuje, že hodnota nastavení v profilu odpovídá nastavení v zařízení. K tomuto stavu může dojít v následujících scénářích:

  - Profil DFCI úspěšně nakonfiguroval nastavení v profilu.
  - Zařízení nemá funkci hardwaru řízenou nastavením a nastavení profilu je **zakázané**.
  - Rozhraní UEFI nepovoluje, aby DFCI funkci zakázal, a nastavení profilu je **povolené**.
  - Zařízení nemá hardware k zakázání této funkce a nastavení profilu je **povolené**.

- **Nelze použít**: Tento stav ukazuje, když je **povolená**hodnota nastavení v profilu a že se nenalezne nastavení odpovídajícího zařízení. K tomuto stavu může dojít, pokud hardware zařízení tuto funkci nemá.

- **Nekompatibilní**: Tento stav ukazuje, že hodnota nastavení v profilu neodpovídá nastavení v zařízení. K tomuto stavu může dojít v následujících scénářích:

  - Rozhraní UEFI nepovoluje DFCI zakázat nastavení a nastavení profilu je **zakázané**.
  - Zařízení nemá hardware k zakázání této funkce a nastavení profilu je **zakázané**.
  - Zařízení nemá nejnovější verzi firmwaru DFCI.
  - DFCI byl před registrací do Intune zakázán pomocí místního ovládacího prvku "výslovný nedostatek" v nabídce UEFI.
  - Zařízení bylo zaregistrováno do Intune mimo registraci autopilotu.
  - Zařízení není zaregistrované na autopilotu pomocí CSP Microsoftu nebo přímo zaregistrované výrobcem OEM.

## <a name="next-steps"></a>Další kroky

[Běžné otázky, problémy a řešení s profily zařízení](device-profile-troubleshoot.md)  
[Řešení potíží se zásadami a profily a v Intune](troubleshoot-policies-in-microsoft-intune.md)
