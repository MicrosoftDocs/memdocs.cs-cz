---
title: Možnosti ve verzi Technical Preview 1607
titleSuffix: Configuration Manager
description: Přečtěte si o funkcích dostupných v Technical Preview pro Configuration Manager verze 1607.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 73aac9e1bfb7b902a7db28ba4be00a2a02277324
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905695"
---
# <a name="capabilities-in-technical-preview-1607-for-configuration-manager"></a>Funkce ve verzi Technical Preview 1607 pro Configuration Manager

*Platí pro: Configuration Manager (větev Technical Preview)*

V tomto článku se seznámíte s funkcemi, které jsou k dispozici v Technical Preview pro Configuration Manager verze 1607. Tuto verzi můžete nainstalovat, abyste aktualizovali a přidali nové funkce na web Configuration Manager Technical Preview.      Před instalací této verze Technical Preview si Projděte úvodní téma, [Technical Preview pro Configuration Manager](../../core/get-started/technical-preview.md), abyste se seznámili se základními požadavky a omezeními pro používání Technical Preview, jak aktualizovat mezi verzemi a jak poskytnout zpětnou vazbu k funkcím ve verzi Technical Preview.    


**V následující části najdete nové funkce, které můžete s touto verzí vyzkoušet.**  

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a><a name="dmp_edition"></a>Vylepšení zásad upgradu edice Windows 10

V této verzi jsme provedli následující vylepšení těchto zásad:

* Zásady upgradu edice se teď dají používat s počítači s Windows 10, na kterých běží klient Configuration Manager kromě počítačů s Windows 10 jsou zaregistrované v Microsoft Intune.
* Z Windows 10 Professional můžete upgradovat na kteroukoli z platforem v průvodci, které jsou kompatibilní s vaším hardwarem.

[Přečtěte si další informace o zásadách upgradu edice Windows 10.](../../compliance/deploy-use/upgrade-windows-version.md)

### <a name="try-it-out"></a>Určitě to udělejte!

1. Použijte informace v [tématu Zásady upgradu existující edice](../../compliance/deploy-use/upgrade-windows-version.md) k vytvoření zásady upgradu edice.
2. Nasaďte tuto zásadu na počítač s Windows 10, na kterém běží klient Configuration Manager.
Až zásady dorazí do cílového počítače s Windows, počítač se během dvou hodin restartuje a nainstaluje se upgrade. V tuto chvíli nemůžete tento restart potlačit. Ujistěte se, že budete informovat všechny uživatele, na které zásadu nasazujete, nebo naplánovat, aby se zásady spouštěly mimo pracovní dobu uživatelů.

### <a name="known-issue-with-this-release"></a>Známý problém s touto verzí
V Configuration Manager nastavení klienta se můžou zobrazit nastavení **upgradu edice**. Tato nastavení nejsou v této verzi funkční. Pomocí výše uvedených pokynů upgradujte Windows 10 na novější verzi.

## <a name="customizable-branding-for-software-center-dialogs"></a>Přizpůsobitelné přidání údajů výrobce počítače v dialogových oknech v Centru softwaru

Vlastní branding pro Centrum softwaru byla představena ve verzi Configuration Manager 1602. Ve verzi Technical Preview 1607 je toto branding teď rozšířené na všechna přidružená dialogová okna a oznámení na hlavním panelu, aby poskytovala jednotnější prostředí pro uživatele centra softwaru.

### <a name="try-it-out"></a>Určitě to udělejte!

Vlastní branding pro Centrum softwaru se používá podle následujících pravidel:

1. Pokud není nainstalovaná role serveru lokality bodu webu katalogu aplikací, Centrum softwaru zobrazí název organizace uvedený v klientském nastavení **Počítačového agenta****Název organizace zobrazený v Centru softwaru**. Pokyny najdete v tématu [Postup konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).

2. Pokud je nainstalovaná role serveru lokality bodu webu katalogu aplikací, Centrum softwaru zobrazí název organizace a barvu zadanou ve vlastnostech role serveru lokality bodu webu katalogu aplikací. Další informace najdete v tématu [Možnosti konfigurace pro bod webu Katalog aplikací](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

3. Pokud je předplatné Microsoft Intune nakonfigurované a připojené k Configuration Manager prostředí, Centrum softwaru zobrazí název organizace, barvu a logo společnosti zadané ve vlastnostech předplatného Intune.

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Použití stejného síťového adaptéru pro více nasazení inicializovaných pomocí technologie PXE
Pokud ve verzi Technical Preview 1607 používáte adaptér sítě Ethernet k zobrazení imagí více zařízení (například ethernetového adaptéru USB, který používáte na více zařízeních), můžete povolit nové nastavení, které vám umožní zadat identifikátory hardwaru pro adaptéry Ethernet. Configuration Manager ignoruje identifikátory hardwaru v seznamu při provádění instalace PXE a registrace klienta.

Další informace o tomto problému najdete na [blogu týmu podpory pro Configuration Manager OSD](https://techcommunity.microsoft.com/t5/configuration-manager-archive/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in/ba-p/273721).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Povolení funkce pro správu duplicitních identifikátorů hardwaru  
1. V konzole Configuration Manager v části Přehled **správy**  >  **Overview**  >  **Cloud Services**  >  **Možnosti aktualizace a údržba**  >  **Features**.
2. V podokně zobrazení vyberte možnost **Správa duplicitních identifikátorů hardwaru**.
3. Na kartě **Domů** ve skupině **funkce** klikněte na **zapnout**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Přidejte identifikátory hardwaru pro Configuration Manager, které se mají ignorovat.  
1. V konzole Configuration Manager v části **Správa**  >  **Přehled**  >  **Konfigurace lokality**  >  **lokality**.
2. Na kartě **Domů** ve skupině **Lokality** klikněte na možnost **Nastavení hierarchie**.
3. Přejít na kartu **schválení klienta a konfliktní záznamy** .
4. Chcete-li přidat nové identifikátory hardwaru, klikněte na tlačítko **Přidat** v části **duplicitní identifikátory hardwaru** .
