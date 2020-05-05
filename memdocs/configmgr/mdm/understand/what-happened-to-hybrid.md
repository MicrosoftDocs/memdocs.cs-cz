---
title: Co se stalo s hybridní správou MDM?
titleSuffix: Configuration Manager
description: Přečtěte si o vyřazení hybridní správy mobilních zařízení (MDM) v Configuration Manager
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e9e0da6d-bd5a-48d9-930a-e74b34b9286c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d07a014cdcb3f371a90028ec09be3c0c939b8424
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721812"
---
# <a name="what-happened-to-hybrid-mdm"></a>Co se stalo s hybridní správou MDM?

*Platí pro: Configuration Manager (Current Branch)*

> [!WARNING]
> Společnost Microsoft vyřazení hybridních služeb MDM od 1. září 2019. Všechna zbývající hybridní zařízení MDM nebudou dostávat zásady, aplikace ani aktualizace zabezpečení.

## <a name="remove-hybrid-mdm"></a>Odebrat hybridní MDM

Pokud váš Configuration Manager web má Microsoft Intune předplatné, je potřeba ho odebrat.

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Cloud Services**a vyberte uzel **Microsoft Intune předplatné** . Odstraňte stávající předplatné Intune.

1. V **Průvodci odebráním Předplatného Microsoft Intune**vyberte možnost **Odebrání Microsoft Intune předplatného z Configuration Manager**a pak klikněte na **Další**.

1. Dokončete průvodce.

## <a name="deprecation-announcement"></a>Oznámení o zastarání

Následující Poznámka je původní oznámení o zastaralosti:

> [!NOTE]  
> Od 14. srpna 2018 je hybridní Správa mobilních zařízení [zastaralá funkce](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Od verze 1902 Intune, která se očekává na konci února 2019, noví zákazníci nemůžou vytvořit nové hybridní připojení.
> <!--Intune feature 2683117-->  
> Vzhledem k tomu, že služba Intune po dobu před rokem začíná, přidá stovky nových funkcí požadovaných pro zákazníky a špičkové služby na trhu. Teď nabízí mnohem více funkcí, než nabízí hybridní Správa mobilních zařízení (MDM). Intune v Azure poskytuje více integrovaných a zjednodušených administrativních prostředí pro potřeby vaší podnikové mobility.
>
> V důsledku toho většina zákazníků zvolí Intune v Azure prostřednictvím hybridní správy mobilních zařízení (MDM). Počet zákazníků, kteří používají hybridní MDM, se i nadále zkrátí, protože další zákazníci se přesunou do cloudu. Proto od 1. září 2019 vyřadí Microsoft hybridní nabídku služby MDM.
>
> Tato změna neovlivní místní Configuration Manager ani [spolusprávu pro zařízení s Windows 10](../../comanage/overview.md). Pokud si nejste jistí, jestli používáte hybridní správu mobilních zařízení (MDM), v konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Cloud Services**a vyberte **Microsoft Intune odběry**. Pokud máte nastavené předplatné Microsoft Intune, je váš tenant nakonfigurovaný pro hybridní MDM.
>
> **Co to pro mě znamená?**
>
> - Microsoft bude podporovat vaše hybridní využívání MDM po dobu příštího roku. Tato funkce bude i nadále získávat hlavní opravy chyb. Microsoft bude podporovat existující funkce pro nové verze operačního systému, jako je registrace v iOS 12. Pro hybridní MDM nebudou k dispozici žádné nové funkce.  
>
> - Pokud migrujete do Intune v Azure před koncem nabídky hybridních MDM, nemělo by to mít žádný dopad na koncového uživatele.  
>
> - Od 1. září 2019 už žádná zbývající hybridní zařízení MDM nebudou dostávat zásady, aplikace ani aktualizace zabezpečení.  
>
> - Licencování zůstává stejné. Licence Intune na Azure jsou součástí hybridní správy mobilních zařízení (MDM).  
>
> - Místní funkce MDM v Configuration Manager není zastaralá. Od verze Configuration Manager 1810 můžete použít místní MDM bez připojení Intune. Další informace najdete v tématu [připojení Intune už není potřeba pro nová místní nasazení MDM](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm).
>
> - Místní funkce podmíněného přístupu Configuration Manager je také zastaralá s hybridními MDM. Pokud používáte podmíněný přístup na zařízeních spravovaných pomocí klienta Configuration Manager, před migrací se ujistěte, že jsou chráněné.
>     1. Nastavení zásad podmíněného přístupu v Azure
>     2. Nastavení zásad dodržování předpisů na portálu Intune
>     3. Dokončete hybridní migraci a nastavte autoritu MDM na Intune.
>     4. Povolení spolusprávy
>     5. Přesunutí úlohy spolusprávy zásad dodržování předpisů do Intune
>
>     Další informace najdete v tématu [podmíněný přístup s spolusprávou](../../comanage/quickstart-conditional-access.md).
>
> **Jak se mám na tuto změnu připravit?**
>
> - Zahajte plánování migrace pro MDM z konzoly ConfigMgr do Azure. Tento proces prošl mnoha zákazníky, včetně Microsoft IT. Další informace najdete v této [případové studii Microsoftu](https://aka.ms/Intune_MSFT).  
>
> - Požádejte o pomoc svého partnera o záznamu nebo FastTrack. [FastTrack pro Microsoft 365](https://aka.ms/hybrid_fasttrack) můžou pomoct při migraci z hybridní správy MDM do Intune v Azure.
>
> Další informace najdete v [příspěvku na blogu podpory Intune](https://aka.ms/hybrid_notification).

## <a name="next-steps"></a>Další kroky

Další informace o podporovaných funkcích pro správu zařízení MDM najdete v následujících článcích:

- [Co je Microsoft Intune?](https://docs.microsoft.com/intune/what-is-intune)
- [Co je místní správa MDM?](manage-mobile-devices-with-on-premises-infrastructure.md)
- [Správa zařízení pomocí Exchange](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
