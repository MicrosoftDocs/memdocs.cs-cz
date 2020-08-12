---
title: Samoobslužný portál BitLocker
titleSuffix: Configuration Manager
description: Jak používat Samoobslužný portál uživatele v Configuration Manager pro obnovení BitLockeru
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ad1f79bb439e0a426229680960092a5f0d8fb3c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129235"
---
# <a name="bitlocker-self-service-portal"></a>Samoobslužný portál BitLocker

*Platí pro: Configuration Manager (Current Branch)*

<!--3601034-->

Pokud nástroj BitLocker uzamkne zařízení uživatele, může po [instalaci samoobslužného portálu BitLockeru](setup-websites.md)nezávisle získat přístup k jejich počítačům. Samoobslužný portál nevyžaduje od pracovníků helpdesku žádnou pomoc.

[![Snímek obrazovky výchozího samoobslužného portálu BitLockeru](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> Pokud chcete získat obnovovací klíč ze samoobslužného portálu, uživatel se musí k počítači úspěšně přihlásit aspoň jednou. Toto přihlášení musí být pro zařízení místní, ne ve vzdálené relaci. V opačném případě musí kontaktovat oddělení technické podpory pro obnovení klíče. Správce helpdesku může k vyžádání obnovovacího klíče použít [web pro správu a monitorování](helpdesk-portal.md) .

BitLocker může zařízení uzamknout v následujících situacích:

- Uživatel zapomene heslo nástroje BitLocker nebo PIN kód.

- Došlo ke změně souborů operačního systému zařízení, systému BIOS nebo čipu TPM (Trusted Platform Module).

Požadavek na obnovení klíče BitLockeru z samoobslužného portálu:

1. Když BitLocker uzamkne zařízení, při spuštění se zobrazí obrazovka pro obnovení BitLockeru. Poznamenejte si ID obnovovacího klíče nástroje BitLocker 32 číslic.

1. V jiném počítači, například, na samoobslužném portálu ve webovém prohlížeči, použijte `https://webserver.contoso.com/SelfService` .

1. Přečtěte si a přijměte oznámení.

1. Do pole **ID obnovovacího klíče** zadejte prvních osm číslic identifikátoru obnovovacího klíče nástroje BitLocker. Pokud odpovídá více klíčům, zadejte všechny číslice 32.

1. Pro **důvod** této žádosti vyberte jednu z následujících možností:

    - Systém BIOS/TPM se změnil.
    - Změněný operační systém
    - KÓD PIN/heslo ke ztrátě

1. Vyberte **získat klíč**. Samoobslužný portál zobrazuje **obnovovací klíč bitlockeru**48 číslic.

1. Do obrazovky pro obnovení BitLockeru v počítači zadejte tento kód 48.

> [!NOTE]
> Samoobslužný portál BitLocker může být po určité době nečinnosti časový limit. Například po pěti minutách se může zobrazit upozornění s časovým limitem s 60 sekundou.
>
> ![Výstraha na Samoobslužný portál BitLocker – časové omezení](media/bitlocker-self-service-portal-timeout-warning.png)
>
> Pokud neodpovíte na odpočítávání, vyprší platnost relace.
>
> ![Stránka vypršení platnosti relace samoobslužného portálu BitLocker](media/bitlocker-self-service-portal-session-expired.png)
