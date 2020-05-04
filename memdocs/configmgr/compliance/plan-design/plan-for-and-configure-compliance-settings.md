---
title: Plánování a konfigurace nastavení dodržování předpisů
titleSuffix: Configuration Manager
description: Přečtěte si o požadavcích a úlohách konfigurace pro práci s nastavením dodržování předpisů v Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73ccec4ca318b522c0714bc8e5cc89f6c8899edd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/21/2020
ms.locfileid: "81712152"
---
# <a name="plan-for-and-configure-compliance-settings-in-configuration-manager"></a>Plánování a konfigurace nastavení dodržování předpisů v Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

Než začnete pracovat s Configuration Manager nastavením dodržování předpisů, je nutné mít na starosti několik požadovaných požadavků a některé úlohy konfigurace, které budete muset provést.  

## <a name="prerequisites-for-compliance-settings"></a>Předpoklady pro nastavení dodržování předpisů  

|Požadavek|Další informace|  
|------------------|----------------------|  
|Pro vyhodnocení dodržování předpisů musí být povolená a nakonfigurovaná klientská Configuration Manager systému Windows.|Viz níže|  
|Pokud chcete používat sestavy, musíte pro vaši lokalitu nakonfigurovat jejich generování.|[Úvod do vytváření sestav](../../core/servers/manage/introduction-to-reporting.md)|  
|Požadovaná oprávnění zabezpečení.|Role zabezpečení **Správce nastavení dodržování předpisů** zahrnuje nezbytná oprávnění pro správu nastavení dodržování předpisů, položky konfigurace uživatelských dat a profilů a profilů vzdáleného připojení.<br /><br /> [Konfigurace správy na základě rolí](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Povolení a konfigurace nastavení dodržování předpisů (jenom pro počítače s Windows)  

Tento postup nakonfiguruje výchozí nastavení klienta pro nastavení dodržování předpisů a použije se pro všechny počítače ve vaší hierarchii. Pokud chcete toto nastavení použít jenom pro některé počítače, vytvořte vlastní nastavení klientského zařízení a přiřaďte ho ke kolekci obsahující počítače, pro které chcete nastavení dodržování předpisů použít. Další informace o tom, jak vytvořit vlastní nastavení zařízení, najdete v tématu [Postup konfigurace nastavení klienta](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Ostatní typy zařízení nevyžadují pro vyhodnocení nastavení dodržování předpisů žádnou speciální konfiguraci.  

1.  V konzole Configuration Manager klikněte na **Správa** > **Nastavení** > klienta**výchozí nastavení**.  
2.  Na kartě **Domů** ve skupině **Vlastnosti** klikněte na možnost **Vlastnosti**.  
3.  V dialogovém okně **Výchozí nastavení** klikněte na **Nastavení dodržování předpisů**.  
4.  Nakonfigurujte následující klientská nastavení pro nastavení dodržování předpisů:
    - **Povolit vyhodnocování dodržování předpisů u klientů** – nastavte na **hodnotu true** , pokud chcete vyhodnotit dodržování předpisů u klientských zařízení.
    - **Plánování vyhodnocení dodržování předpisů** – klikněte na **plán** , pokud chcete upravit výchozí plán vyhodnocení shody na klientských zařízeních.
    - **Povolit profily a data uživatelů** – tuto možnost povolte, pokud chcete vytvořit a nasadit položky konfigurace profilů a dat uživatele do počítačů se systémem Windows. Podrobnosti najdete v tématu [Vytvoření položek konfigurace profilů a dat uživatele](../deploy-use/create-remote-connection-profiles.md).
5. Kliknutím na **OK** zavřete dialogové okno **Výchozí nastavení** .  

Při příštím stažení zásad klienta se klientské počítače nakonfigurují tímto nastavením.  
