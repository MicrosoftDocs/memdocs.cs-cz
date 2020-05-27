---
title: Obejít Zámek aktivace pro iOS/iPadOS s Intune
titleSuffix: Microsoft Intune
description: Přečtěte si, jak pomocí Intune obejít iOS/iPadOS Zámek aktivace pro přístup k uzamčeným zařízením.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 9ca3b0ba-e41c-45fb-af28-119dff47c59f
ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: eec2bb84a27445444c85f7d64a8d0531fbc30939
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989949"
---
# <a name="disable-activation-lock-on-supervised-iosipados-devices-with-intune"></a>Zakázání Zámek aktivace na zařízeních s iOS/iPadOS pod dohledem v Intune


[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Microsoft Intune vám může pomáhat spravovat Zámek aktivace pro iOS/iPadOS, což je funkce aplikace Najít iPhone pro zařízení s iOS/iPadOS 8,0 a novějším. Zámek aktivace je automaticky zapnutý, když uživatel na zařízení otevře aplikaci Najít iPhone. Když je tato funkce povolená, musí se zadat Apple ID a heslo uživatele, aby bylo možné:

- Vypnout aplikaci Můj iPhone
- Vymazat zařízení
- Znovu aktivovat zařízení

## <a name="how-activation-lock-affects-you"></a>Jaký vliv má funkce Zámek aktivace na práci se zařízením

I když Zámek aktivace pomáhá zabezpečit zařízení s iOS/iPadOS a vylepšuje pravděpodobnost obnovování ztraceného nebo odcizeného zařízení, může vám jako správce IT předcházet několik problémů. Příklad:

- Uživatel si na zařízení nastaví zámek aktivace. Tento uživatel pak společnost opustí a zařízení vrátí. Bez Apple ID a hesla uživatele neexistuje způsob, jak zařízení znovu aktivovat.
- Potřebujete sestavu všech zařízení, která mají povolený zámek aktivace.
- Při obnovování zařízení v organizaci chcete některá zařízení přiřadit jinému oddělení. Můžete to provést jedině se zařízeními, ve kterých není zámek aktivace povolený.

Aby bylo možné tyto problémy vyřešit, společnost Apple zavedla Zámek aktivace zakázat v systému iOS/iPadOS 7,1. Disable Zámek aktivace umožňuje odebrat Zámek aktivace ze zařízení pod dohledem bez Apple ID a hesla uživatele. Dozorovaná zařízení mohou generovat kód pro vyřazení zámku aktivace, který je uložený na aktivačním serveru společnosti Apple.

>[!TIP]
>Režim pod dohledem pro zařízení s iOS/iPadOS umožňuje pomocí Apple Configuratoru zamknout zařízení a omezit funkčnost jenom na konkrétní obchodní účely. Režim dohledu se používá jenom u zařízení v majetku podniků.

Další informace o zámku aktivace najdete na [webu společnosti Apple](https://support.apple.com/HT201365).

## <a name="how-intune-helps-you-manage-activation-lock"></a>Jak Intune pomáhá se správou zámku aktivace
Intune může požádat o stav Zámek aktivace zařízení pod dohledem, na kterých běží iOS/iPadOS 8,0 a novější. V případě zařízení pod dohledem může Intune získat kód pro zákaz Zámek aktivace a přímo ho vydat do zařízení. Pokud bylo zařízení vymazáno, můžete k němu získat přístup přímo tak, že uživatelské jméno necháte prázdné a jako heslo zadáte tento kód.

**Správy zámku aktivace pomocí Intune přináší firmám následující výhody:**

- Uživatel získá výhody zabezpečení aplikace Najít iPhone.
- Dokážete zajistit, aby uživatel mohl zařízení používat ke své práci, a zároveň budete vědět, že když bude nutné zařízení použít k jinému účelu, budete ho moct vyřadit nebo odemknout.

## <a name="before-you-start"></a>Než začnete
Než budete moct Zámek aktivace na zařízeních zakázat, je potřeba, abyste je povolili pomocí následujících pokynů:

1. Nakonfigurujte profil omezení zařízení Intune pro iOS/iPadOS s použitím informací v tématu [jak nakonfigurovat nastavení omezení zařízení](../configuration/device-restrictions-configure.md).
2. V [Nastavení omezení pro zařízení s iOS/iPadOS](../configuration/device-restrictions-ios.md)v části **Obecné** nastavení povolte možnost **zámek aktivace**.
3. Uložte profil a [přiřaďte ho](../configuration/device-profile-assign.md) k zařízením, na kterých chcete spravovat zámek aktivace zakázat.


## <a name="how-to-use-disable-activation-lock"></a>Jak používat Disable Zámek aktivace

>[!IMPORTANT]
>Když Zámek aktivace v zařízení zakážete, je při spuštění aplikace Najít iPhone automaticky použita nová Zámek aktivace. Z tohoto důvodu **byste měli mít před provedením tohoto postupu zařízení fyzicky u sebe**.

Akce **zakázat zámek aktivace** vzdálené zařízení v Intune odebere zámek aktivace ze zařízení se systémem iOS/iPadOS, aniž by bylo nutné použít Apple ID a heslo uživatele. Když Zámek aktivace zakážete, zařízení se znovu zapne Zámek aktivace při spuštění aplikace Najít iPhone. Zakažte Zámek aktivace jenom v případě, že máte fyzický přístup k zařízení.

1. Přihlaste se k [centru pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
3. V okně **Intune** vyberte **Zařízení**.
4. V okně **Zařízení** vyberte **Všechna zařízení**.
5. V seznamu zařízení, která spravujete, vyberte vzdálenou akci **zakázat zámek aktivace** zařízení.
6. Přejděte do části hardware zařízení a potom zkopírujte hodnotu **kód pro obejití zámek aktivace** v části **podmíněný přístup**.

    >[!NOTE]
    >Před vymazáním zařízení si kód zkopírujte. Když nastavení zařízení obnovíte před zkopírováním kódu, kód se z Azure odebere.

7. Přejděte do okna zařízení **Přehled** a pak vyberte **Vymazat**.
8. Jakmile se zařízení obnoví, zobrazí se výzva k zadání *Apple ID* a *hesla*. Pole *ID* nechte prázdné a jako *heslo* zadejte **kód pro překonání zámku**. Tímto se účet odebere ze zařízení. 


## <a name="next-steps"></a>Další kroky

Stav požadavku na odemčení můžete zkontrolovat na stránce podrobností pro dané zařízení v úloze **Spravovat zařízení**.
