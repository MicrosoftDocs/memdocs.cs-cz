---
title: Instalace rolí systému lokality
titleSuffix: Configuration Manager
description: Přidejte role systému lokality do stávajícího nebo nového serveru systému lokality v lokalitě.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 30b57de75e637aa083070832783647b8ad35b4a7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700527"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>Nainstalovat role systému lokality pro Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Existují dvě metody v konzole Configuration Manager pro instalaci rolí systému lokality:

- **Přidat role systému lokality**: Přidat role systému lokality na existující server systému lokality v lokalitě.

- **Vytvoření serveru systému lokality**: zadejte nový server jako server systému lokality a pak nainstalujte jednu nebo více rolí. Tato metoda je stejná jako při **Přidání rolí systému lokality**s výjimkou první stránky. Nejdřív zadejte název serveru a lokality, do které ho chcete nainstalovat.

> [!TIP]
> Při instalaci role na vzdáleném počítači Configuration Manager přidá účet počítače vzdáleného počítače do místní skupiny na serveru lokality.
>
> Když nainstalujete lokalitu na řadič domény, skupina na serveru lokality je skupina domény místo místní skupiny. V takovém případě role vzdáleného systému lokality okamžitě nefunguje. Systémový server lokality se musí restartovat, nebo můžete aktualizovat lístek protokolu Kerberos pro účet počítače vzdáleného serveru. Další informace najdete v tématu [používané účty](../../../plan-design/hierarchy/accounts.md).

Než nainstalujete roli systému lokality, Configuration Manager zkontroluje cílový počítač, aby se ujistil, že splňuje požadavky pro vybrané role.

Ve výchozím nastavení platí, že když Configuration Manager nainstaluje roli systému lokality, nainstaluje soubory na první dostupnou diskovou jednotku s formátem NTFS, která má nejvíce dostupného volného místa na disku. Chcete-li zabránit Configuration Manager instalaci na konkrétní jednotky, před instalací serveru systému lokality vytvořte v kořenovém adresáři jednotky prázdný soubor s názvem **NO_SMS_ON_DRIVE. SMS** .

Pro instalaci rolí používá Configuration Manager **účet instalace systému lokality** . Tento účet zadáte při instalaci role. Ve výchozím nastavení je tento účet účet místního systému počítače serveru lokality. Účet uživatele domény můžete zadat jako účet instalace systému lokality. Další informace najdete v tématu [účty – účet instalace systému lokality](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

## <a name="install-roles-on-an-existing-site-system-server"></a><a name="bkmk_addrole"></a> Instalace rolí na existující server systému lokality

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality**a vyberte uzel **servery a role systému lokality** . Vyberte existující server systému lokality, na kterém chcete nainstalovat nové role systému lokality.

1. Na pásu karet na kartě **Domů** ve skupině **Server** vyberte **Přidat role systému lokality**.

1. Na stránce **Obecné** zkontrolujte nastavení.

    > [!TIP]
    >  Pokud chcete získat přístup k roli systému lokality z Internetu, ujistěte se, že zadáváte plně kvalifikovaný název domény (FQDN) pro Internet.

1. Pokud role na tomto serveru vyžadují internetový proxy server, zadejte na stránce **proxy** serveru nastavení proxy server. Další informace najdete v tématu [Podpora proxy serveru](../../../plan-design/network/proxy-server-support.md).

1. Na stránce **Výběr role systému** vyberte role systému lokality, které chcete přidat.

1. Dokončete průvodce. Pro konkrétní role se můžou zobrazit další stránky. Další informace najdete v tématu [Možnosti konfigurace pro role systému lokality](configuration-options-for-site-system-roles.md).

> [!TIP]
> Rutina **New-CMSiteSystemServer**prostředí Windows PowerShell provádí stejnou funkci jako tento postup. Další informace najdete v tématu [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="install-roles-on-a-new-site-system-server"></a><a name="bkmk_createnew"></a> Instalovat role na nový server systému lokality

1. V konzole Configuration Manager otevřete pracovní prostor **Správa** . Rozbalte položku **Konfigurace lokality**a vyberte uzel **servery a role systému lokality** .

1. Na pásu karet na kartě **Domů** ve skupině **vytvořit** vyberte možnost **vytvořit server systému lokalit**.

1. Na stránce **Obecné** zadejte obecné nastavení systému lokality.

    > [!TIP]
    > Chcete-li získat přístup k nové roli systému lokality z Internetu, ujistěte se, že jste zadali internetový plně kvalifikovaný název domény.

1. Pokud role na tomto serveru vyžadují internetový proxy server, zadejte na stránce **proxy** serveru nastavení proxy server. Další informace najdete v tématu [Podpora proxy serveru](../../../plan-design/network/proxy-server-support.md).

1. Na stránce **Výběr role systému** vyberte role systému lokality, které chcete přidat.

1. Dokončete průvodce. Pro konkrétní role se můžou zobrazit další stránky. Další informace najdete v tématu [Možnosti konfigurace pro role systému lokality](configuration-options-for-site-system-roles.md).

> [!TIP]
> Rutina **New-CMSiteSystemServer**prostředí Windows PowerShell provádí stejnou funkci jako tento postup. Další informace najdete v tématu [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps).

## <a name="next-steps"></a>Další kroky

- [Možnosti konfigurace pro role systému lokality](configuration-options-for-site-system-roles.md)

- [Odebrat roli](../install/uninstall-sites-and-hierarchies.md#bkmk_role)