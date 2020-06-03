---
title: Nasazení mnoha profilů OEMConfig do zařízení Zebra pomocí Microsoft Intune – Azure | Microsoft Docs
description: Pomocí Microsoft Intune můžete vytvořit a nasadit několik profilů konfigurace zařízení OEMConfig na zařízeních Zebra se systémem Android Enterprise. K uspořádání profilů použijte akce a kroky zebra.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a38c445018200d9fe80db19142f123aba783b60
ms.sourcegitcommit: 8a023e941d90c107c9769a1f7519875a31ef9393
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/03/2020
ms.locfileid: "84311152"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>Nasazení několika profilů OEMConfig do zařízení Zebra v Microsoft Intune

V Microsoft Intune použijte OEMConfig k přizpůsobení nastavení pro zařízení s Androidem Enterprise určených výrobcem OEM. Tato nastavení jsou specifická pro výrobce zařízení a nasazují se pomocí konfiguračních profilů v Intune.

Na zařízeních Zebra můžete ke stejnému zařízení nasadit nebo přiřadit víc profilů. Stávající profily OEMConfig můžou tuto funkci použít při příští synchronizaci zařízení s Intune.

Tato funkce platí pro:

- Zebra zařízení se systémem Android Enterprise

Další informace o OEMConfig, včetně toho, co dělá a jak ho používat, najdete v tématu [konfigurační profil OEMConfig](android-oem-configuration-overview.md).

Tento článek popisuje nasazení OEMConfig několika profilů do zařízení Zebra, popisuje řazení a používání funkcí vytváření sestav v Microsoft Intune.

## <a name="prerequisites"></a>Požadavky

Vytvořte [konfigurační profil OEMConfig](android-oem-configuration-overview.md).

## <a name="use-multiple-profiles"></a>Použít více profilů

Na zařízeních Zebra můžete mít každé zařízení současně spoustu profilů. Tato funkce umožňuje rozdělit nastavení Zebra OEMConfig na menší profily. Vytvořte například základní profil, který má vliv na všechna zařízení. Pak vytvořte další profily, které konfigurují nastavení specifická pro zařízení.

Zebra schéma OEMConfig také používá **Akce**. Akce jsou operace, které se spouštějí na zařízení. Nekonfigurují žádná nastavení. Pomocí těchto akcí můžete spustit stažení souboru, vymazat schránku a další. Úplný seznam podporovaných akcí najdete v [dokumentaci k Zebra](https://techdocs.zebra.com/oemconfig/10-0/about/) (otevření webu Zebra).

Například vytvoříte profil Zebra OEMConfig, který na zařízení aplikuje některá nastavení. Jiný profil Zebra OEMConfig obsahuje akci, která vymaže schránku. Přiřadíte první profil ke skupině zařízení zebra. Později musíte vymazat schránku na těchto zařízeních. Druhý profil přiřadíte ke stejné skupině zařízení, aniž byste změnili první profil. Schránka zařízení se vymazala bez opětovného odeslání nebo ovlivnění nastavení konfigurace vytvořená v prvním profilu.

V jiném příkladu jste přiřadili profil OEMConfig, který nakonfiguroval některá nastavení zařízení zebra. V poslední době uživatelé nahlásí problémy se specifickou aplikací a chcete vymazat mezipaměť aplikace. Vytvořte nový profil OEMConfig, který obsahuje jenom akci vymazat mezipaměť. Přiřaďte profil k zařízením, která ho potřebují.

## <a name="ordering"></a>Řazení

U několika profilů na každém zařízení není zaručeno pořadí, v jakém se profily nasazují. Toto chování je omezení Google Play. Chcete-li spustit operace v sekvenci, můžete použít [funkci kroku transakce Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/) (otevře web Zebra). 

Chcete-li vytvořit souhrn, pokud se jedná o záležitosti, použijte [funkci kroku transakce Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/) (otevře web Zebra). Pokud se vám pořadí nezáleží, použijte víc profilů Intune. 

Pojďme se podívat na několik příkladů:

- Chcete zapnout Bluetooth pro všechna nově zaregistrovaná zařízení Zebra před konfigurací jakýchkoli dalších nastavení na těchto zařízeních. Chcete-li spustit operace v sekvenci, použijte funkci **kroků** ve schématu zebra.

  Vytvořte jeden profil Intune, který má dva kroky transakce. První krok zahrnuje nastavení Bluetooth a druhý krok nakonfiguruje ostatní nastavení. Když aplikace Zebra OEMConfig obdrží profil, spustí postup v uvedeném pořadí.

  Další informace najdete v tématu [postup transakce Zebra](https://techdocs.zebra.com/oemconfig/10-0/mc/) (otevření webu Zebra).

- Chcete, aby všechna zařízení Zebra zobrazovala čas ve 24hodinovém formátu. U některých z těchto zařízení je třeba vypnout fotoaparát. Nastavení času a kamery nejsou na sobě navzájem závislé.

  Vytvořte dva profily Intune:

  - **Profil 1**: zobrazuje čas ve 24hodinovém formátu. V pondělí se tento profil přiřadí ke skupině **všechna zařízení Zebra AE** .
  - **Profil 2**: vypne fotoaparát. V úterý je tento profil přiřazen ke skupině **zařízení Zebra AE** .

  Ve středu zaregistrujete 10 nových zařízení Zebra do Intune. Profil 1 a profil 2 jsou přiřazeny. Jakmile se nová zařízení synchronizují s Intune, obdrží profily. Zařízení mohou profil 2 získat před profilací 1.

## <a name="enhanced-reporting"></a>Rozšířené vytváření sestav

Nasadíte profil a spustí se na zařízení aplikace Zebra OEMConfig. Aplikace Zebra OEMConfig hlásí stav profilu do Intune. V centru pro správu Správce koncových bodů můžete zobrazit stav nasazených profilů OEMConfig a všechny chyby nebo upozornění.

1. Otevřete [Centrum pro správu služby Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Vyberte profil Zebra OEMConfig > **monitorovat**  >  **stav zařízení**. Tato možnost zobrazuje zařízení, která mají přiřazený profil OEMConfig.
3. Vyberte zařízení > **Konfigurace zařízení** > vyberte profil Zebra OEMConfig. Tato možnost zobrazuje nastavení profilu, které bylo úspěšné nebo neúspěšné.

    Vyberte řádek, který selhal. Zobrazí se podrobnosti, které obsahují další informace o tom, proč došlo k chybě.

## <a name="next-steps"></a>Další kroky

- Přečtěte si další informace o [konfiguračních profilech OEMConfig](android-oem-configuration-overview.md).
- U Správce zařízení s Androidem nakonfigurujte [rozšíření mobility (MX)](android-zebra-mx-overview.md).
- [Monitorujte stav profilu](device-profile-monitor.md).
