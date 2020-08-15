---
title: Připojení tenanta Microsoft Endpoint Manageru
titleSuffix: Configuration Manager
description: Nahrajte zařízení Configuration Manager do cloudové služby a proveďte akce z centra pro správu.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 676ae288003b257802eea495c4101a95129eaf34
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/15/2020
ms.locfileid: "88251860"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a> Připojení tenanta Microsoft Endpoint Manageru: synchronizace zařízení a akce zařízení
<!--3555758 live 3/4/2020-->
*Platí pro: Configuration Manager (Current Branch)*

Microsoft Endpoint Manager je integrované řešení pro správu všech vašich zařízení. Společnost Microsoft spojuje Configuration Manager a Intune s jednou konzolou s názvem **Centrum pro správu Microsoft Endpoint Manager**.

Configuration Manager počínaje verzí 2002 můžete do cloudové služby nahrát vaše Configuration Manager zařízení a provádět akce z okna **zařízení** v centru pro správu.

## <a name="prerequisites"></a>Požadavky

- Účet, který je *globálním správcem* pro přihlašování při použití této změny. Další informace najdete v tématu [role správce služby Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - Připojování vytvoří v tenantovi služby Azure AD aplikaci třetí strany a instanční objekt první strany.
- Prostředí veřejného cloudu Azure.
- Uživatelské účty, které aktivují akce zařízení, mají následující požadavky:
   - Zjistila se [Azure Active Directory zjišťování uživatele](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) i [zjišťování uživatelů služby Active Directory](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
      - To znamená, že uživatelský účet musí být synchronizovaný objekt uživatele ve službě Azure AD.
   - Oprávnění **zahájit akci Configuration Manager** v části **vzdálené úlohy** v centru pro správu Microsoft Endpoint Manager.
- Pokud má lokalita centrální správy [vzdáleného zprostředkovatele](../core/plan-design/hierarchy/plan-for-the-sms-provider.md), postupujte podle pokynů pro [certifikační autority ve scénáři vzdáleného poskytovatele](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) v článku CMPivot. <!--7796824-->

## <a name="internet-endpoints"></a>Internetové koncové body

[!INCLUDE [Internet endpoints for tenant attach](../core/plan-design/network/includes/internet-endpoints-tenant-attach.md)]

## <a name="enable-device-upload-when-co-management-is-already-enabled"></a><a name="bkmk_edit"></a> Povolit nahrávání zařízení, když už je spoluspráva povolená

Pokud máte v tuto chvíli povolenou spolusprávu, použijte k povolení nahrávání zařízení vlastnosti spolusprávy. Pokud už spoluspráva není povolená, [použijte k tomu průvodce **konfigurací spolusprávy** ](#bkmk_config) , aby bylo možné místo toho nahrávat zařízení.

Pokud už spoluspráva je povolená, upravte vlastnosti spolusprávy tak, aby bylo možné nahrávat zařízení pomocí následujících pokynů:

1. V konzole pro správu Configuration Manager najdete v části **Administration**  >  **Přehled**správy  >  **Cloud Services**  >  **spoluspráva**.
1. Na pásu karet vyberte **vlastnosti** pro produkční zásady spolusprávy.
1. Na kartě **Konfigurovat nahrávání** vyberte **Odeslat do centra pro správu služby Microsoft Endpoint Manager**. Vyberte **Použít**.
   - Výchozím nastavením pro nahrávání zařízení jsou **všechna moje zařízení spravovaná pomocí koncového bodu Microsoft Configuration Manager**. V případě potřeby můžete nahrávání omezit na jednu kolekci zařízení.
1. Pokud chcete získat přehledy pro optimalizaci prostředí koncových uživatelů v rámci služby [Endpoint Analytics](../../analytics/overview.md), zaškrtněte možnost **Povolit službu Endpoint Analytics pro zařízení nahraná službě Microsoft Endpoint Manager** .

   [![Nahrávání zařízení do centra pro správu Microsoft Endpoint Manageru](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. Po zobrazení výzvy se přihlaste pomocí účtu *globálního správce* .
1. Výběrem **Ano** přijměte oznámení o **Vytvoření aplikace AAD** . Tato akce zřídí instanční objekt a vytvoří registraci aplikace služby Azure AD, která usnadňuje synchronizaci.
1. Kliknutím na **tlačítko OK** zavřete vlastnosti spolusprávy poté, co provedete změny.


## <a name="enable-device-upload-when-co-management-isnt-enabled"></a><a name="bkmk_config"></a> Povolit nahrávání zařízení, když není povolená spoluspráva

Pokud nemáte povolenou spolusprávu, budete k povolení nahrávání zařízení používat Průvodce **konfigurací spolusprávy** . Zařízení můžete nahrát bez povolení automatické registrace pro spolusprávu nebo přepínání úloh do Intune. Nahraje se všechna zařízení spravovaná Configuration Manager, která mají **Ano** ve sloupci **Client** . V případě potřeby můžete nahrávání omezit na jednu kolekci zařízení. Pokud je spoluspráva už ve vašem prostředí povolená, [upravte vlastnosti spolusprávy](#bkmk_edit) tak, aby místo nich bylo možné nahrávat zařízení.

Pokud spoluspráva není povolená, povolte nahrávání zařízení pomocí následujících pokynů:

1. V konzole pro správu Configuration Manager najdete v části **Administration**  >  **Přehled**správy  >  **Cloud Services**  >  **spoluspráva**.
1. Na pásu karet vyberte **Konfigurovat spolusprávu** a spusťte tak průvodce.
1. Na stránce registrace **tenanta** vyberte **AzurePublicCloud** pro vaše prostředí. Azure Government Cloud a Azure Čína 21Vianet se nepodporují.
1. Vyberte **Přihlásit se**. Přihlaste se pomocí účtu *globálního správce* .
1. Ujistěte se, že je na stránce registrace **tenanta** vybraná možnost **Odeslat do centra pro správu Microsoft Endpoint Manageru** .
   - Ujistěte se, že možnost **Povolit automatický zápis klientů pro spolusprávu** není zaškrtnutá, pokud nechcete povolit spolusprávu hned. Pokud chcete povolit spolusprávu, vyberte možnost.
   - Pokud povolíte spolusprávu společně s nahráváním zařízení, budete mít v průvodci další stránky k dokončení. Další informace najdete v tématu [Povolení spolusprávy](../comanage/how-to-enable.md).

   [![Průvodce konfigurací spolusprávy](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Klikněte na tlačítko **Další** a pak na **Ano** , pokud chcete přijmout oznámení o **Vytvoření aplikace AAD** . Tato akce zřídí instanční objekt a vytvoří registraci aplikace služby Azure AD, která usnadňuje synchronizaci.
     - Volitelně můžete importovat dřív vytvořenou aplikaci Azure AD během připojování klienta (počínaje verzí 2006). Další informace najdete v části [Import dřív vytvořené aplikace Azure AD](#bkmk_aad_app) .
1. Na stránce **Konfigurace nahrávání** vyberte Doporučené nastavení nahrávání zařízení pro **všechna moje zařízení spravovaná pomocí koncového bodu Microsoft Configuration Manager**. V případě potřeby můžete nahrávání omezit na jednu kolekci zařízení.
1. Pokud chcete získat přehledy pro optimalizaci prostředí koncových uživatelů v nástroji [Endpoint Analytics](../../analytics/overview.md) , zaškrtněte možnost **Povolení služby Endpoint Analytics pro zařízení nahraná v Microsoft Endpoint Manageru** .
1. Vyberte **Souhrn** pro kontrolu výběru a pak klikněte na tlačítko **Další**.
1. Po dokončení průvodce vyberte **Zavřít**.  

## <a name="perform-device-actions"></a>Provést akce zařízení

1. V prohlížeči přejděte na `endpoint.microsoft.com`
1. Vyberte **zařízení** a potom **všechna zařízení** zobrazí odeslaná zařízení. Pro nahraná zařízení se ve sloupci **Managed by** zobrazí **ConfigMgr** .
   [![Všechna zařízení v centru pro správu služby Microsoft Endpoint Manager](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Vyberte zařízení, na které se má načíst stránka s **přehledem** .
1. Vyberte některou z následujících akcí:
   - **Synchronizovat zásady počítače**
   - **Synchronizovat zásady uživatele**
   - **Cyklus hodnocení aplikace**

   [![Přehled zařízení v centru pro správu služby Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="import-a-previously-created-azure-ad-application-optional"></a><a name="bkmk_aad_app"></a> Importovat dřív vytvořenou aplikaci Azure AD (volitelné)
<!--6479246-->
*(Představené ve verzi 2006)*

Během [nového zprovoznění](#bkmk_config)může správce během připojování k tenantovi zadat dříve vytvořenou aplikaci. Nesdílejte ani nepoužívejte aplikace Azure AD v několika hierarchiích. Pokud máte více hierarchií, vytvořte pro každou z nich samostatné aplikace služby Azure AD.

Na stránce registrace **tenanta** v **Průvodci konfigurací spolusprávy**vyberte **volitelně import samostatné webové aplikace pro synchronizaci Configuration Manager klientských dat s centrem pro správu služby Microsoft Endpoint Manager**. Tento příkaz vás vyzve k zadání následujících informací pro vaši aplikaci Azure AD:

- Název tenanta Azure AD
- ID tenanta Azure AD
- Název aplikace
- ID klienta
- Tajný klíč
- Vypršení platnosti tajného klíče
- Identifikátor URI ID aplikace

### <a name="azure-ad-application-permissions-and-configuration"></a>Oprávnění a konfigurace aplikace Azure AD

Použití dříve vytvořené aplikace během připojování k tenantovi připojení vyžaduje následující oprávnění:

- Configuration Manager oprávnění pro mikroslužby:
   - CmCollectionData. Read
   - CmCollectionData. Write

- Microsoft Graph oprávnění:
   - Adresář. Read. všechna [oprávnění aplikací](https://docs.microsoft.com/graph/permissions-reference#application-permissions)
   - Adresář. Read. všechna [oprávnění delegovaného adresáře](https://docs.microsoft.com/graph/permissions-reference#directory-permissions)

- Zajistěte, aby byl pro aplikaci Azure AD vybraný **oprávnění udělení souhlasu správce pro tenanta** . Další informace najdete v tématu [udělení souhlasu správce v registrace aplikací](https://docs.microsoft.com/azure/active-directory/manage-apps/grant-admin-consent).

- Importovaná aplikace musí být nakonfigurovaná takto:
   - Registrováno pro **účty pouze v tomto organizačním adresáři**. Další informace najdete v tématu [Změna toho, kdo má přístup k vaší aplikaci](https://docs.microsoft.com/azure/active-directory/develop/quickstart-modify-supported-accounts#to-change-who-can-access-your-application).
   -  Má platný identifikátor URI a tajný kód aplikace.



## <a name="next-steps"></a>Další kroky

- [Registrace zařízení Configuration Manager do služby Endpoint Analytics](../../analytics/enroll-configmgr.md#bkmk_cm_enroll)
- Informace o tom, jak klient připojovat soubory protokolů, najdete v tématu [řešení potíží s připojením tenanta](troubleshoot.md).
