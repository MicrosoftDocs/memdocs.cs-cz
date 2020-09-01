---
title: Použití zásad Intune se zařízeními připojenými Configuration Manager klienta | Microsoft Docs
description: Nakonfigurujte připojení klienta Configuration Manager zařízení k centru pro správu Microsoft Endpoint Manageru, abyste mohli nasadit podporované zásady z Microsoft Intune na tato zařízení.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 5c3d5bd14efddc74e1898f374bbaac2aa962ebf7
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193661"
---
# <a name="configure-tenant-attach-to-support-endpoint-security-policies-from-intune"></a>Konfigurace připojení tenanta pro podporu zásad zabezpečení koncového bodu služby Intune

Když použijete scénář připojení klienta Configuration Manager, můžete nasadit zásady zabezpečení koncového bodu z Intune do zařízení, která spravujete pomocí Configuration Manager. Pokud chcete použít tento scénář, musíte nejdřív nakonfigurovat připojení tenanta pro Configuration Manager a povolit shromažďování zařízení z Configuration Manager pro použití s Intune. Po povolení použití kolekcí použijte centrum pro správu Microsoft Endpoint Manageru k vytvoření a nasazení zásad.

Configuration Manager zařízení, která jsou připojená k tenantovi, podporují následující typy zásad:

- Zásady antivirové ochrany Endpoint Security
- Zásady odezvy služby AD pro zjišťování koncových bodů zabezpečení koncového bodu

## <a name="requirements-to-use-intune-policy-for-tenant-attach"></a>Požadavky na použití zásad Intune pro připojení tenanta

