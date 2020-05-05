---
title: Správa zařízení pomocí Exchange
titleSuffix: Configuration Manager
description: Správa mobilních zařízení pomocí konektoru systému Exchange Server v Configuration Manager.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08d92d5c09331d675dc679a374e1bbf81633748e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721924"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>Správa zařízení pomocí Exchange a Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Pokud máte mobilní zařízení, která se připojují k systému Exchange Server prostřednictvím protokolu ActiveSync, můžete ke správě těchto zařízení použít konektor systému Exchange Server v Configuration Manager. Konektor funguje s místním systémem Exchange Server nebo Exchange Online. Použijte konzolu Configuration Manager ke konfiguraci funkcí správy mobilních zařízení systému Exchange. Například vzdálené vymazání zařízení a řízení nastavení pro více serverů Exchange.

![Logický diagram konektoru Exchange serveru s Configuration Manager](media/configmgr-with-exchange.png)  

Když spravujete mobilní zařízení pomocí tohoto konektoru, nenainstaluje klienta Configuration Manager ani nezaregistruje zařízení přes MDM. V porovnání s těmito dalšími možnostmi jsou funkce správy systému Exchange Server omezené. Například nemůžete instalovat software ani používat položky konfigurace ke konfiguraci těchto zařízení. Další informace najdete v tématu [Výběr řešení správy zařízení pro Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md).  

## <a name="policies"></a>Zásady

Při použití konektoru Configuration Manager konfiguruje nastavení na mobilních zařízeních. Zařízení nepoužívají výchozí zásady poštovní schránky protokolu Exchange ActiveSync. Definujte nastavení, které chcete použít, do následujících skupin:

- **Obecné**
- **Heslo**
- **Správa e-mailů**
- **Zabezpečení**
- **Aplikace**

Ve skupině **heslo** můžete například nakonfigurovat následující nastavení:

- Zda mobilní zařízení vyžadují heslo
- Minimální délka hesla
- Složitost hesla
- Zda je povoleno obnovení hesla

Pokud ve skupině nakonfigurujete alespoň jedno nastavení, Configuration Manager spravuje všechna nastavení ve skupině pro mobilní zařízení. Pokud ve skupině nenakonfigurujete žádné nastavení, bude Exchange dál spravovat tato nastavení pro mobilní zařízení. Všechny zásady poštovní schránky protokolu Exchange ActiveSync, které nakonfigurujete na serveru Exchange a přiřadí se uživatelům, se pořád používají.

## <a name="access-rules-and-remote-actions"></a>Pravidla přístupu a vzdálené akce

Můžete také nakonfigurovat konektor systému Exchange Server tak, aby spravoval pravidla přístupu k Exchangi. Tato pravidla přístupu zahrnují mobilní zařízení Allow, Block nebo Quarantine. Mobilní zařízení můžete vzdáleně vymazat pomocí konzoly Configuration Manager a uživatelé můžou vzdáleně vymazat svoje mobilní zařízení pomocí katalogu aplikací.

Mobilní zařízení uživatele se v katalogu aplikací automaticky zobrazí, když je spravujete a server Exchange je místní. Aby se mobilní zařízení zobrazilo v katalogu aplikací při použití Exchange Online, nakonfigurujte ručně spřažení uživatelských zařízení. Další informace najdete v tématu [propojení uživatelů a zařízení pomocí spřažení uživatelských zařízení](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

> [!TIP]  
> Když se mobilní zařízení přenese na jiného uživatele, před tím, než nový vlastník nakonfiguruje svůj účet Exchange na zařízení, odstraňte mobilní zařízení z konzoly Configuration Manager.

## <a name="prerequisites"></a>Požadavky

> [!IMPORTANT]  
> Než nainstalujete tento konektor, potvrďte, že Configuration Manager podporuje vaši verzi Exchange. Další informace najdete v tématu [podporované konfigurace – konektor systému Exchange Server](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_ExSrvConOS).  

### <a name="permissions-to-configure-the-connector"></a>Oprávnění ke konfiguraci konektoru

Ke konfiguraci konektoru serveru Exchange Server v Configuration Manager potřebujete následující oprávnění zabezpečení:

- Přidání, úpravy a odstranění konektoru Exchange Serveru: oprávnění **Upravit** pro objekt **Lokalita** .  

- Konfigurace nastavení mobilního zařízení: oprávnění **ModifyConnectorPolicy** pro objekt **Lokalita** .  

Například integrovaná role **úplného správce** obsahuje tato požadovaná oprávnění.  

### <a name="permissions-to-manage-mobile-devices"></a>Oprávnění ke správě mobilních zařízení

Ke správě mobilních zařízení potřebujete následující oprávnění zabezpečení:  

- Vymazání mobilního zařízení: **Odstranit prostředek** pro objekt **Kolekce** .  

- Zrušení příkazu vymazání: **Upravit prostředek** pro objekt **Kolekce** .  

- Povolení a blokování mobilních zařízení: **Upravit prostředek** pro objekt **Kolekce** .  

Například integrovaná role **správce operací** zahrnuje tato požadovaná oprávnění.

Další informace najdete v tématu [Konfigurace správy na základě rolí](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="next-steps"></a>Další kroky

> [!div class="nextstepaction"]
> [Instalace a konfigurace softwaru Exchange Connector](install-configure-exchange-connector.md)
