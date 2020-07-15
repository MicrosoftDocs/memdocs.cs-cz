---
title: Upgrade zařízení s Windows na jinou verzi
titleSuffix: Configuration Manager
description: Pomocí Configuration Manager můžete automaticky upgradovat zařízení s Windows 10 na jinou edici Windows.
ms.date: 07/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7a82a635eafcc0ecb5251457db9d4fbb301fce33
ms.sourcegitcommit: 1edcfb3ce4350ba1a6f36a6150e86301d35c631b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/15/2020
ms.locfileid: "86390836"
---
# <a name="upgrade-windows-devices-to-a-new-edition-with-configuration-manager"></a>Upgrade zařízení s Windows na novou edici pomocí Configuration Manager

*Platí pro: Configuration Manager (Current Branch)*

**Zásady upgradu edice** umožňují automaticky upgradovat zařízení s Windows 10 na jinou edici.

Podporují se tyto možnosti upgradu:

- Z Windows 10 Pro na Windows 10 Enterprise
- Z Windows 10 Home na Windows 10 Education
- Z Windows 10 Mobile na Windows 10 Mobile Enterprise

Zařízení musí spustit klientský software Configuration Manager. Zařízení spravovaná pomocí místní správy mobilních zařízení [(MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) ) se nepodporují.

## <a name="before-you-start"></a>Než začnete

Než začnete s upgradem zařízení na nejnovější verzi, Projděte si následující požadavky:  

- Pro desktopové edice Windows 10: platný kód Product Key pro novou verzi Windows ve všech zařízeních, na která tato zásada cílíte. Tento kód Product Key může být klíč k vícenásobné aktivaci (MAK) nebo obecný multilicenční klíč (GVLK). GVLK se také označuje jako klíč pro nastavení klienta služby správy klíčů (KMS). Další informace najdete v tématu [plánování aktivace multilicence](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Seznam klíčů pro instalaci klienta služby správy klíčů najdete v [příloze a](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) v příručce k aktivaci Windows serveru. <!--496871-->  

- Pro Windows 10 Mobile: soubor s licencí XML z Microsoft Volume Licensing Service Center (VLSC). Tento soubor obsahuje informace o licencích pro novou verzi Windows ve všech zařízeních, na která tato zásada cílíte. Stáhněte si soubor ISO pro **Windows 10 Mobile Enterprise**, který obsahuje kód XML pro licencování.<!-- SCCMDocs#2033 -->

- Pokud chcete spravovat tento typ zásad, musíte být v roli zabezpečení **správce s úplnými oprávněními** Configuration Manager.

## <a name="configure-the-policy"></a>Konfigurace zásad  

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte položku **Nastavení dodržování předpisů**a vyberte uzel **upgrade edice Windows 10** .  

2. Na kartě **Domů** na pásu karet ve skupině **vytvořit** vyberte možnost **vytvořit zásadu upgradu edice**.  

3. Vyberte **vytvořit zásadu**.  

4. Na stránce **Obecné** v **průvodci vytvořením zásad upgradu edice**zadejte následující informace:  

    - **Název** – zadejte název pro zásady upgradu edice  

    - **Popis** (volitelný) – volitelně zadejte popis zásady, který vám pomůže ho identifikovat v konzole Configuration Manager.  

    - **SKU pro upgrade zařízení na** – v rozevíracím seznamu vyberte cílovou edici Windows 10 Desktop nebo Windows 10 Mobile.  

    - **Informace o licenci** – vyberte jednu z následujících možností:  

        - **Kód Product Key** – zadejte platný kód Product Key pro cílovou edici Windows 10 Desktop.  

            > [!NOTE]  
            > Až vytvoříte zásady obsahující kód Product Key, nebudete moct kód Product Key později upravit. Configuration Manager skryje klíč z bezpečnostních důvodů. Pokud chcete kód Product Key změnit, zadejte znovu celý klíč.  

        - **Soubor s licencí** – zvolte **Procházet** a zvolte platný soubor s licencí ve formátu XML. Configuration Manager používá tento licenční soubor k upgradu zařízení s Windows 10 Mobile.  

5. Dokončete průvodce.  

## <a name="deploy-the-policy"></a>Nasazení zásady  

1. V konzole Configuration Manager otevřete pracovní prostor **prostředky a kompatibilita** , rozbalte položku **Nastavení dodržování předpisů**a vyberte uzel **upgrade edice Windows 10** .  

2. Vyberte zásadu upgradu edice Windows 10, kterou chcete nasadit. Na kartě **Domů** na pásu karet ve skupině **nasazení** vyberte **nasadit**.  

3. Vyberte kolekci zařízení, do které chcete zásady nasadit.

4. Vyberte plán, podle kterého klient vyhodnocuje zásady.

5. Dokončete průvodce.

## <a name="next-steps"></a>Další kroky

Monitorujte toto nasazení v uzlu **nasazení** pracovního prostoru **monitorování** . Pokud se zobrazí chyby indikující neúspěšné nasazení, například:

- **Neplatí pro toto zařízení.**
- **Převod datového typu se nepodařil.**

Tyto chyby neznamená, že nasazení selhalo. Ověřte u cílového zařízení, že upgrade proběhl úspěšně.

Jakmile klient vyhodnotí cílovou zásadu, použije se upgrade během dvou hodin. [Některé verze systému Windows](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades) mohou v daném okamžiku vyžadovat restart. Ujistěte se, že budete informovat všechny uživatele, na které zásadu nasazujete, nebo naplánovat, aby se zásady spouštěly mimo pracovní dobu uživatelů.

Pokud se v **DcmWmiProvider. log** v klientovi zobrazí následující chyba, ověřte, že používáte správný klíč pro svůj scénář aktivace. Další informace najdete v části [než začnete](#before-you-start) . Pokud pro aktivaci používáte službu správy klíčů (KMS), ujistěte se, že používáte [instalační klíč klienta služby správy klíčů](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`

## <a name="see-also"></a>Viz také

- [Plánování aktivace multilicence](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client)

- [Upgrade edice Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-edition-upgrades)

- [Upgradovat edice Windows 10 nebo zapínat na zařízeních v režimu S použitím Microsoft Intune](https://docs.microsoft.com/intune/edition-upgrade-configure-windows-10)