Aby bylo možné podporovat používání zásad zabezpečení koncového bodu služby Intune s Configuration Managermi zařízeními, vyžaduje Configuration Manager prostředí následující konfigurace. [Pokyny k konfiguraci](#set-up-configuration-manager-to-support-intune-policies) jsou k dispozici v tomto článku:

### <a name="general-requirements-for-tenant-attach"></a>Obecné požadavky na připojení tenanta

- **Konfigurovat připojení tenanta** – pomocí scénáře *připojení tenanta* synchronizujete kolekce zařízení z Configuration Manager do centra pro správu Microsoft Endpoint Manager. Pak můžete použít Centrum pro správu k nasazení podporovaných zásad do těchto kolekcí.

  Připojení klienta se často konfiguruje se spolusprávou, ale můžete nakonfigurovat připojení tenanta sami.

- **Synchronizovat kolekce Configuration Manager** – když konfigurujete připojení tenanta, můžete vybrat kolekce Configuration Managerch zařízení, které se mají synchronizovat s centrem pro správu Microsoft Endpoint Manageru. Můžete se také vrátit později a upravit kolekce zařízení, které synchronizujete. Podporované zásady pro zařízení Configuration Manager se dají přiřadit jenom ke kolekcím, které jste synchronizovali.

  Po výběru kolekcí k synchronizaci je musíte povolit, aby je bylo možné použít se zásadami zabezpečení koncového bodu služby Intune.

- **Oprávnění pro Azure AD** – dokončení nastavení připojení klienta vyžaduje účet s oprávněním globálního správce k vašemu předplatnému Azure.

### <a name="specific-requirements-for-intune-endpoint-security-policies"></a>Specifické požadavky na zásady zabezpečení koncového bodu služby Intune

- **Zásady antivirové ochrany** (*Preview*):

  - **Configuration Manager** – podporují se následující prostředí:

    - **Configuration Manager aktuální větev verze 2006 nebo novější** – v této aktuální verzi větve se přidala podpora pro zásady antivirové ochrany Intune.
    <!--
    - **Configuration Manager technical preview 2007 or later** - Support for Intune antivirus policies was added with this technical preview version. -->

  - **Tenant pro Microsoft Defender Advanced Threat Protection** – váš tenant Microsoft Defender ATP musí být integrovaný do vašeho tenanta Microsoft Endpoint Manageru (předplatné Intune).  Viz [Použití ATP v programu Microsoft Defender](advanced-threat-protection.md) v dokumentaci k Intune.

- **Zjišťování koncových bodů a zásady odezvy**:

  - **Configuration Manager** – podporují se následující prostředí:

    - **Configuration Manager Technical preview 2003 nebo novější** – podpora zjišťování koncových bodů a zásad odezvy Intune se přidala ve verzi technical Preview 2003.

    - **Configuration Manager aktuální větev verze 2002 nebo novější** – pokud používáte Configuration Manager s verzí 2002, je nutné nainstalovat konzolovou aktualizaci **Configuration Manager 2002 hotfix (KB4563473)**. Tato aktualizace umožňuje podporu v Configuration Manager 2002 pro používání zásad zabezpečení koncového bodu.

  - **Tenant pro Microsoft Defender Advanced Threat Protection** – váš tenant Microsoft Defender ATP musí být integrovaný do vašeho tenanta Microsoft Endpoint Manageru (předplatné Intune).  Viz [Použití ATP v programu Microsoft Defender](advanced-threat-protection.md) v dokumentaci k Intune.

## <a name="set-up-configuration-manager-to-support-intune-policies"></a>Nastavení Configuration Manager pro podporu zásad Intune

Před nasazením zásad Intune pro Configuration Manager zařízení dokončete konfigurace popsané v následujících částech. Tyto konfigurace přiřadí vaše zařízení Configuration Manager s využitím ATP Microsoft Defender a umožňují jim pracovat se zásadami Intune.

Následující úkoly jsou dokončeny v konzole Configuration Manager. Pokud nejste obeznámeni s Configuration Manager, při provádění těchto úloh Spolupracujte se správcem Configuration Manager.

1. [Instalace aktualizace pro Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Povolení připojení tenanta](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Vybrat kolekce, které se mají synchronizovat](#task-3-select-collections-to-synchronize)
4. [Povolit shromažďování dat pro podporu zásad Intune](#task-4-enable-collections-for-endpoint-security-policies)

> [!TIP]
> Další informace o používání služby Microsoft Defender ATP s Configuration Manager najdete v následujících článcích v Configuration Managerm obsahu:
>
> - [Připojení klientů Configuration Manager k ochraně ATP v programu Microsoft Defender prostřednictvím centra pro správu Microsoft Endpoint Manageru](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Připojení tenanta Microsoft Endpoint Manageru: synchronizace zařízení a akce zařízení](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach)

### <a name="task-1-install-the-update-for-configuration-manager"></a>Úloha 1: instalace aktualizace pro Configuration Manager

Pokud používáte Configuration Manager aktuální větev verze 2002, nainstalujte následující konzolovou aktualizaci, která přidá podporu pro zásady zabezpečení koncového bodu, které nasazujete z centra pro správu Microsoft Endpoint Manageru.

**Podrobnosti aktualizace**:

- **Oprava hotfix Configuration Manager 2002 (KB4563473)**

Pokud chcete nainstalovat tuto aktualizaci, postupujte podle pokynů v části [instalace konzolových aktualizací](../../configmgr/core/servers/manage/install-in-console-updates.md) v dokumentaci k Configuration Manager.

Až aktualizaci nainstalujete, vraťte se sem, abyste mohli pokračovat v konfiguraci prostředí pro podporu zásad zabezpečení koncových bodů z centra pro správu Microsoft Endpoint Manageru.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Úloha 2: Konfigurace tenanta pro připojení a synchronizaci kolekcí

Když se připojíte ke klientovi, určete kolekce zařízení z nasazení Configuration Manager pro synchronizaci s centrem pro správu Microsoft Endpoint Manageru. Po synchronizaci kolekcí použijte centrum pro správu k zobrazení informací o těchto zařízeních a nasazení zásad zabezpečení koncového bodu z Intune.

Další informace o scénáři připojení klienta najdete v tématu [Povolení připojení tenanta](../../configmgr/tenant-attach/device-sync-actions.md) v obsahu Configuration Manager.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Povolit připojení tenanta, když není povolená spoluspráva

> [!TIP]
> Pomocí **Průvodce konfigurací spolusprávy** v konzole Configuration Manager můžete povolit připojení tenanta, ale nemusíte umožňovat spolusprávu.
>
> Pokud máte v plánu povolit spolusprávu, Seznamte se se spolusprávou, jejími požadavky a správou úloh, než budete pokračovat. Přečtěte si téma [co je spoluspráva?](../../configmgr/comanage/overview.md) v dokumentaci k Configuration Manager.

1. V konzole pro správu Configuration Manager najdete v části **Administration**  >  **Přehled**správy  >  **Cloud Services**  >  **spoluspráva**.
2. Na pásu karet klikněte na **Konfigurovat spolusprávu** a otevřete průvodce.
3. Na stránce registrace **tenanta** vyberte **AzurePublicCloud** pro vaše prostředí. Cloud Azure Government není podporovaný.
   1. Klikněte na **Přihlásit se**. Přihlaste se pomocí účtu *globálního správce* .

   2. Ujistěte se, že je na stránce pro **registraci tenanta** vybraná možnost **nahrajte do centra pro správu Microsoft Endpoint Manageru** .

   3. Odstraňte kontrolu z **Povolení automatického zápisu klientů pro spolusprávu**.

      Pokud je vybrána tato možnost, průvodce nabídne další stránky k dokončení nastavení spolusprávy. Další informace najdete v tématu [Povolení spolusprávy](../../configmgr/comanage/how-to-enable.md) v obsahu Configuration Manager.

     ![Konfigurovat připojení tenanta](./media/tenant-attach-intune/tenant-onboarding.png)

4. Klikněte na tlačítko **Další** a pak na **Ano** , pokud chcete přijmout oznámení o **Vytvoření aplikace AAD** . Tato akce zřídí instanční objekt a vytvoří registraci aplikace služby Azure AD, aby se usnadnila synchronizace kolekcí do centra pro správu služby Microsoft Endpoint Manager.

5. Na stránce **Konfigurace nahrávání** nakonfigurujte, které kolekce se mají synchronizovat. Můžete omezit konfiguraci na jednu nebo několik kolekcí zařízení nebo použít nastavení Doporučené nahrávání zařízení pro **všechna moje zařízení spravovaná službou Microsoft Endpoint Configuration Manager**.

   > [!TIP]
   > Můžete teď přeskočit výběr kolekce a později pomocí informací v následující úloze, úloze 3 nakonfigurovat, které kolekce se budou synchronizovat s centrem pro správu Microsoft Endpoint Manageru.

6. Kliknutím na **Souhrn** zkontrolujte výběr a pak klikněte na **Další**.

7. Po dokončení průvodce klikněte na tlačítko **Zavřít**.

   Připojení tenanta je teď nakonfigurované a vybrané kolekce se synchronizují do centra pro správu Microsoft Endpoint Manageru.

#### <a name="enable-tenant-attach-when-you-already-use-co-management"></a>Povolit připojení tenanta, když už používáte spolusprávu

1. V konzole pro správu Configuration Manager najdete v části **Administration**  >  **Přehled**správy  >  **Cloud Services**  >  **spoluspráva**.

2. Klikněte pravým tlačítkem na nastavení spolusprávy a vyberte **vlastnosti**.

3. Na kartě **Konfigurovat nahrávání** vyberte **Odeslat do centra pro správu služby Microsoft Endpoint Manager**. Klikněte na **Použít**.

   Výchozím nastavením pro nahrávání zařízení jsou **všechna moje zařízení spravovaná pomocí koncového bodu Microsoft Configuration Manager**. Můžete taky zvolit omezení konfigurace na jednu nebo několik kolekcí zařízení.

   ![Zobrazit kartu vlastnosti spolusprávy](./media/tenant-attach-intune/configure-upload.png)

   > [!TIP]
   > Můžete teď přeskočit výběr kolekce a později pomocí informací v následující úloze, úloze 3 nakonfigurovat, které kolekce se budou synchronizovat s centrem pro správu Microsoft Endpoint Manageru.

4. Po zobrazení výzvy se přihlaste pomocí účtu *globálního správce* .

5. Kliknutím na **Ano** přijměte oznámení o **Vytvoření aplikace AAD** . Tato akce zřídí instanční objekt a vytvoří registraci aplikace služby Azure AD, která usnadňuje synchronizaci.

6. Kliknutím na tlačítko **OK** zavřete vlastnosti spolusprávy poté, co provedete změny.

   Připojení tenanta je teď nakonfigurované a vybrané kolekce se synchronizují do centra pro správu Microsoft Endpoint Manageru.

### <a name="task-3-select-collections-to-synchronize"></a>Úloha 3: Vyberte kolekce, které chcete synchronizovat.

Když je nakonfigurované připojení tenanta, můžete vybrat kolekce, které se mají synchronizovat. Pokud jste ještě nesynchronizoval kolekce nebo potřebujete změnit konfiguraci těch, které synchronizujete, můžete upravit vlastnosti spolusprávy v konzole Configuration Manager.

#### <a name="select-collections"></a>Vybrat kolekce

1. V konzole pro správu Configuration Manager najdete v části **Administration**  >  **Přehled**správy  >  **Cloud Services**  >  **spoluspráva**.

2. Klikněte pravým tlačítkem na nastavení spolusprávy a vyberte **vlastnosti**.

3. Na kartě **Konfigurovat nahrávání** vyberte **Odeslat do centra pro správu služby Microsoft Endpoint Manager**. Klikněte na **Použít**.

   Výchozím nastavením pro nahrávání zařízení jsou **všechna moje zařízení spravovaná pomocí koncového bodu Microsoft Configuration Manager**. Můžete taky zvolit omezení konfigurace na jednu nebo několik kolekcí zařízení.

### <a name="task-4-enable-collections-for-endpoint-security-policies"></a>Úloha 4: povolení kolekcí pro zásady zabezpečení koncového bodu

Až nakonfigurujete kolekce, které se mají synchronizovat s centrem pro správu Microsoft Endpoint Manageru, povolte těmto kolekcím práci se zásadami zabezpečení koncového bodu. Když povolíte shromažďování zařízení pro práci se zásadami zabezpečení koncového bodu služby Intune, konfigurujete zařízení v těchto kolekcích tak, aby se připojila ke službě Microsoft Defender ATP.

#### <a name="enable-collections-for-use-with-endpoint-security-policies"></a>Povolení kolekcí pro použití se zásadami zabezpečení koncového bodu

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](includes/make-configmgr-collection-available-edr.md)]

## <a name="next-steps"></a>Další kroky

- [Nakonfigurujte zásady zabezpečení koncového bodu](endpoint-security-policy.md#create-an-endpoint-security-policy) pro *antivirovou* a *detekci a odpověď koncového bodu*.

- Přečtěte si další informace o [detekci a odezvě koncových bodů](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) v dokumentaci ke službě Microsoft Defender atp.