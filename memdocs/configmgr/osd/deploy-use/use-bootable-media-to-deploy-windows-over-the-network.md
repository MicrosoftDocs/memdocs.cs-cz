---
title: Použití spouštěcího média k nasazení Windows přes síť
titleSuffix: Configuration Manager
description: Pomocí nasazení spouštěcího média v Configuration Manager nasaďte operační systém při spuštění cílového počítače.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 999b5409-7e72-48d2-8554-4d44427ce383
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: db28c89e88ba08f92618c6d5fde1d1516b74afe4
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124752"
---
# <a name="use-bootable-media-to-deploy-windows-over-the-network-with-configuration-manager"></a>Použití spouštěcího média k nasazení Windows přes síť pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Spouštěcí médium zahrnuje pouze spouštěcí bitovou kopii a ukazatel na pořadí úkolů. Stáhne bitovou kopii operačního systému a další odkazovaný obsah ze sítě. Vzhledem k tomu, že spouštěcí médium neobsahuje mnoho obsahu, můžete aktualizovat pořadí úkolů a většinu obsahu, aniž byste museli nahradit médium.

Nasaďte operační systémy přes síť pomocí spouštěcího média v následujících scénářích:

- [Aktualizace existujícího počítače na novou verzi Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

- [Instalace nové verze Windows do nového počítače (holý počítač)](install-new-windows-version-new-computer-bare-metal.md)

- [Nahrazení existujícího počítače a nastavení přenosu](replace-an-existing-computer-and-transfer-settings.md)

Proveďte kroky v jednom ze scénářů nasazení operačního systému a potom použijte následující části k nasazení operačního systému pomocí spouštěcího média.

## <a name="configure-deployment-settings"></a>Konfigurace nastavení nasazení

Když použijete spouštěcí médium k zahájení procesu nasazení operačního systému, nakonfigurujte nasazení pořadí úkolů tak, aby byl operační systém pro médium k dispozici. Tuto možnost nastavte na stránce **nastavení nasazení** v nasazení. Pro nastavení **zpřístupnit pro následující** vyberte jednu z následujících možností:

- Configuration Manager klienty, média a technologie PXE

- Pouze média a technologie PXE

- Pouze média a technologie PXE (skryté)

Další informace naleznete v části [Deploy a task sequence](deploy-a-task-sequence.md).

## <a name="create-the-bootable-media"></a>Vytvoření spouštěcího média

Při vytváření spouštěcího média určete, zda se jedná o jednotku USB flash nebo sadu disků CD/DVD. Počítač, který spouští médium, musí podporovat možnost, kterou zvolíte jako spouštěcí jednotku. Další informace najdete v tématu [Vytvoření spouštěcího média](create-bootable-media.md).

## <a name="install-the-os-from-bootable-media"></a><a name="BKMK_Deploy"></a>Instalace operačního systému ze spouštěcího média

Chcete-li nainstalovat operační systém, vložte spouštěcí médium a potom počítač zapněte.

## <a name="support-for-cloud-based-content"></a>Podpora cloudového obsahu

<!--6209223-->

Počínaje verzí 2006 může spouštěcí médium stahovat cloudový obsah. Například odešlete klíč USB uživateli ve vzdálené kanceláři, který obnoví image zařízení. Nebo Office, který má místní server PXE, ale chcete, aby zařízení mohla upřednostňovat Cloud Services co nejvíce. Místo dalšího zdanění sítě WAN ke stažení velkého obsahu nasazení operačního systému, spouštěcí média a nasazení PXE teď můžou získávat obsah z cloudových zdrojů. Například brána pro správu cloudu (CMG), kterou povolíte pro sdílení obsahu.

> [!NOTE]
> Zařízení ještě potřebuje intranetové připojení k bodu správy.

Když je pořadí úloh spuštěno, stahuje obsah z cloudových zdrojů. Zkontrolujte **souboru Smsts. log** na klientovi.

### <a name="prerequisites"></a>Požadavky

- Ve **Cloud Services** skupině Povolte následující nastavení klienta: **Povolit přístup k distribučnímu bodu cloudu**. Ujistěte se, že je nastavení klienta nasazeno do cílových klientů. Další informace najdete v tématu [o nastavení klienta – cloudové služby](../../core/clients/deploy/about-client-settings.md#cloud-services).

- Pro skupinu hranic, ve které je klient nástroje:

  - Přidružte systémy lokality CMG nebo cloudového distribučního bodu s povoleným obsahem. Další informace najdete v tématu [Konfigurace hraniční skupiny](../../core/servers/deploy/configure/boundary-group-procedures.md#bkmk_config).

  - Povolte následující možnost: **preferovat cloudové zdroje prostřednictvím místních zdrojů**. Další informace najdete v tématu [Možnosti hraniční skupiny pro rovnocenné soubory ke stažení](../../core/servers/deploy/configure/boundary-groups.md#bkmk_bgoptions).

- Distribuujte obsah odkazovaný pořadím úkolů do CMG nebo cloudového distribučního bodu s povoleným obsahem.

## <a name="next-steps"></a>Další kroky

[Uživatelská prostředí pro nasazení operačního systému](../understand/user-experience.md#task-sequence-wizard)
