---
title: Instalovat role pro místní správu mobilních zařízení (MDM)
titleSuffix: Configuration Manager
description: Nainstalujte požadované role systému lokality pro místní správu mobilních zařízení (MDM) v Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721854"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>Instalace rolí systému lokality pro místní správu mobilních zařízení (MDM) v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Configuration Manager místní správy mobilních zařízení (MDM) vyžaduje v Configuration Manager lokalitě následující role systému lokality:

- Bod registrace

- Zprostředkující bod registrace

- Distribuční bod

- Bod správy zařízení, což je bod správy, který je povolený pro mobilní zařízení

## <a name="requirements-and-limitations"></a>Požadavky a omezení

- Místní MDM vyžaduje, abyste povolili role systému lokality pro komunikaci pomocí protokolu HTTPS. Další informace najdete v tématu [nastavení certifikátů pro důvěryhodnou komunikaci v místní](set-up-certificates-on-premises-mdm.md)správě mobilních zařízení (MDM).

- Aktuální větev Configuration Manager podporuje jenom *intranetová* připojení ze zařízení do distribučních bodů a bodů správy zařízení pro místní správu mobilních zařízení (MDM). Pokud ale spravujete i počítače s macOS, klienti nástroje budou k těmto rolím potřebovat připojení k *Internetu* . Když konfigurujete distribuční bod a bod správy zařízení, použijte možnost pro **Povolení intranetových a internetových připojení**.

- Distribuční body, které nakonfigurujete pro připojení k intranetu, vyžadují, abyste pro ně nakonfigurovali hranice lokality. Configuration Manager podporuje pouze hranice rozsahu IPv4 pro místní správu mobilních zařízení (MDM). Další informace najdete v tématu [definice hranic lokality a skupin hranic](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

- Pokud používáte [repliky databáze](../../core/servers/deploy/configure/database-replicas-for-management-points.md) s bodem správy zařízení, nově zaregistrovaná zařízení se zpočátku nepodaří připojit. K tomuto selhání připojení dochází, protože replika databáze neobsahuje informace o nově zaregistrovaných zařízeních nezbytných pro úspěšné připojení. Repliky se synchronizují každých pět minut. Zařízení se nepodaří připojit po dobu prvních pěti minut po registraci, většinou se jedná o dva pokusy o připojení. Pak se zařízení úspěšně připojí.

## <a name="add-roles"></a>Přidání rolí

Pokud přidáváte místní správu mobilních zařízení (MDM) do lokality, která má většinu zařízení spravovaných pomocí klienta Configuration Manager, možná už máte v lokalitě nainstalované některé z těchto rolí. Například distribuční bod je společná role a bod správy zařízení je nutný ke správě zařízení macOS.

Další informace o tom, jak přidat role do lokality, najdete v tématu [Přidání rolí systému lokality](../../core/servers/deploy/configure/install-site-system-roles.md).

## <a name="configure-roles"></a>Konfigurace rolí

Nakonfigurujte nové nebo existující role pro správu mobilních zařízení. Postupujte podle následujících kroků a nakonfigurujte distribuční bod a bod správy zařízení tak, aby fungovaly správně pro místní správu mobilních zařízení (MDM):

1. V konzole Configuration Manager klikněte na pracovní prostor **Správa** , rozbalte položku **Konfigurace lokality**a vyberte uzel **servery a role systému lokality** .

1. Vyberte server systému lokality s distribučním bodem nebo bodem správy zařízení, který chcete konfigurovat. V seznamu vyberte server a pak v podokně podrobností role systému lokality vyberte roli **systému lokality** . Na pásu karet na kartě **role webového serveru** vyberte **vlastnosti**.

    > [!TIP]
    > Ve velkém webu můžete zobrazení oboru zobrazovat pouze servery s konkrétními rolemi. Když vyberete uzel **servery a role systému lokality** , na pásu karet na domovské značce vyberte **servery s rolí**. Pak ze seznamu rolí, které jsou aktuálně k dispozici v lokalitě, vyberte požadovanou roli.

    Na kartě **Obecné** ve **vlastnostech systému lokality**se ujistěte, že **název** je plně kvalifikovaný název domény (FQDN). Zavřete vlastnosti.

1. V seznamu konzola vyberte server s rolí místního distribučního bodu. V podokně podrobností role systému lokality vyberte roli **distribučního bodu** . Na pásu karet na kartě **role webového serveru** vyberte **vlastnosti**. Na kartě **komunikace** ve **vlastnostech distribučního bodu**:

    1. Vyberte **https**a vyberte možnost **povoluje jenom intranetové připojení**.

        > [!IMPORTANT]
        > Pokud spravujete i počítače s macOS pomocí klienta Configuration Manager, místo toho použijte možnost **Povolení připojení k intranetu a Internetu** .

    1. Povolte možnost **Povolit mobilním zařízením připojení k tomuto distribučnímu bodu**a pak vlastnosti zavřete.

1. Otevřete vlastnosti role systému lokality **bodu správy** .

    1. Na kartě **Obecné** vyberte **https**a vyberte možnost **povoluje pouze intranetové připojení**.

        > [!IMPORTANT]
        > Pokud spravujete i počítače s macOS pomocí klienta Configuration Manager, místo toho použijte možnost **Povolení připojení k intranetu a Internetu** .

    1. Povolte možnost **Povolit mobilním zařízením a počítačům Mac používat tento bod správy**a pak vlastnosti zavřete.

        > [!NOTE]
        > Tato možnost efektivně zapíná bod správy do bodu správy *zařízení* .  

## <a name="next-step"></a>Další krok

Po přidání a konfiguraci rolí pro správu mobilních zařízení nakonfigurujte servery jako důvěryhodné koncové body. Tento vztah důvěryhodnosti umožňuje rolím komunikaci se spravovanými zařízeními a jejich registraci.

> [!div class="nextstepaction"]
> [Nastavení certifikátů pro důvěryhodnou komunikaci](set-up-certificates-on-premises-mdm.md)
