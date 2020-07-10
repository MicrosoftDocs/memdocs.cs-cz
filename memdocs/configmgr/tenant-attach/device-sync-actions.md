---
title: Připojení tenanta Microsoft Endpoint Manageru
titleSuffix: Configuration Manager
description: Nahrajte zařízení Configuration Manager do cloudové služby a proveďte akce z centra pro správu.
ms.date: 07/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: a9e97c74e4825dc49ce628b3ae176c55f4288966
ms.sourcegitcommit: 3806a1850813b7a179d703e002bcc5c7eb1cb621
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/09/2020
ms.locfileid: "86210316"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Připojení tenanta Microsoft Endpoint Manageru: synchronizace zařízení a akce zařízení
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


## <a name="internet-endpoints"></a>Internetové koncové body

- `https://aka.ms/configmgrgateway`
- `https://*.manage.microsoft.com` <!--7424742-->

## <a name="enable-device-upload"></a>Povolit nahrávání zařízení

- Pokud je v současné době povolená spoluspráva, [upravte vlastnosti spolusprávy](#bkmk_edit) tak, aby bylo možné nahrávat zařízení.
- Pokud nemáte povolenou spolusprávu, [pomocí průvodce **konfigurací spolusprávy** ](#bkmk_config) povolte nahrávání zařízení.
   - Zařízení můžete nahrát bez povolení automatické registrace pro spolusprávu nebo přepínání úloh do Intune.
- Nahraje se všechna zařízení spravovaná Configuration Manager, která mají **Ano** ve sloupci **Client** . V případě potřeby můžete nahrávání omezit na jednu kolekci zařízení.

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>Úprava vlastností spolusprávy, aby bylo možné nahrávat zařízení

Pokud máte aktuálně povolenou spolusprávu, upravte vlastnosti spolusprávy tak, aby bylo možné nahrávat zařízení pomocí následujících pokynů:

1. V konzole pro správu Configuration Manager najdete v části **Administration**  >  **Přehled**správy  >  **Cloud Services**  >  **spoluspráva**.
1. Klikněte pravým tlačítkem na nastavení spolusprávy a vyberte **vlastnosti**.
1. Na kartě **Konfigurovat nahrávání** vyberte **Odeslat do centra pro správu služby Microsoft Endpoint Manager**. Klikněte na **Použít**.
   - Výchozím nastavením pro nahrávání zařízení jsou **všechna moje zařízení spravovaná pomocí koncového bodu Microsoft Configuration Manager**. V případě potřeby můžete nahrávání omezit na jednu kolekci zařízení.
1. Pokud chcete získat přehledy pro optimalizaci prostředí koncových uživatelů v rámci služby [Endpoint Analytics](../../analytics/overview.md), zaškrtněte možnost **Povolit službu Endpoint Analytics pro zařízení nahraná službě Microsoft Endpoint Manager** .

   [![Nahrávání zařízení do centra pro správu Microsoft Endpoint Manageru](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. Po zobrazení výzvy se přihlaste pomocí účtu *globálního správce* .
1. Kliknutím na **Ano** přijměte oznámení o **Vytvoření aplikace AAD** . Tato akce zřídí instanční objekt a vytvoří registraci aplikace služby Azure AD, která usnadňuje synchronizaci.
1. Kliknutím na tlačítko **OK** zavřete vlastnosti spolusprávy poté, co provedete změny.


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>Použití Průvodce konfigurací spolusprávy k povolení nahrávání zařízení
Pokud nemáte povolenou spolusprávu, pomocí průvodce **konfigurací spolusprávy** povolte nahrávání zařízení. Zařízení můžete nahrát bez povolení automatické registrace pro spolusprávu nebo přepínání úloh do Intune. Pomocí následujících pokynů povolte nahrávání zařízení:

1. V konzole pro správu Configuration Manager najdete v části **Administration**  >  **Přehled**správy  >  **Cloud Services**  >  **spoluspráva**.
1. Na pásu karet klikněte na **Konfigurovat spolusprávu** a otevřete průvodce.
1. Na stránce registrace **tenanta** vyberte **AzurePublicCloud** pro vaše prostředí. Cloud Azure Government není podporovaný.
1. Klikněte na **Přihlásit se**. Přihlaste se pomocí účtu *globálního správce* .
1. Ujistěte se, že je na stránce registrace **tenanta** vybraná možnost **Odeslat do centra pro správu Microsoft Endpoint Manageru** .
   - Ujistěte se, že možnost **Povolit automatický zápis klientů pro spolusprávu** není zaškrtnutá, pokud nechcete povolit spolusprávu hned. Pokud chcete povolit spolusprávu, vyberte možnost.
   - Pokud povolíte spolusprávu společně s nahráváním zařízení, budete mít v průvodci další stránky k dokončení. Další informace najdete v tématu [Povolení spolusprávy](../comanage/how-to-enable.md).

   [![Průvodce konfigurací spolusprávy](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Klikněte na tlačítko **Další** a pak na **Ano** , pokud chcete přijmout oznámení o **Vytvoření aplikace AAD** . Tato akce zřídí instanční objekt a vytvoří registraci aplikace služby Azure AD, která usnadňuje synchronizaci.
1. Na stránce **Konfigurace nahrávání** vyberte Doporučené nastavení nahrávání zařízení pro **všechna moje zařízení spravovaná pomocí koncového bodu Microsoft Configuration Manager**. V případě potřeby můžete nahrávání omezit na jednu kolekci zařízení.
1. Pokud chcete získat přehledy pro optimalizaci prostředí koncových uživatelů v nástroji [Endpoint Analytics](../../analytics/overview.md) , zaškrtněte možnost **Povolení služby Endpoint Analytics pro zařízení nahraná v Microsoft Endpoint Manageru** .
1. Kliknutím na **Souhrn** zkontrolujte výběr a pak klikněte na **Další**.
1. Po dokončení průvodce klikněte na tlačítko **Zavřít**.  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>Kontrola nahrávání

1. Otevřete **CMGatewaySyncUploadWorker. log** z &lt; instalačního adresáře nástroje ConfigMgr> \Logs.
1. Čas další synchronizace je zaznamenán podle záznamů protokolu podobných `Next run time will be at approximately: 02/28/2020 16:35:31` .
1. V případě nahrávání zařízení vyhledejte položky protokolu podobné `Batching N records` . **N** je počet zařízení odeslaných do cloudu. 
1. Nahrávání probíhá každých 15 minut, než se změny projeví. Po nahrání změn může trvat dalších 5 až 10 minut, než se změny klienta zobrazí v centru pro **správu Microsoft Endpoint Manager**.

## <a name="perform-device-actions"></a>Provést akce zařízení

1. V prohlížeči přejděte na`endpoint.microsoft.com`
1. Vyberte **zařízení** a potom **všechna zařízení** zobrazí odeslaná zařízení. Pro nahraná zařízení se ve sloupci **Managed by** zobrazí **ConfigMgr** .
   [![Všechna zařízení v centru pro správu služby Microsoft Endpoint Manager](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Kliknutím na zařízení načtete jeho stránku s **přehledem** .
1. Klikněte na některou z následujících akcí:
   - **Synchronizovat zásady počítače**
   - **Synchronizovat zásady uživatele**
   - **Cyklus hodnocení aplikace**

   [![Přehled zařízení v centru pro správu služby Microsoft Endpoint Manager](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="known-issues"></a>Známé problémy

### <a name="specific-devices-dont-synchronize"></a>Konkrétní zařízení se nesynchronizují

<!--7099564-->
Je možné, že konkrétní zařízení, která jsou Configuration Manager klientech, se do této služby neodešlou.

**Ovlivněná zařízení:** Pokud je zařízení distribuční bod, který používá stejný certifikát PKI pro funkci distribučního bodu i jeho agenta klienta, nebude toto zařízení zahrnuto do synchronizace zařízení připojit klienta.

**Chování:** Při provádění připojení tenanta během fáze zprovoznění se provede Úplná synchronizace poprvé. Následné synchronizační cykly jsou rozdílové synchronizace. Jakákoli aktualizace ovlivněných zařízení způsobí odebrání zařízení z synchronizace.

## <a name="log-files"></a>Soubory protokolu
Použijte následující protokoly umístěné ve spojovacím bodu služby:

- **CMGatewaySyncUploadWorker. log**
- **CMGatewayNotificationWorker. log**

## <a name="next-steps"></a>Další kroky

Další informace o tom, jak klient připojovat soubory protokolů, najdete v tématu [řešení potíží s připojením tenanta](troubleshoot.md).
