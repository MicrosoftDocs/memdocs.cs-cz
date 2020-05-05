---
title: Spojovací bod služby
titleSuffix: Configuration Manager
description: Přečtěte si o této Configuration Manager roli systému lokality a seznamte se s nimi a Naučte se využívat jejich rozsahy.
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d167ea14537d88c31ca3930614fc24d8ebc92a02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81721182"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>O spojovacím bodu služby v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Spojovací bod služby je role systému lokality, která poskytuje několik důležitých funkcí pro hierarchii. Než nastavíte spojovací bod služby, budete rozumět a plánujete jeho rozsah používání. Plánování použití může mít vliv na nastavení této role systému lokality:

- Stáhněte si aktualizace, které se vztahují k vaší Configuration Manager infrastruktuře. Na základě dat o využití, která nahráváte, jsou k dispozici pouze relevantní aktualizace vaší infrastruktury.

- Nahrajte data o využití ze své infrastruktury Configuration Manager. Můžete řídit úroveň nebo množství podrobností, které odešlete. Další informace najdete v tématu [úrovně a nastavení dat o využití](../install/setup-reference.md#bkmk_usage).

- Nasazení [brány pro správu cloudu](../../../clients/manage/cmg/plan-cloud-management-gateway.md) v Azure

- Synchronizace aplikací z [Microsoft Store pro firmy a vzdělávání](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)

- Zjišťování uživatelů a skupin v [Azure Active Directory (Azure AD)](about-discovery-methods.md#azureaddisc)

- Použití funkce [Desktop Analytics](../../../../desktop-analytics/overview.md) k získání přehledů o připravenosti na aktualizace a přípravu aplikací pro Windows 10

Každá hierarchie podporuje jednu instanci této role. Dá se nainstalovat jenom v lokalitě nejvyšší úrovně vaší hierarchie, což je lokalita centrální správy (CAS) nebo samostatná primární lokalita. Pokud rozbalíte samostatnou primární lokalitu do větší hierarchie, odinstalujte tuto roli z primární lokality a pak ji nainstalujte do certifikačních autorit.

## <a name="modes-of-operation"></a><a name="bkmk_modes"></a>Režimy provozu

Spojovací bod služby podporuje dva režimy činnosti:

- **Online**: spojovací bod služby automaticky kontroluje aktualizace každých 24 hodin. Stáhne nové aktualizace, které jsou dostupné pro vaši aktuální infrastrukturu a verzi produktu, a zpřístupní je v konzole Configuration Manager.

- **Offline**: spojovací bod služby se nepřipojuje ke cloudové službě Microsoftu. Chcete-li ručně importovat dostupné aktualizace, použijte [Nástroj pro připojení služby](../../manage/use-the-service-connection-tool.md).

### <a name="change-mode"></a>Režim změny

Pokud provedete změnu mezi online nebo offline režimem po instalaci spojovacího bodu služby, restartujte **SMS_DMP_DOWNLOADER** vlákno služby SMS_Executive. Restartováním tohoto vlákna se změna projeví. Pro restartování tohoto vlákna použijte Configuration Manager Service Manager.

> [!TIP]
> Můžete také restartovat službu SMS_Executive pro Configuration Manager, která restartuje většinu součástí lokality. Případně můžete počkat na naplánovanou úlohu, jako je zálohování lokality, která zastaví a restartuje službu SMS_Executive za vás.

Chcete-li použít Service Manager Configuration Manager k restartování SMS_DMP_DOWNLOADER vlákna:

1. V konzole Configuration Manager přejdete do pracovního prostoru **monitorování** , rozbalíte možnost **stav systému**a vyberete uzel **Stav součásti** . Na pásu karet klikněte na tlačítko **Start**a poté vyberte možnost **Configuration Manager Service Manager**.

1. V navigačním podokně portálu Service Manager rozbalte lokalitu, rozbalte položku **součásti**a pak zvolte součást, kterou chcete restartovat: **SMS_DMP_DOWNLOADER**.

1. Přejděte do nabídky **Komponenta** a klikněte na příkaz **dotaz**.

1. Potvrďte aktuální stav součásti. Pak přejděte do nabídky **Komponenta** a zvolte možnost **zastavit**.  

1. Spusťte **dotaz** na součást znovu a potvrďte, že byla zastavena. Pak zvolte akci **Spustit** součást a restartujte ji.

## <a name="remote-site-system-requirements"></a>Požadavky na systém vzdáleného webu

Při instalaci spojovacího bodu služby na server systému lokality, který je vzdálený od serveru lokality, nakonfigurujte následující požadavky:

- Počítačový účet serveru lokality musí být místní správce v počítači, který je hostitelem spojovacího bodu vzdálené služby.

- Nastavte server systému lokality, který je hostitelem této role, s [účtem instalace systému lokality](../../../plan-design/hierarchy/accounts.md#site-system-installation-account). Správce distribuce na serveru lokality používá účet instalace systému lokality k přenosu aktualizací ze spojovacího bodu služby.

## <a name="internet-access-requirements"></a><a name="bkmk_urls"></a>Požadavky na přístup k Internetu

Pokud vaše organizace omezuje síťovou komunikaci s Internetem pomocí brány firewall nebo proxy zařízení, je nutné povolit spojovacímu bodu služby přístup k internetovým koncovým bodům.

Další informace najdete v tématu [požadavky na přístup k Internetu](../../../plan-design/network/internet-endpoints.md#bkmk_scp).

## <a name="install"></a>Instalace

Když spustíte **instalační program** a nainstalujete lokalitu nejvyšší úrovně v hierarchii, můžete nainstalovat spojovací bod služby.

Po spuštění instalačního programu nebo při přeinstalaci role použijte průvodce **přidáním rolí systému lokality** nebo průvodce **vytvořením serveru systému lokality** . (Nainstalujte spojovací bod služby pouze v lokalitě nejvyšší úrovně ve vaší hierarchii.) Další informace najdete v tématu [Instalace rolí systému lokality](install-site-system-roles.md).

## <a name="move-the-role"></a><a name="bkmk_move"></a>Přesunutí role

<!-- SCCMDocs#922 -->
K dispozici je několik scénářů, ve kterých může být nutné přesunout spojovací bod služby na jiný server:

- [Obnovení](../../manage/recover-sites.md)
- [Vysoká dostupnost serveru lokality](site-server-high-availability.md)
- [Rozšíření lokality](../install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)

Po přesunutí spojovacího bodu služby ověřte všechny funkce webu. Například může být nutné obnovit tajný klíč pro všechna připojení k klientům Azure Active Directory (Azure AD). Další informace najdete v tématu [obnovení tajného klíče](azure-services-wizard.md#bkmk_renew).

## <a name="log-files"></a>Soubory protokolů

Chcete-li zobrazit informace o nahrávání do společnosti Microsoft, zobrazte **souboru Dmpuploader. log** na serveru, na kterém je spuštěn spojovací bod služby. Průběh stahování aktualizací najdete v **protokolu dmpdownloader. log**. Úplný seznam protokolů souvisejících se spojovacím bodem služby najdete v tématu [soubory protokolu – bod připojení služby](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog).

## <a name="next-steps"></a>Další kroky

Pomocí následujících vývojových diagramů pochopíte tok procesů a položky protokolu klíčů. Tento proces zahrnuje aktualizace ke stažení a replikaci aktualizací do jiných lokalit.

- [Vývojový diagram – stahování aktualizací](../../manage/download-updates-flowchart.md)

- [Vývojový diagram – replikace aktualizací](../../manage/update-replication-flowchart.md)
